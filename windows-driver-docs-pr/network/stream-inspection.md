---
title: 流检查
description: 流检查
keywords:
- 流检查 WDK Windows 筛选平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b04adf77b45a27fa7e285d82ddcd0417af0083c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818329"
---
# <a name="stream-inspection"></a>流检查


## <a name="inline-stream-inspection"></a>内联流检查


内联流修饰符可以通过在从 [*classifyFn*](/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_classify_fn0) CALLOUT 函数返回 **.fwp \_ 操作 \_ 允许** 或 **.Fwp \_ 操作 \_ 块** 时，通过设置 [**FWPS \_ 流 \_ CALLOUT \_ IO \_ PACKET0**](/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-fwps_stream_callout_io_packet0_)结构的 **countBytesEnforced** 成员的值，来允许或阻止部分指示的数据，从而编辑流数据。 它们还可以调用 [**FwpsStreamInjectAsync0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsstreaminjectasync0) 函数来向流中添加新内容。 此内容可以是新内容，也可以替换已阻止的数据。

若要替换在指定段中间找到的模式 (例如， *n* 个字节后跟一个 *p* 字节的模式，后跟 *m* 字节) ，则标注将遵循以下步骤：

1.  使用 *classifyFn* *n*  +  *p*  +  *m* 字节调用标注的 classifyFn 函数。

2.  标注返回允许将 **countBytesEnforced** 成员设置为 *n* 的 **.fwp \_ 操作 \_** 。

3.  再次调用带有 *classifyFn* *p*  +  *m* 字节的标注的 classifyFn 函数。 如果 **countBytesEnforced** 小于指定的量，WFP 将再次调用 *classifyFn* 。

4.  在 *classifyFn* 函数中，标注调用 *FwpsStreamInjectAsync0* 函数来注入替换模式 *p*。 然后，标注返回 **countBytesEnforced** 设置为 *p* 的 **.fwp \_ 操作 \_ 块**。

5.  再次调用带有 *m* 个字节的标注的 *classifyFn* 函数。

6.  标注返回 **countBytesEnforced** 设置为 *m* 的 **.fwp \_ 操作 \_ 块**。

如果指示的数据对于标注来说不足以做出检查决定，则它可以将 [**FWPS \_ 流 \_ 标注 \_ IO \_ PACKET0**](/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-fwps_stream_callout_io_packet0_)结构的 **streamAction** 成员设置为 **FWPS \_ STREAM \_ 操作 \_ 需要 \_ 更多 \_ 数据**，并将 **countBytesRequired** 成员设置为最小值。 如果设置了 **streamAction** ，则标注应从 *ClassifyFn* 函数返回 **.fwp \_ 操作 \_ NONE** 。

如果设置了 **FWPS \_ 流 \_ 操作 \_ 需要 \_ 更多 \_ 数据** ，则 WFP 最多可以累积到 8 MB 的流数据。 在调用标注的 *classifyFn* 函数时，WFP 会将 "已 **\_ 达到 FWPS 分类 \_ \_ 标志 \_ 缓冲区 \_ 限制 \_** " 标记设置为 "已达到"。 设置后一标志时，标注必须完全接受所指示的数据。 当 FWPS 不使用其他 **\_ \_ \_ \_ \_ \_ 数据** 标志时，标注不得返回 **FWPS \_ STREAM \_ 操作 \_ 需要 \_ 更多 \_ 数据**。

为了方便能够从平面缓冲区扫描流模式，WFP 提供了 [**FwpsCopyStreamDataToBuffer0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpscopystreamdatatobuffer0) 实用工具函数，该函数可以将指示的流数据复制到一个连续的缓冲区中。

## <a name="out-of-band-stream-inspection"></a>带外流检测


对于带外检查或修改，流标注将遵循与数据包检查标注类似的模式：它首先克隆所有指示的流段以进行延迟处理，然后它会阻止这些段。 稍后会将已检查或修改的数据注入回数据流。 在带外插入数据时，标注必须返回所有指定段上的 **.Fwp \_ 操作 \_ 块** ，以确保生成的流的完整性。 带外检查模块不能随意注入某个 FIN (这表示发件人) 没有更多数据进入传出数据流。 如果该模块必须删除连接，则其 *classifyFn* callout 函数必须将 [**FWPS \_ 流 \_ 标注 \_ IO \_ PACKET0**](/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-fwps_stream_callout_io_packet0_)结构的 **streamAction** 成员设置为 **FWPS \_ stream \_ 操作 \_ 断开 \_ 连接**。

由于流数据可以表示为 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 链，因此，.fwp 提供了在网络缓冲区列表链上操作的 [**FwpsCloneStreamData0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsclonestreamdata0) 和 [**FwpsDiscardClonedStreamData0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsdiscardclonedstreamdata0) 实用工具函数。

WFP 还支持传入方向的流数据限制。 如果某个标注不能跟上传入的数据速率，则它可以返回 **FWPS \_ 流 \_ 操作 \_ 延迟** 为 "暂停" 流。 然后，可以通过调用 [**FwpsStreamContinue0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsstreamcontinue0) 函数 "恢复" 流。 使用此函数延迟流会导致 TCP/IP 堆栈停止确认处理传入的数据。 这会导致 TCP 滑动窗口向0减小。

对于带外流检查标注，调用 **FwpsStreamInjectAsync0** 函数时不得调用 [**FwpsStreamContinue0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsstreamcontinue0) 。

注入的流数据将不会被重新指明给标注，但会提供给低权重子层的流标注。

GitHub 上的[windows 驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=616507)存储库中的[Windows 筛选平台流编辑示例](https://go.microsoft.com/fwlink/p/?LinkId=617933)显示了如何在流层执行内联和带外编辑。

**注意**  Windows Server 2008 和更高版本不支持在以下过程中删除流筛选器：
-   标注正在执行带外数据包注入。

-   标注正在请求更多数据，方法是将 [**FWPS \_ 流 \_ 标注 \_ IO \_ PACKET0**](/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-fwps_stream_callout_io_packet0_)结构的 **streamAction** 成员设置为 **FWPS \_ STREAM \_ 操作 \_ 需要 \_ 更多 \_ 数据**。

-   标注正在延迟流，方法是将 [**FWPS \_ 流 \_ 标注 \_ IO \_ PACKET0**](/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-fwps_stream_callout_io_packet0_)结构的 **streamAction** 成员设置为 **FWPS \_ stream \_ 操作 \_ 延迟**。

 

## <a name="dynamic-stream-inspection"></a>动态流检查


Windows 7 和更高版本支持动态流检查。 动态流检查对现有流数据流进行操作，而不是创建和撕裂新流。 可以 **Flags** 执行动态流 [**\_**](/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-fwps_callout2_) [**\_**](/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-fwps_callout1_) **\_ \_ \_ \_ \_ \_ 检查** 的标注驱动程序应在 FWPS CALLOUT1 或 FWPS CALLOUT2 结构的 Flags 成员中设置 .fwp 标注标志。

## <a name="avoiding-unnecessary-inspections"></a>避免不必要的检查


若要仅对驱动程序所感兴趣的连接执行流检查，标注可以在 [**FWPS \_ CALLOUT0**](/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-fwps_callout0_)结构的 **Flags** 成员中设置 " **\_ \_ \_ \_ \_ 流上有条件**" 标记。 将忽略所有其他连接的此标注。 性能将得到改进，驱动程序将不需要维护不必要的状态数据。

## <a name="stream-layer-waterfall-model"></a>流层瀑布模型

WFP 中的流层遵循严格的瀑布模型;也就是说，仅当之前的标注 (任何) 显式允许的情况下，才允许此层中的标注检查流段。 如果标注阻止指示的段，则会永久从流中取出该段，并且不允许任何标注对其进行检查。

而且

1. 流层上的每个非检查标注都必须显式为 *classifyOut* 参数的 **actionType** 成员赋值，而不考虑以前在该参数中设置的值。
2. *ClassifyOut* 参数的 **权限** 成员中的 **FWPS \_ 右 \_ 操作 \_ 写入** 标志在 WFP 流层中没有任何意义。 此层上的标注不应检查是否存在此标志。 无论 *classifyOut* 的值是什么，标注都可以处理指示的 *layerData* 参数 -> **rights**。

 


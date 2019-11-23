---
title: 流检查
description: 流检查
ms.assetid: 77e152bf-cb6b-4845-9a5e-9c37281f23f1
keywords:
- 流检查 WDK Windows 筛选平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3ae108552f7a5037d3fe1080dbcba62e5e44a47
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841817"
---
# <a name="stream-inspection"></a>流检查


## <a name="inline-stream-inspection"></a>内联流检查


内联流修饰符可以通过将 FWPS\_流中的 CountBytesEnforced 成员的值设置 **\_** 为[ **\_\_\_流**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-fwps_stream_callout_io_packet0_)的值来编辑流数据，方法是将流的 " " 成员的[*值设置为*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_classify_fn0)""\_\_\_ 它们还可以调用[**FwpsStreamInjectAsync0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsstreaminjectasync0)函数来向流中添加新内容。 此内容可以是新内容，也可以替换已阻止的数据。

若要替换在指示的段中间找到的模式（例如*n*个字节，后跟一个*p*字节后跟*m*个字节的模式），则标注将遵循以下步骤：

1.  使用*n* + *p* + *m*字节调用标注的*classifyFn*函数。

2.  标注返回 **\_操作的\_允许**，并将**countBytesEnforced**成员设置为*n*。

3.  再次调用标注的*classifyFn*函数， *p* + *m*个字节。 如果**countBytesEnforced**小于指定的量，WFP 将再次调用*classifyFn* 。

4.  在*classifyFn*函数中，标注调用*FwpsStreamInjectAsync0*函数来注入替换模式*p*。 然后，标注会返回**countBytesEnforced**设置为*p* **\_块的 .fwp\_操作**。

5.  再次调用带有*m*个字节的标注的*classifyFn*函数。

6.  标注返回 **\_操作的\_块的 .fwp** ，并将**其设置为** *m*。

如果指示的数据对于标注来说不足以做出检查决定，则它可以将 FWPS\_流的**streamAction**成员设置为[ **\_标注\_IO\_PACKET0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-fwps_stream_callout_io_packet0_)结构设置为**FWPS\_流\_操作\_需要\_更多的数据**，并将**countBytesRequired**成员设置为最小值。\_ 如果设置了**streamAction** ，则标注应\_从*ClassifyFn*函数返回 **.fwp\_操作**。

当**FWPS\_stream\_操作\_需要\_更多\_数据**时，WFP 可以累积最多 8 MB 的流数据。 在调用标注的*classifyFn*函数时，WFP 会将 " **FWPS\_分类\_的"\_标志\_缓冲区\_** "已达到" 标志设置为 "已达到限制"。\_ 设置后一标志时，标注必须完全接受所指示的数据。 当**FWPS\_分类**\_\_\_\_标志时，标注不能返回**FWPS\_STREAM\_操作\_需要\_更多的数据**。\_\_

为了方便能够从平面缓冲区扫描流模式，WFP 提供了[**FwpsCopyStreamDataToBuffer0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpscopystreamdatatobuffer0)实用工具函数，该函数可以将指示的流数据复制到一个连续的缓冲区中。

## <a name="out-of-band-stream-inspection"></a>带外流检测


对于带外检查或修改，流标注将遵循与数据包检查标注类似的模式：它首先克隆所有指示的流段以进行延迟处理，然后它会阻止这些段。 稍后会将已检查或修改的数据注入回数据流。 在带外注入数据时，标注必须返回所有指定段上的 **\_操作\_块的 .fwp** ，以确保生成的流的完整性。 带外检查模块不能将 FIN （表示没有来自发件人的更多数据）注入到传出数据流。 如果该模块必须删除连接，则其*classifyFn* callout 函数必须将 FWPS\_流的**streamAction**成员（ [ **\_标注\_IO\_PACKET0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-fwps_stream_callout_io_packet0_)结构设置为**FWPS\_流\_操作\_丢弃\_连接**。

由于流数据可以表示为[**网络\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)链，因此，.fwp 提供了在网络缓冲区列表链上操作的[**FwpsCloneStreamData0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsclonestreamdata0)和[**FwpsDiscardClonedStreamData0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsdiscardclonedstreamdata0)实用工具函数。

WFP 还支持传入方向的流数据限制。 如果某一标注不能跟上传入的数据速率，则它可以返回**FWPS\_流\_操作\_延迟**为 "暂停" 流。 然后，可以通过调用[**FwpsStreamContinue0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsstreamcontinue0)函数 "恢复" 流。 使用此函数延迟流会导致 TCP/IP 堆栈停止确认处理传入的数据。 这会导致 TCP 滑动窗口向0减小。

对于带外流检查标注，调用**FwpsStreamInjectAsync0**函数时不得调用[**FwpsStreamContinue0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsstreamcontinue0) 。

注入的流数据将不会被重新指明给标注，但会提供给低权重子层的流标注。

GitHub 上的[windows 驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=616507)存储库中的[Windows 筛选平台流编辑示例](https://go.microsoft.com/fwlink/p/?LinkId=617933)显示了如何在流层执行内联和带外编辑。

**请注意**  Windows Server 2008 和更高版本不支持在以下过程中删除流筛选器：
-   标注正在执行带外数据包注入。

-   标注正在请求更多数据，方法是：将 FWPS\_流的**streamAction**成员设置为[ **\_标注\_IO\_PACKET0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-fwps_stream_callout_io_packet0_)结构设置为 FWPS\_\_\_\_\_**需要更多数据**。

-   标注正在延迟流，方法是将 FWPS\_流的**streamAction**成员设置[ **\_标注\_IO\_PACKET0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-fwps_stream_callout_io_packet0_)结构设置为**FWPS\_** \_\_操作。

 

## <a name="dynamic-stream-inspection"></a>动态流检查


Windows 7 和更高版本支持动态流检查。 动态流检查对现有流数据流进行操作，而不是创建和撕裂新流。 可以执行动态流检查的标注驱动程序应将 **.fwp\_标注\_标志\_允许** [**FWPS\_CALLOUT1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-fwps_callout1_)或[**FWPS\_CALLOUT2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-fwps_callout2_)结构的**Flags**成员中\_中\_流\_检查标志。

## <a name="avoiding-unnecessary-inspections"></a>避免不必要的检查


若要仅对驱动程序所感兴趣的连接执行流检查，标注可以在[**FWPS\_CALLOUT0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-fwps_callout0_)结构的**Flags**成员的 **\_FLOW 标志上设置 .fwp\_标注\_\_\_标志**。 将忽略所有其他连接的此标注。 性能将得到改进，驱动程序将不需要维护不必要的状态数据。

## <a name="stream-layer-waterfall-model"></a>流层瀑布模型

WFP 中的流层遵循严格的瀑布模型;也就是说，仅当上一标注（如果有）明确允许时，才允许此层中的标注检查流段。 如果标注阻止指示的段，则会永久从流中取出该段，并且不允许任何标注对其进行检查。

而且

1. 流层上的每个非检查标注都必须显式为*classifyOut*参数的**actionType**成员赋值，而不考虑以前在该参数中设置的值。
2. *ClassifyOut*参数的**权限**成员中的**FWPS\_RIGHT\_操作\_写入**标志在 WFP 流层中没有任何意义。 此层上的标注不应检查是否存在此标志。 无论*classifyOut*的值->**权限**如何，标注都可以处理指示的*layerData*参数。

 

 






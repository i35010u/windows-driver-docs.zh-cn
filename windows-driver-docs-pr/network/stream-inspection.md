---
title: 流检查
description: 流检查
ms.assetid: 77e152bf-cb6b-4845-9a5e-9c37281f23f1
keywords:
- 流检查 WDK Windows 筛选平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bcd0517c6f1d33bf4be18ed732c657c06bfac3c1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370585"
---
# <a name="stream-inspection"></a>流检查


## <a name="inline-stream-inspection"></a>内联 Stream 检查


内联流修饰符可以编辑流数据来允许或阻止通过设置的值所指示的数据的一部分**countBytesEnforced**的成员[ **FWPS\_流\_标注\_IO\_PACKET0** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/ns-fwpsk-fwps_stream_callout_io_packet0_)结构，因为它们返回**FWP\_操作\_允许**或**FWP\_操作\_阻止**从[ *classifyFn* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nc-fwpsk-fwps_callout_classify_fn0)标注函数。 它们还可以调用[ **FwpsStreamInjectAsync0** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsstreaminjectasync0)函数以将新内容添加到流。 此内容可以是新也可以替换已阻止的数据。

替换模式中间指示段 (例如， *n*字节后跟的模式*p*字节后跟*m*字节)，遵循标注以下步骤：

1.  标注*classifyFn*函数通过使用调用*n* + *p* + *m*字节。

2.  返回标注**FWP\_操作\_允许**与**countBytesEnforced**成员设置为*n*。

3.  标注*classifyFn*使用再次调用函数*p* + *m*字节。 将调用 WFP *classifyFn*试如果**countBytesEnforced**小于指定的量。

4.  从*classifyFn*函数，标注调用*FwpsStreamInjectAsync0*函数注入替换模式*p*。 然后返回标注**FWP\_操作\_阻止**与**countBytesEnforced**设置为*p*。

5.  标注*classifyFn*使用再次调用函数*m*字节。

6.  返回标注**FWP\_操作\_阻止**与**countBytesEnforced**设置为*m*。

如果所指示的数据不足，无法进行检查决策的标注，它可以设置**streamAction**的成员[ **FWPS\_流\_标注\_IO\_PACKET0** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/ns-fwpsk-fwps_stream_callout_io_packet0_)结构**FWPS\_流\_操作\_需要\_详细\_数据**并设置**countBytesRequired**之前再次指示数据应累计的最少工作量 WFP 的成员。 当**streamAction** ，则应返回标注**FWP\_操作\_NONE**从*classifyFn*函数。

WFP 会累积最多 8 MB 中的数据进行流式传输时**FWPS\_流\_操作\_需要\_详细\_数据**设置。 将设置 WFP **FWPS\_分类\_OUT\_标志\_缓冲区\_限制\_已达到**标记时调用的标注*classifyFn*函数和缓冲区空间用尽。 设置后一种标志后，标注必须接受完整中指示的数据。 不能返回一个标注**FWPS\_流\_操作\_需要\_详细\_数据**时**FWPS\_分类\_OUT\_标志\_否\_详细\_数据**设置标志。

为能够扫描从平面缓冲区的流模式的方便起见，提供 WFP [ **FwpsCopyStreamDataToBuffer0** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpscopystreamdatatobuffer0)实用工具函数，可以将复制到连续指示流数据缓冲区。

## <a name="out-of-band-stream-inspection"></a>带外 Stream 检查


对于带外检查或修改，流标注应遵循的数据包检查标注类似的模式： 它首先将克隆的延迟处理的所有指示的流段，然后它会阻止这些段。 经检查或修改的数据更高版本注入到数据流中。 必须返回时将注入数据扩展外，标注**FWP\_操作\_阻止**上所有指示段，以确保生成的流的完整性。 带外检查模块必须任意注入 FIN （这表明从发送方没有更多数据） 到输出的数据流。 如果该模块必须删除此连接，其*classifyFn*标注函数必须设置**streamAction**的成员[ **FWPS\_流\_标注\_IO\_PACKET0** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/ns-fwpsk-fwps_stream_callout_io_packet0_)结构**FWPS\_流\_操作\_删除\_连接**.

由于流数据可以作为表明[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)链接，提供了 FWP [ **FwpsCloneStreamData0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsclonestreamdata0)并[ **FwpsDiscardClonedStreamData0** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsdiscardclonedstreamdata0)实用工具函数进行操作的净缓冲区列表链。

WFP 还支持对传入的方向的阻止的流数据。 如果一个标注无法跟上传入的数据速率，它可以返回**FWPS\_流\_操作\_DEFER**地"暂停"流。 流可以然后"恢复"通过调用[ **FwpsStreamContinue0** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsstreamcontinue0)函数。 延迟的流，此函数会导致停止确认处理传入数据的 TCP/IP 堆栈。 这将导致 TCP 滑动窗口以减少到 0。

有关带外流检查标注[ **FwpsStreamContinue0** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsstreamcontinue0)不得调用时**FwpsStreamInjectAsync0**调用函数。

注入的流数据将不会重新指定为标注，但它将可供流标注从较低权重子图层。

[Windows 筛选平台 Stream 编辑示例](https://go.microsoft.com/fwlink/p/?LinkId=617933)中[Windows 驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=616507)GitHub 上的存储库演示如何执行内联和带外编辑流层。

**请注意**  Windows Server 2008 和更高版本不支持以下进程期间删除的流筛选器：
-   标注正在执行的带数据包注入。

-   标注请求更多的数据，通过设置**streamAction**的成员[ **FWPS\_流\_标注\_IO\_PACKET0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/ns-fwpsk-fwps_stream_callout_io_packet0_)结构**FWPS\_流\_操作\_需要\_详细\_数据**。

-   标注通过设置延迟流**streamAction**的成员[ **FWPS\_流\_标注\_IO\_PACKET0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/ns-fwpsk-fwps_stream_callout_io_packet0_)结构**FWPS\_流\_操作\_DEFER**。

 

## <a name="dynamic-stream-inspection"></a>动态 Stream 检查


Windows 7 和更高版本支持动态流检查。 通过动态流检测对现有的流数据流动，而不是创建和关闭新建一个。 可以执行动态流检查的标注驱动程序应设置**FWP\_标注\_标志\_允许\_MID\_流\_检查**中的标志**标志**的成员[ **FWPS\_CALLOUT1** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/ns-fwpsk-fwps_callout1_)或[ **FWPS\_CALLOUT2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/ns-fwpsk-fwps_callout2_)结构。

## <a name="avoiding-unnecessary-inspections"></a>避免不必要的检查


若要仅在驱动程序感兴趣的连接上执行流检查之外，标注可以设置**FWP\_标注\_标志\_条件\_ON\_流**中的标志**标志**的成员[ **FWPS\_CALLOUT0** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/ns-fwpsk-fwps_callout0_)结构。 此标注将在所有其他连接上被忽略。 将提高性能和驱动程序将无需维护不必要的状态数据。

## <a name="stream-layer-waterfall-model"></a>Stream 层瀑布模型

WFP 的流层遵循严格的瀑布式模型;也就是说，将允许在此层中的标注检查流段仅当显式允许的上一个标注 （如果有）。 如果一个标注阻止指示的段，该时间段永久移出流并无标注将允许对其进行检查。

此外：

1. 每个非检查标注流层必须显式将值赋给**actionType**的成员*classifyOut*而不考虑哪些值可能之前尚未设置中的参数参数。
2. **FWPS\_右\_操作\_编写**标志中**权限**的成员*classifyOut*参数具有任何重要性在 WFP 流层。 在此层的标注应检查存在此标志。 可以处理所指示的标注*数据*而不考虑的值的参数*classifyOut*->**权限**。

 

 






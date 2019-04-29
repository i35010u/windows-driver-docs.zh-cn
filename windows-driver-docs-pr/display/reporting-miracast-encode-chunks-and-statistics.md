---
title: 报告 Miracast 编码区块和统计信息
description: 显示硬件可以处理通过 Miracast 无线显示链接发送通过将帧拆分成多个部分，每个视频帧或编码的区块。
ms.assetid: E1CE637F-42ED-4BEB-A2FF-04B4B88469DC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b9770ebb7be1d5e2ff1a4af05051baafd522074
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383267"
---
# <a name="reporting-miracast-encode-chunks-and-statistics"></a>报告 Miracast 编码区块和统计信息


显示硬件可以处理通过 Miracast 无线显示链接发送通过将帧拆分成多个部分，每个视频帧或*编码的区块*。 每个区块具有从帧数和框架部分 （或扇区） 号生成一个唯一的块 ID。 必须将与相同的桌面框架更新每个区块分配相同的帧数。

## <a name="span-idreportingchunkprocessingspanspan-idreportingchunkprocessingspanspan-idreportingchunkprocessingspanreporting-chunk-processing"></a><span id="Reporting_chunk_processing"></span><span id="reporting_chunk_processing"></span><span id="REPORTING_CHUNK_PROCESSING"></span>报告区块处理


驱动程序可以对要在多个通过 Miracast 无线链接发送的帧进行编码的处理步骤 — 例如分隔从编码的颜色转换，或在单个步骤中。 应在框架内的唯一帧部件号分配每个处理步骤。

Miracast 用户模式驱动程序或显示微型端口驱动程序必须通知操作系统每次硬件已完成，框架和每个帧的一部分发送到网络之前的处理步骤。 特定的报告的处理步骤的时间将假定为事件报告给操作系统，因此，必须以尽可能最快报告阶段的时间。

操作系统而不执行任何操作来记录这些事件使用 Windows 事件跟踪 (ETW) 内核级别跟踪工具。 此信息至关重要，不过以测量和调查性能问题。

这些是驱动程序可以提供通知的可能方法：

-   Miracast 用户模式驱动程序调用[ **ReportStatistic** ](https://msdn.microsoft.com/library/windows/hardware/dn265503)回调函数来报告的详细信息与**MIRACAST\_统计信息\_类型\_区块\_处理\_完成**类型，或使用**MIRACAST\_统计信息\_类型\_区块\_SENT**到指示区块是刚要传输的发送到网络堆栈。
-   显示微型端口驱动程序报告的区块处理的详细信息**DXGK\_中断\_MICACAST\_区块\_处理\_完成**中断键入，尽管此报表只能在中断时进行日志记录块区信息的补充，在区块数据包创建并已排队，以便于 Miracast 用户模式驱动程序可以通过调用检索它[ **GetNextChunkData** ](https://msdn.microsoft.com/library/windows/hardware/dn265462)回调函数。
-   显示微型端口驱动程序调用[ **DxgkCbReportChunkInfo** ](https://msdn.microsoft.com/library/windows/hardware/dn344647)任何 IRQL 级别的回调函数。 此函数日志仅区块信息并不会排队区块的任何数据包。

如果不更新桌面映像，但该驱动程序必须对桌面的图像，也能提高质量进行编码，应使用相同的帧数和部件号。 性能工具将触发第二个相同的帧和部件号，指示执行了相同的框架的第二个编码进行编码完成事件。

**请注意**  最后一个切片的每个帧必须具有零帧部件号。 执行此操作指示性能工具，这是最后一个帧的切片。

 

若要确保正确同步主图面上，如果任何请求的像素管道执行的编码，则在访问主表面的编码完成之前，不应报告间隔 VSync 翻转操作。 这可以防止表示器呈现到主图面时从其读取编码引擎。

Miracast 用户模式驱动程序应告知操作系统每一个处理帧的几个阶段：

<span id="Start_frame__chunk_type__MIRACAST_CHUNK_TYPE_FRAME_START_"></span><span id="start_frame__chunk_type__miracast_chunk_type_frame_start_"></span><span id="START_FRAME__CHUNK_TYPE__MIRACAST_CHUNK_TYPE_FRAME_START_"></span>开始帧、 类型消息的分块**MIRACAST\_区块\_类型\_帧\_启动**:  
表示其中操作系统要求驱动程序以显示新的桌面框架的点。 尽管从技术上讲这无法报告的 Miracast 用户模式驱动程序，开始处理新帧将始终涉及显示微型端口驱动程序，应由该驱动程序报告。

<span id="Color_convert_complete__chunk_type_MIRACAST_CHUNK_TYPE_COLOR_CONVERT_COMPLETE_"></span><span id="color_convert_complete__chunk_type_miracast_chunk_type_color_convert_complete_"></span><span id="COLOR_CONVERT_COMPLETE__CHUNK_TYPE_MIRACAST_CHUNK_TYPE_COLOR_CONVERT_COMPLETE_"></span>颜色转换完成，类型消息的分块**MIRACAST\_区块\_类型\_颜色\_转换\_完成**:  
某些解决方案都具有单独的颜色转换和编码阶段。 在此类解决方案中的颜色转换完成处理事件应会报告越早越好，并且驱动程序应使用[ **DXGK\_MIRACAST\_区块\_信息**](https://msdn.microsoft.com/library/windows/hardware/dn322056).**ProcessingTime**成员以报告的硬件来执行该操作所花费的时间。 如果整个框架的颜色转换一次性而不是在切片，部件号应为零。

<span id="Encode_complete__chunk_type_MIRACAST_CHUNK_TYPE_ENCODE_COMPLETE_"></span><span id="encode_complete__chunk_type_miracast_chunk_type_encode_complete_"></span><span id="ENCODE_COMPLETE__CHUNK_TYPE_MIRACAST_CHUNK_TYPE_ENCODE_COMPLETE_"></span>编码完成，类型消息的分块**MIRACAST\_区块\_类型\_编码\_完成**:  
指示 H.264 编码已完成。 **ProcessingTime**并**EncodeRate**的成员[ **DXGK\_MIRACAST\_块区\_信息**](https://msdn.microsoft.com/library/windows/hardware/dn322056)结构应已完成。

<span id="Frame_send__calling_ReportStatistic_using_MIRACAST_STATISTIC_TYPE_CHUNK_SENT_"></span><span id="frame_send__calling_reportstatistic_using_miracast_statistic_type_chunk_sent_"></span><span id="FRAME_SEND__CALLING_REPORTSTATISTIC_USING_MIRACAST_STATISTIC_TYPE_CHUNK_SENT_"></span>帧发送，请调用[ **ReportStatistic** ](https://msdn.microsoft.com/library/windows/hardware/dn265503)使用**MIRACAST\_统计信息\_类型\_块区\_SENT**:  
指示此帧/部件号的数据包不只是要从支持 Miracast 的用户模式驱动程序发送到传输的网络 API。 如果使用多个网络 API 调用发送此帧/部分数据，则这应仅记录发送的第一个数据包之前。 调用以指示这应在调用网络 API 之前。 这非常重要，因为如果网络 API 块调用，然后我们不希望该阻塞的时间计算在内的帧的图形堆栈的处理。

<span id="Dropped_frame__chunk_type__MIRACAST_CHUNK_TYPE_FRAME_DROPPED_"></span><span id="dropped_frame__chunk_type__miracast_chunk_type_frame_dropped_"></span><span id="DROPPED_FRAME__CHUNK_TYPE__MIRACAST_CHUNK_TYPE_FRAME_DROPPED_"></span>已删除的帧、 块类型**MIRACAST\_区块\_类型\_帧\_丢弃**:  
如果在任何时候驱动程序决定它不会完成处理的帧/部件并将其发送到接收器，它应该报告已删除的帧。 在此上下文中一个帧时，才考虑删除该驱动程序实际已开始处理它的日志记录**MIRACAST\_区块\_类型\_帧\_启动**。 如果驱动程序计算，它将跳过此帧，而无需任何处理，它可以记录**MIRACAST\_区块\_类型\_帧\_丢弃**无需登录**MIRACAST\_区块\_类型\_帧\_启动**。

<span id="Driver_defined_chunk_type_MIRACAST_CHUNK_TYPE_ENCODE_DRIVER_DEFINED_1_or__2_"></span><span id="driver_defined_chunk_type_miracast_chunk_type_encode_driver_defined_1_or__2_"></span><span id="DRIVER_DEFINED_CHUNK_TYPE_MIRACAST_CHUNK_TYPE_ENCODE_DRIVER_DEFINED_1_OR__2_"></span>驱动程序定义的块类型**MIRACAST\_区块\_类型\_编码\_驱动程序\_定义\_1**或 **\_2**:  
这些区块类型是可用于帮助你了解方案的性能。 示例将驱动程序在其中使用这些类型指示为此帧已创建一个 I 帧。 另一个示例就是其中驱动程序日志的其他数据包后已与网络包含编码帧的总大小的 Api 发送帧的最后一个切片。

下面是如何转换框架颜色，然后显示微型端口驱动程序如何报告完成的颜色转换的示例。

**报告单个帧，而无需使用切片：**

值[ **MIRACAST\_区块\_信息**](https://msdn.microsoft.com/library/windows/hardware/dn265473)成员：**ChunkType**值**ChunkId**。
**ChunkId**。
处理 MIRACAST 阶段\_区块\_类型\_FrameNumber PartNumber ProcessingTime EncodeRate 开始处理帧**帧\_启动**101 0 0 0 颜色转换为完整**颜色\_转换\_** **完成**101 0 950 0 编码已完成**编码\_** **COMPLETE** 101 0 1042年 15000 就调用，以将数据发送到网络之前[ **ReportStatistic** ](https://msdn.microsoft.com/library/windows/hardware/dn265503)调用\*101，值为**ChunkSent**. **ChunkId**。 **FrameNumber**的值 0， **ChunkSent**。 **ChunkId**。 **PartNumber** N/A N/A
 

\*使用调用**MIRACAST\_统计信息\_类型\_区块\_SENT**。

**报告单个帧，使用切片处理：**

值[ **MIRACAST\_区块\_信息**](https://msdn.microsoft.com/library/windows/hardware/dn265473)成员：**ChunkType**
**ChunkId**。
**ChunkId**。
处理 MIRACAST 阶段\_区块\_类型\_FrameNumber PartNumber ProcessingTime EncodeRate 开始处理帧**帧\_启动**101 0 0 0 颜色转换为完整**颜色\_转换\_** **完成**101 0 950 的段 1 0 编码已完成**编码\_** **完整**101 1 1042年 15000 编码切片 2 是完成**编码\_** **完整**101 0 400 15000 就之前调用发送切片 1 个数据网络[ **ReportStatistic** ](https://msdn.microsoft.com/library/windows/hardware/dn265503)调用\*101，值为**ChunkSent**。 **ChunkId**。 **FrameNumber**的值 1， **ChunkSent**。 **ChunkId**。 **PartNumber**不适用不适用只需调用发送之前对进行网络到 2 个数据切片[ **ReportStatistic** ](https://msdn.microsoft.com/library/windows/hardware/dn265503)调用\*101，值**ChunkSent**。 **ChunkId**。 **FrameNumber**的值 0， **ChunkSent**。 **ChunkId**。 **PartNumber** （请参阅上面的说明。）N/A N/A
 

\*使用调用**MIRACAST\_统计信息\_类型\_区块\_SENT**。

**报告原始帧中，处理和重新编码而无需使用切片：**

值[ **MIRACAST\_区块\_信息**](https://msdn.microsoft.com/library/windows/hardware/dn265473)成员：**ChunkType**
**ChunkId**。
**ChunkId**。
处理 MIRACAST 阶段\_区块\_类型\_FrameNumber PartNumber ProcessingTime EncodeRate 开始处理帧**帧\_启动**101 0 0 0 颜色转换为完整**颜色\_转换\_** **完成**101 0 950 0 编码已完成**编码\_** **COMPLETE** 101 0 1042年 15000 就调用，以将原始帧中的数据发送到网络之前[ **ReportStatistic** ](https://msdn.microsoft.com/library/windows/hardware/dn265503)调用\*101，值为**ChunkSent**。 **ChunkId**。 **FrameNumber**的值 0， **ChunkSent**。 **ChunkId**。 **PartNumber**不适用不适用重新编码完毕**编码\_** **完成**101 0 500 15000 就调用，以将数据重新编码帧发送到网络之前[ **ReportStatistic** ](https://msdn.microsoft.com/library/windows/hardware/dn265503)调用\*101，值为**ChunkSent**。 **ChunkId**。 **FrameNumber**的值 0， **ChunkSent**。 **ChunkId**。 **PartNumber** N/A N/A
 

\*使用调用**MIRACAST\_统计信息\_类型\_区块\_SENT**。

## <a name="span-idreportingprotocoleventsspanspan-idreportingprotocoleventsspanspan-idreportingprotocoleventsspanreporting-protocol-events"></a><span id="Reporting_protocol_events"></span><span id="reporting_protocol_events"></span><span id="REPORTING_PROTOCOL_EVENTS"></span>报告协议事件


当 Miracast 用户模式驱动程序通过调用报告协议事件[ **ReportStatistic** ](https://msdn.microsoft.com/library/windows/hardware/dn265503)函数与[ **MIRACAST\_统计信息\_数据**](https://msdn.microsoft.com/library/windows/hardware/dn265479)。**StatisticType**设置为**MIRACAST\_统计信息\_类型\_事件**，操作系统将记录事件，但不执行任何其他操作。 不过，这些事件是诊断和性能调查的有价值。

[ **MIRACAST\_协议\_事件**](https://msdn.microsoft.com/library/windows/hardware/dn265477)枚举包括可报告的可能协议事件类型。

## <a name="span-idreportingprotocolerrorsspanspan-idreportingprotocolerrorsspanspan-idreportingprotocolerrorsspanreporting-protocol-errors"></a><span id="Reporting_protocol_errors"></span><span id="reporting_protocol_errors"></span><span id="REPORTING_PROTOCOL_ERRORS"></span>协议错误报告


尽管连接的 Miracast 会话是在进行中，如果 Miracast 用户模式驱动程序发现错误，则应调用[ **ReportSessionStatus** ](https://msdn.microsoft.com/library/windows/hardware/dn265502)具有相应的回调函数[**MIRACAST\_状态**](https://msdn.microsoft.com/library/windows/hardware/dn265481)中的错误状态信息*MiracastStatus*参数。 运行会话始终会销毁的会话时，会报告错误。

请注意，虽然操作系统只记录[ **ReportSessionStatus**](https://msdn.microsoft.com/library/windows/hardware/dn265502)*状态*诊断的参数，并且不会根据其值的任何操作。 但是，我们建议驱动程序使用此参数来区分不同的错误的原因。

 

 






---
title: 报告 Miracast 编码区块和统计信息
description: 显示硬件可以通过将帧拆分为多个部分或编码区块来处理通过 Miracast 无线显示链接发送的每个视频帧。
ms.assetid: E1CE637F-42ED-4BEB-A2FF-04B4B88469DC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2379210e7f533c86859aa156b329351202432ca3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825937"
---
# <a name="reporting-miracast-encode-chunks-and-statistics"></a>报告 Miracast 编码区块和统计信息


显示硬件可以通过将帧拆分为多个部分或*编码区块*来处理通过 Miracast 无线显示链接发送的每个视频帧。 每个区块都有一个从帧号和帧部分（或切片）编号生成的唯一区块 ID。 与相同桌面帧更新相关的每个区块都必须分配有相同的帧号。

## <a name="span-idreporting_chunk_processingspanspan-idreporting_chunk_processingspanspan-idreporting_chunk_processingspanreporting-chunk-processing"></a><span id="Reporting_chunk_processing"></span><span id="reporting_chunk_processing"></span><span id="REPORTING_CHUNK_PROCESSING"></span>报告区块处理


驱动程序可以将帧编码为在多个处理步骤（例如，从编码中分离颜色转换）或单个步骤中通过 Miracast 无线链接发送。 应在帧内为每个处理步骤分配一个唯一的帧部分号。

Miracast 用户模式驱动程序或显示微型端口驱动程序必须在每次硬件已经完成帧的处理步骤时，并且在框架的每个部分都发送到网络之前，通知操作系统。 将特定报告的处理步骤的时间假定为向操作系统报告事件的时间，因此，尽可能快地报告阶段非常重要。

除了使用 Windows 事件跟踪（ETW）内核级别跟踪功能记录这些事件外，操作系统不需要执行任何操作。 此信息对于测量和调查性能问题并不重要。

驱动程序可以使用以下方法提供通知：

-   Miracast 用户模式驱动程序调用[**ReportStatistic**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_report_statistic)回调函数以报告有关 MIRACAST\_统计信息的详细信息 **\_类型\_区块\_处理\_完整**类型或与**Miracast\_统计信息\_\_发送\_区块**，以指示区块只发送到网络堆栈进行传输。
-   显示微型端口驱动程序报告的区块处理详细信息 **\_中断\_MICACAST\_区块\_处理\_完整**中断类型，不过，这种情况下只能在中断时间执行此报告，除了记录区块信息外，还会创建和排队数据包，以便 Miracast 用户模式驱动程序可以通过调用[**GetNextChunkData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_get_next_chunk_data)回调函数来检索它。
-   显示微型端口驱动程序在任何 IRQL 级别调用[**DxgkCbReportChunkInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_miracast_report_chunk_info)回调函数。 此函数只记录区块信息，不会将任何区块数据包排队。

如果未更新桌面映像，但驱动程序需要再次对桌面图像进行编码以提高质量，则应使用相同的帧号和部件号。 性能工具将触发相同帧和部件号的第二个编码完成事件，指示已执行同一帧的第二个编码。

**请注意**  每个帧的最后一个切片的帧部分必须为零。 执行此操作会向性能工具指示这是帧的最后一个切片。

 

若要确保主图面的正确同步，如果该编码由像素管道执行，则在编码完成访问主图面之前，不应报告任何 VSync 时间间隔请求的反向操作。 这可以防止在编码引擎读取时，呈现器呈现到主要表面。

Miracast 用户模式驱动程序应在每个处理该帧的阶段通知操作系统：

<span id="Start_frame__chunk_type__MIRACAST_CHUNK_TYPE_FRAME_START_"></span><span id="start_frame__chunk_type__miracast_chunk_type_frame_start_"></span><span id="START_FRAME__CHUNK_TYPE__MIRACAST_CHUNK_TYPE_FRAME_START_"></span>开始帧，区块类型**MIRACAST\_区块\_类型\_帧\_开始**：  
表示操作系统要求驱动程序显示新桌面帧的点。 尽管从技术上讲，可以从 Miracast 用户模式驱动程序中报告这一点，但开始处理新帧始终涉及显示微型端口驱动程序，并且应由该驱动程序报告。

<span id="Color_convert_complete__chunk_type_MIRACAST_CHUNK_TYPE_COLOR_CONVERT_COMPLETE_"></span><span id="color_convert_complete__chunk_type_miracast_chunk_type_color_convert_complete_"></span><span id="COLOR_CONVERT_COMPLETE__CHUNK_TYPE_MIRACAST_CHUNK_TYPE_COLOR_CONVERT_COMPLETE_"></span>颜色转换完成，区块类型**MIRACAST\_区块\_类型\_颜色\_转换\_完成**：  
某些解决方案具有不同的颜色转换和编码阶段。 在此类解决方案中，应尽快报告颜色转换完成处理事件，并且驱动程序应使用[**DXGK\_MIRACAST\_区块\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-dxgk_miracast_chunk_info)。**ProcessingTime**成员报告硬件执行操作所需的时间。 如果整个帧是一次性转换的，而不是在切片中，则部件号应为零。

<span id="Encode_complete__chunk_type_MIRACAST_CHUNK_TYPE_ENCODE_COMPLETE_"></span><span id="encode_complete__chunk_type_miracast_chunk_type_encode_complete_"></span><span id="ENCODE_COMPLETE__CHUNK_TYPE_MIRACAST_CHUNK_TYPE_ENCODE_COMPLETE_"></span>编码完成，区块类型**MIRACAST\_区块\_类型\_编码\_完成**：  
指示已完成了 h.264 编码。 应完成[**DXGK\_MIRACAST\_区块\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-dxgk_miracast_chunk_info)结构的**ProcessingTime**和**EncodeRate**成员。

<span id="Frame_send__calling_ReportStatistic_using_MIRACAST_STATISTIC_TYPE_CHUNK_SENT_"></span><span id="frame_send__calling_reportstatistic_using_miracast_statistic_type_chunk_sent_"></span><span id="FRAME_SEND__CALLING_REPORTSTATISTIC_USING_MIRACAST_STATISTIC_TYPE_CHUNK_SENT_"></span>帧发送，使用 MIRACAST 调用[**ReportStatistic**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_report_statistic) **\_统计信息\_类型\_区块\_发送**：  
指示此帧/部件号的数据包即将发送到网络 API 以从 Miracast 用户模式驱动程序传输。 如果此帧/部件的数据是使用多个网络 API 调用发送的，则只应在发送第一个数据包之前记录。 指示此情况的调用应在调用网络 API 之前进行。 这一点很重要，因为如果网络 API 阻止调用，则不希望阻塞的时间计入图形堆栈中的帧的处理。

<span id="Dropped_frame__chunk_type__MIRACAST_CHUNK_TYPE_FRAME_DROPPED_"></span><span id="dropped_frame__chunk_type__miracast_chunk_type_frame_dropped_"></span><span id="DROPPED_FRAME__CHUNK_TYPE__MIRACAST_CHUNK_TYPE_FRAME_DROPPED_"></span>已删除帧，区块类型**MIRACAST\_区块\_类型\_帧\_已删除**：  
如果在任何时候驱动程序决定它不会完成帧/部件的处理并将其发送到接收器，则它应报告删除的帧。 在这种情况下，仅当驱动程序实际通过日志记录\_MIRACAST 开始处理时，才会将帧视为已删除， **\_类型\_帧\_开始**。 如果驱动程序计算它将跳过此帧而不进行任何处理，则它可以记录**miracast\_区块\_类型\_帧\_删除**，而不会记录 MIRACAST\_\_\_的\_**帧类型**。

<span id="Driver_defined_chunk_type_MIRACAST_CHUNK_TYPE_ENCODE_DRIVER_DEFINED_1_or__2_"></span><span id="driver_defined_chunk_type_miracast_chunk_type_encode_driver_defined_1_or__2_"></span><span id="DRIVER_DEFINED_CHUNK_TYPE_MIRACAST_CHUNK_TYPE_ENCODE_DRIVER_DEFINED_1_OR__2_"></span>驱动程序定义的区块类型**MIRACAST\_区块\_类型\_编码\_驱动程序\_定义\_1**或 **\_2**：  
这些区块类型可帮助你了解方案的性能。 例如，驱动程序使用这些类型指示已为此帧创建了一个 I 帧。 另一个示例是，在将帧的最后一个切片发送到包含编码的帧总大小的网络 Api 之后，驱动程序会记录其他数据包。

下面是有关如何转换框架颜色的示例，以及显示微型端口驱动程序如何报告颜色转换完成的示例。

**报告不使用切片的单个帧：**

[**MIRACAST\_区块\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdispumdddi/ns-netdispumdddi-miracast_chunk_info)成员： **ChunkType**值**ChunkId**的值。
**ChunkId**。
处理 MIRACAST\_ 区块\_类型的阶段\_ FrameNumber PartNumber ProcessingTime EncodeRate 开始处理帧**帧\_开始**101 0 0 0 颜色转换是完整的**颜色\_转换\_** **完整**的 101 0 950 0 编码是完整的**编码\_** 在调用将数据发送到网络[**ReportStatistic**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_report_statistic)调用\* 101， **ChunkSent**的值之前**完成**101 0 1042 15000。 **ChunkId**。 **FrameNumber** 0， **ChunkSent**的值。 **ChunkId**。 **PartNumber**不适用
 

使用**MIRACAST\_统计信息\_类型\_块区\_发送**\*调用。

**报告使用切片处理的单个帧：**

[**MIRACAST\_区块\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdispumdddi/ns-netdispumdddi-miracast_chunk_info)成员： **ChunkType**
**ChunkId**的值。
**ChunkId**。
处理 MIRACAST\_ 区块\_类型的阶段\_ FrameNumber PartNumber ProcessingTime EncodeRate 开始处理帧**帧\_开始**101 0 0 0 颜色转换是完整的**颜色\_转换\_** 切片1的**完整**101 0 950 0 编码是完成**编码\_** 切片2的**完成**101 1 1042 15000 编码是完成**编码\_** **完成**101 0 400 15000，就像调用将切片1数据发送到网络[**ReportStatistic**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_report_statistic)调用\* 101，值为**ChunkSent**。 **ChunkId**。 **FrameNumber** 1， **ChunkSent**的值。 **ChunkId**。 **PartNumber**在调用将切片2数据发送到网络[**ReportStatistic**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_report_statistic)调用\* 101，值为**ChunkSent**时，不能为 n/a。 **ChunkId**。 **FrameNumber** 0， **ChunkSent**的值。 **ChunkId**。 **PartNumber** （请参阅上面的说明）。不适用
 

使用**MIRACAST\_统计信息\_类型\_块区\_发送**\*调用。

**报告原始帧，处理后再重新编码，而不使用切片：**

[**MIRACAST\_区块\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdispumdddi/ns-netdispumdddi-miracast_chunk_info)成员： **ChunkType**
**ChunkId**的值。
**ChunkId**。
处理 MIRACAST\_ 区块\_类型的阶段\_ FrameNumber PartNumber ProcessingTime EncodeRate 开始处理帧**帧\_开始**101 0 0 0 颜色转换是完整的**颜色\_转换\_** **完整**的 101 0 950 0 编码是完整的**编码\_** 在调用以将原始帧的数据发送到网络[**ReportStatistic**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_report_statistic)调用\* 101， **ChunkSent**的值之前**完成**101 0 1042 15000。 **ChunkId**。 **FrameNumber** 0， **ChunkSent**的值。 **ChunkId**。 **PartNumber**N/A N/A 重新编码是完整的**编码\_** 在调用以将重新编码的帧发送到网络[**ReportStatistic**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_report_statistic)调用\* 101，值为**ChunkSent**的情况下，**完成**101 0 500 15000。 **ChunkId**。 **FrameNumber** 0， **ChunkSent**的值。 **ChunkId**。 **PartNumber**不适用
 

使用**MIRACAST\_统计信息\_类型\_块区\_发送**\*调用。

## <a name="span-idreporting_protocol_eventsspanspan-idreporting_protocol_eventsspanspan-idreporting_protocol_eventsspanreporting-protocol-events"></a><span id="Reporting_protocol_events"></span><span id="reporting_protocol_events"></span><span id="REPORTING_PROTOCOL_EVENTS"></span>报告协议事件


当 Miracast 用户模式驱动程序通过将[**ReportStatistic**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_report_statistic)函数与 Miracast 一起调用来报告协议事件时， [ **\_数据\_统计信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdispumdddi/ns-netdispumdddi-miracast_statistic_data)。**StatisticType**设置为**MIRACAST\_统计\_类型\_事件**，操作系统会记录事件，但不执行任何其他操作。 这些事件对于诊断和性能调查非常有用。

[**MIRACAST\_协议\_事件**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdispumdddi/ne-netdispumdddi-miracast_protocol_event)枚举包含可以报告的可能的协议事件类型。

## <a name="span-idreporting_protocol_errorsspanspan-idreporting_protocol_errorsspanspan-idreporting_protocol_errorsspanreporting-protocol-errors"></a><span id="Reporting_protocol_errors"></span><span id="reporting_protocol_errors"></span><span id="REPORTING_PROTOCOL_ERRORS"></span>报告协议错误


当 Miracast 连接会话正在进行时，如果 Miracast 用户模式驱动程序发现错误，则应在*MiracastStatus*参数中使用相应的[**Miracast\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdispumdddi/ne-netdispumdddi-miracast_status)错误状态信息调用[**ReportSessionStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_report_session_status)回调函数。 报告错误时，操作会话将始终销毁会话。

请注意，尽管操作系统只记录诊断的[**ReportSessionStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_report_session_status)*状态*参数，而不会根据其值执行任何操作。 但建议使用此参数来区分错误的不同原因。

 

 






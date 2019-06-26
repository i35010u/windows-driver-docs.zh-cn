---
title: SRB\_OPEN\_STREAM
description: SRB\_OPEN\_STREAM
ms.assetid: 53732add-e304-4128-9235-525ff073d777
keywords:
- SRB_OPEN_STREAM 流式处理媒体设备
topic_type:
- apiref
api_name:
- SRB_OPEN_STREAM
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a80cf5bab4605cb63573fba8c1b8efab22dc3462
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377885"
---
# <a name="srbopenstream"></a>SRB\_OPEN\_STREAM


## <span id="ddk_srb_open_stream_ks"></span><span id="DDK_SRB_OPEN_STREAM_KS"></span>


在类驱动程序将发送此请求打开的流。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

微型驱动程序应设置以下项之一为 SRB 中的状态：

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>状态\_成功  
指示命令成功完成。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>状态\_不\_实现  
指示该函数不受微型驱动程序。

<span id="STATUS_TOO_MANY_NODES"></span><span id="status_too_many_nodes"></span>状态\_过\_许多\_节点  
指示不资源不足，无法打开此流。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>状态\_IO\_设备\_错误  
指示发生了硬件故障。

### <a name="comments"></a>备注

在类驱动程序提供了[ **HW\_流\_对象**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_stream_object)中的缓冲区*pSrb* - &gt; **StreamObject**，使用*pSrb*-&gt;**StreamObject**-&gt;**StreamNumber**设置为流的数量，以打开。 *PSrb*指针指向[ **HW\_流\_请求\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_stream_request_block)结构。 **StreamNumber**对应于流中的偏移量[ **HW\_流\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_stream_descriptor)微型驱动程序提供响应的结构[**SRB\_获取\_流\_信息**](srb-get-stream-info.md)请求。 在类驱动程序指定打开的流应在提供的数据格式*pSrb*-&gt;**CommandData** - &gt; **OpenFormat**。

当微型驱动程序收到此请求时，它应确定是否可以在这一次打开指定的流。 微型驱动程序还应验证[ **KSDATAFORMAT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksdataformat)格式传递。 SRB OpenFormat 字段。 如果可以打开流，微型驱动程序更新 HW\_流\_对象的结构，并返回状态\_成功。 如果最大流实例数已打开，或打开此流所需的硬件资源不可用，微型驱动程序将返回相应的错误状态。

**当 SRB\_打开\_微型驱动程序收到流命令时，微型驱动程序应：**

1.  检查尚未超过最大流实例数，以及流索引值有效。

2.  检查请求的数据格式有效此流。

3.  流的格式设置。

4.  维护设备扩展中的所有流扩展结构的数组，以便可以从任何流取消 Irp。

5.  指定指针、 中到流数据处理程序和控件处理程序的流对象。

6.  在流中的 DMA 标志对象数据如果设备将直接执行 DMA 缓冲区地址集传递到**ReceiveDataPacket**例程。 如果驱动程序访问数据缓冲区中使用逻辑寻址传递，还设置 PIO 标志的流对象中。

7.  如果时钟支持在流上可用，此信息指示通过**HwClockObject**流对象中的成员。

 

 






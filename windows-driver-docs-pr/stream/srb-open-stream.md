---
title: SRB\_打开\_流
description: SRB\_打开\_流
ms.assetid: 53732add-e304-4128-9235-525ff073d777
keywords:
- SRB_OPEN_STREAM 流媒体设备
topic_type:
- apiref
api_name:
- SRB_OPEN_STREAM
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c5731cd17a738868667a0bd25e9c2906eda6556
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843290"
---
# <a name="srb_open_stream"></a>SRB\_打开\_流


## <span id="ddk_srb_open_stream_ks"></span><span id="DDK_SRB_OPEN_STREAM_KS"></span>


类驱动程序发送此请求以打开流。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

微型驱动程序应将以下内容之一设置为 SRB 中的状态：

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>成功\_状态  
指示命令成功完成。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>状态\_未\_实现  
指示微型驱动程序不支持该函数。

<span id="STATUS_TOO_MANY_NODES"></span><span id="status_too_many_nodes"></span>状态\_太\_许多\_节点  
指示没有足够的资源来打开此流。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>IO\_设备状态\_\_错误  
指示出现硬件故障。

### <a name="comments"></a>备注

类驱动程序在*pSrb*-&gt;**StreamObject**中提供了[**HW\_流\_对象**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_object)缓冲区， *pSrb*-&gt;**StreamObject**-&gt;**StreamNumber**设置为要打开的流的编号。 *PSrb*指针指向[**HW\_STREAM\_请求\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_request_block)结构。 **StreamNumber**对应于[**HW\_\_流**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_descriptor)中的流偏移量，微型驱动程序为响应[**SRB\_获取\_流\_INFO**](srb-get-stream-info.md)请求而提供此结构。 类驱动程序指定已打开的流应在*pSrb*-&gt;**CommandData**-&gt;**OpenFormat**中提供的数据格式。

当微型驱动程序收到此请求时，它应确定此时是否可以打开指定的流。 微型驱动程序还应验证传入的[**KSDATAFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)格式。 SRB 的 OpenFormat 字段。 如果流可以打开，则微型驱动程序会将 HW\_流更新\_对象结构，并返回状态\_SUCCESS。 如果已打开流实例的最大数目，或者打开此流所需的硬件资源不可用，则微型驱动程序将返回相应的错误状态。

**当微型驱动程序接收到 SRB\_OPEN\_STREAM 命令时，微型驱动程序应：**

1.  检查是否未超出流实例的最大数量，以及流索引值是否有效。

2.  检查请求的数据格式对于此流是否有效。

3.  设置流的格式。

4.  维护设备扩展中所有流扩展结构的数组，以便可以从任何流中取消 Irp。

5.  在流对象中指定指向流数据处理程序和控件处理程序的指针。

6.  如果设备将直接向传递到**ReceiveDataPacket**例程的数据缓冲区地址执行 dma，请在流对象中设置 dma 标志。 如果驱动程序访问使用逻辑寻址传入的数据缓冲区，还应在 stream 对象中设置 PIO 标志。

7.  如果流上提供了时钟支持，则通过流对象中的**HwClockObject**成员来指示这一点。

 

 






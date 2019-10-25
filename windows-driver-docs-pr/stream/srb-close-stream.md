---
title: SRB\_关闭\_流
description: SRB\_关闭\_流
ms.assetid: e118ddd7-fe0e-4834-9ae6-19eef0348b2c
keywords:
- SRB_CLOSE_STREAM 流媒体设备
topic_type:
- apiref
api_name:
- SRB_CLOSE_STREAM
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 697cab677d0554c5730047e8b165f3d7cc904643
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843305"
---
# <a name="srb_close_stream"></a>SRB\_关闭\_流


## <span id="ddk_srb_close_stream_ks"></span><span id="DDK_SRB_CLOSE_STREAM_KS"></span>


类驱动程序发送此请求以关闭流。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

微型驱动程序应将以下内容之一设置为 SRB 中的状态：

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>成功\_状态  
指示命令成功完成。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>状态\_未\_实现  
指示微型驱动程序不支持该函数。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>IO\_设备状态\_\_错误  
指示出现硬件故障。

### <a name="comments"></a>备注

类驱动程序在*pSrb*-&gt;**StreamObject**中提供了[**HW\_流\_对象**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_object)缓冲区， *pSrb*-&gt;**StreamObject**-&gt;**StreamNumber**设置为要关闭的流的数目。 *PSrb*指针指向[**HW\_STREAM\_请求\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_request_block)结构。 **StreamNumber**对应于[**HW\_\_流**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_descriptor)中的流的偏移量，微型驱动程序为响应[**SRB\_获取\_流\_INFO**](srb-get-stream-info.md)请求而提供此结构。

如果微型驱动程序成功关闭了流，则微型驱动程序将返回状态\_SUCCESS。 否则，它将返回相应的错误状态。

**当微型驱动程序接收到 SRB\_CLOSE\_STREAM 命令时，响应的微型驱动程序例程应：**

1.  释放流打开时微型驱动程序分配的所有资源。

2.  如果时钟用于流，则停止引用时钟。

3.  将流状态重置为 "停止"。

请注意，如果关联的用户模式应用程序发生故障，则在流式处理时，可以随意关闭流。 因此，你必须释放流的所有未完成的资源，完成流的所有挂起的 SRBs，然后将流重新进入静态状态。

 

 






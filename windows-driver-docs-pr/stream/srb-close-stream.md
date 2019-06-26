---
title: SRB\_CLOSE\_STREAM
description: SRB\_CLOSE\_STREAM
ms.assetid: e118ddd7-fe0e-4834-9ae6-19eef0348b2c
keywords:
- SRB_CLOSE_STREAM 流式处理媒体设备
topic_type:
- apiref
api_name:
- SRB_CLOSE_STREAM
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 993d6d26d733b49dc31e116d0653232b25d069fb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358382"
---
# <a name="srbclosestream"></a>SRB\_CLOSE\_STREAM


## <span id="ddk_srb_close_stream_ks"></span><span id="DDK_SRB_CLOSE_STREAM_KS"></span>


在类驱动程序将发送此请求关闭流。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

微型驱动程序应设置以下项之一为 SRB 中的状态：

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>状态\_成功  
指示命令成功完成。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>状态\_不\_实现  
指示该函数不受微型驱动程序。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>状态\_IO\_设备\_错误  
指示发生了硬件故障。

### <a name="comments"></a>备注

在类驱动程序提供了[ **HW\_流\_对象**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_stream_object)中的缓冲区*pSrb* - &gt; **StreamObject**，使用*pSrb*-&gt;**StreamObject**-&gt;**StreamNumber**设置为流的数量，以关闭。 *PSrb*指针指向[ **HW\_流\_请求\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_stream_request_block)结构。 **StreamNumber**对应于流中的偏移量[ **HW\_流\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_stream_descriptor)微型驱动程序提供响应的结构[ **SRB\_获取\_流\_信息**](srb-get-stream-info.md)请求。

如果微型驱动程序已成功关闭流，微型驱动程序将返回状态\_成功。 否则，它返回相应的错误状态。

**当 SRB\_关闭\_微型驱动程序收到流命令时，响应的微型驱动程序例程应：**

1.  释放由微型驱动程序在打开流时分配任何资源。

2.  停止如果时钟用于流引用时钟。

3.  流状态重置为 Stop。

请注意，可以随意关闭流时如果发生故障，关联的用户模式应用程序流式处理。 因此，必须释放所有未完成资源的流，填写所有挂起 Srb，为流，流放回到静止状态。

 

 






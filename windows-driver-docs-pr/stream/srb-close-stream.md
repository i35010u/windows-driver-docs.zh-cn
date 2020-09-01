---
title: SRB \_ 关闭 \_ 流
description: SRB \_ 关闭 \_ 流
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
ms.openlocfilehash: e6ca00b52f236ebe7c436ee46f57935d748437e2
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186097"
---
# <a name="srb_close_stream"></a>SRB \_ 关闭 \_ 流


## <span id="ddk_srb_close_stream_ks"></span><span id="DDK_SRB_CLOSE_STREAM_KS"></span>


类驱动程序发送此请求以关闭流。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

微型驱动程序应将以下内容之一设置为 SRB 中的状态：

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>状态 \_ 成功  
指示命令成功完成。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>状态 \_ 未 \_ 实现  
指示微型驱动程序不支持该函数。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>状态 \_ IO \_ 设备 \_ 错误  
指示出现硬件故障。

### <a name="comments"></a>注释

类驱动程序在*pSrb*StreamObject 中提供了[**HW \_ 流 \_ 对象**](/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_object)缓冲区 - &gt; **StreamObject**， *pSrb* - &gt; **StreamObject** - &gt; **StreamNumber**设置为要关闭的流的数目。 *PSrb*指针指向[**HW \_ 流 \_ 请求 \_ 块**](/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_request_block)结构。 **StreamNumber**对应于微型驱动程序提供的、响应[**SRB \_ 获取 \_ 流 \_ 信息**](srb-get-stream-info.md)请求的[**HW \_ 流 \_ 描述符**](/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_descriptor)结构内的流偏移量。

如果微型驱动程序成功关闭了流，则微型驱动程序返回状态 " \_ 成功"。 否则，它将返回相应的错误状态。

**当 \_ 微型驱动程序接收到 SRB CLOSE \_ STREAM 命令时，响应的微型驱动程序例程应：**

1.  释放流打开时微型驱动程序分配的所有资源。

2.  如果时钟用于流，则停止引用时钟。

3.  将流状态重置为 "停止"。

请注意，如果关联的用户模式应用程序发生故障，则在流式处理时，可以随意关闭流。 因此，你必须释放流的所有未完成的资源，完成流的所有挂起的 SRBs，然后将流重新进入静态状态。

 


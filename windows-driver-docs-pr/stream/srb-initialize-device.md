---
title: SRB \_ 初始化 \_ 设备
description: SRB \_ 初始化 \_ 设备
keywords:
- SRB_INITIALIZE_DEVICE 流媒体设备
topic_type:
- apiref
api_name:
- SRB_INITIALIZE_DEVICE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 491d07c92fca1da0c07f090bded6bdfd675b23df
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799283"
---
# <a name="srb_initialize_device"></a>SRB \_ 初始化 \_ 设备


## <span id="ddk_srb_initialize_device_ks"></span><span id="DDK_SRB_INITIALIZE_DEVICE_KS"></span>


类驱动程序在开始初始化微型驱动程序的硬件时会发送此请求。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

微型驱动程序应将以下内容之一设置为 SRB 中的状态：

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>状态 \_ 成功  
指示找到了主机适配器并且已成功确定配置信息。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>状态 \_ IO \_ 设备 \_ 错误  
指示找到了主机适配器，但获取配置信息时出错。 如果可能，应记录该错误。

<span id="STATUS_NO_SUCH_DEVICE"></span><span id="status_no_such_device"></span>状态 \_ 无 \_ 此类 \_ 设备  
指示提供的配置信息无效。

### <a name="comments"></a>注释

类驱动程序将指针传递到 \_ \_ *pSrb* - &gt; **CommandData.Config信息** 中的端口配置信息结构。 *PSrb* 指针指向 [**HW \_ 流 \_ 请求 \_ 块**](/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_request_block)结构。 类驱动程序会在 *pSrb* CommandData.Config信息中填写大部分字段 - &gt; **** ，以及从操作系统获取的有关设备的信息。 在大多数情况下，微型驱动程序只需在 **ConfigInfo** 的 **StreamDescriptorSize** 成员中填写其 [**HW \_ 流 \_ 描述符**](/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_descriptor)结构的大小。

 


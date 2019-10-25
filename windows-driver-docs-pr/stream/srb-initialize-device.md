---
title: SRB\_初始化\_设备
description: SRB\_初始化\_设备
ms.assetid: a4e35253-43d8-4d11-8a5b-72a9863f6677
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
ms.openlocfilehash: 2ea313ca253460e7843b20d8c21f624091d06185
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843296"
---
# <a name="srb_initialize_device"></a>SRB\_初始化\_设备


## <span id="ddk_srb_initialize_device_ks"></span><span id="DDK_SRB_INITIALIZE_DEVICE_KS"></span>


类驱动程序在开始初始化微型驱动程序的硬件时会发送此请求。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

微型驱动程序应将以下内容之一设置为 SRB 中的状态：

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>成功\_状态  
指示找到了主机适配器并且已成功确定配置信息。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>IO\_设备状态\_\_错误  
指示找到了主机适配器，但获取配置信息时出错。 如果可能，应记录该错误。

<span id="STATUS_NO_SUCH_DEVICE"></span><span id="status_no_such_device"></span>状态\_\_此类\_设备  
指示提供的配置信息无效。

### <a name="comments"></a>备注

类驱动程序将指针传递到*pSrb*-&gt;**CONFIGINFO**中的端口\_配置\_信息结构。 *PSrb*指针指向[**HW\_STREAM\_请求\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_request_block)结构。 类驱动程序会在*pSrb*-&gt;**CommandData. ConfigInfo**中填写大部分字段，其中包含从操作系统获取的有关设备的信息。 在大多数情况下，微型驱动程序只需在**ConfigInfo**的**StreamDescriptorSize**成员中填写其[ **\_HW\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_descriptor)结构的大小。

 

 






---
title: SRB \_ 关闭 \_ 设备 \_ 实例
description: SRB \_ 关闭 \_ 设备 \_ 实例
ms.assetid: 55a72f4f-45b3-427d-80b7-620aac870a8a
keywords:
- SRB_CLOSE_DEVICE_INSTANCE 流媒体设备
topic_type:
- apiref
api_name:
- SRB_CLOSE_DEVICE_INSTANCE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 684590bb980657e19ff34ef8f13a4870a0405dbf
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190359"
---
# <a name="srb_close_device_instance"></a>SRB \_ 关闭 \_ 设备 \_ 实例


## <span id="ddk_srb_close_device_instance_ks"></span><span id="DDK_SRB_CLOSE_DEVICE_INSTANCE_KS"></span>


类驱动程序发送此请求以关闭以前打开的适配器的实例。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

微型驱动程序应将以下内容之一设置为 SRB 中的状态：

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>状态 \_ 成功  
指示命令成功完成。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>状态 \_ 未 \_ 实现  
指示微型驱动程序不支持该函数。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>状态 \_ IO \_ 设备 \_ 错误  
指示出现硬件故障。

### <a name="comments"></a>说明

大多数适配器不支持多个实例，因此在这种情况下， [**HW \_ 初始化 \_ 数据**](/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_initialization_data)结构中的**FilterInstanceExtensionSize**字段应设置为零，且永远不会收到此命令。

 


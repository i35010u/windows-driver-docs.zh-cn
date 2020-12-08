---
title: SRB 取消 \_ 初始化 \_ 设备
description: SRB 取消 \_ 初始化 \_ 设备
keywords:
- SRB_UNINITIALIZE_DEVICE 流媒体设备
topic_type:
- apiref
api_name:
- SRB_UNINITIALIZE_DEVICE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 198ffc538a14be3612057d50e8d7371aea10406d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824881"
---
# <a name="srb_uninitialize_device"></a>SRB 取消 \_ 初始化 \_ 设备


## <span id="ddk_srb_uninitialize_device_ks"></span><span id="DDK_SRB_UNINITIALIZE_DEVICE_KS"></span>


类驱动程序发送此请求，指示微型驱动程序禁用其自身。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

微型驱动程序应将以下内容之一设置为 SRB 中的状态：

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>状态 \_ 成功  
指示命令成功完成。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>状态 \_ 未 \_ 实现  
指示微型驱动程序不支持该函数。

<span id="STATUS_ADAPTER_HARDWARE_ERROR"></span><span id="status_adapter_hardware_error"></span>状态 \_ 适配器 \_ 硬件 \_ 错误  
指示此时不能取消初始化微型驱动程序。

### <a name="comments"></a>注释

微型驱动程序应解除分配其所分配的任何资源，并禁用设备的中断。  (类驱动程序会自动释放其代表微型驱动程序分配的所有资源 ) 

 

 






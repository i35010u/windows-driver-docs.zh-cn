---
title: SRB\_UNINITIALIZE\_DEVICE
description: SRB\_UNINITIALIZE\_DEVICE
ms.assetid: 2cacb65a-8df3-4649-bc44-1bc7a5c598b9
keywords:
- SRB_UNINITIALIZE_DEVICE 流式处理媒体设备
topic_type:
- apiref
api_name:
- SRB_UNINITIALIZE_DEVICE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ea0c1fc7e211d45e89a3eac9569860e1f06a44f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392105"
---
# <a name="srbuninitializedevice"></a>SRB\_UNINITIALIZE\_DEVICE


## <span id="ddk_srb_uninitialize_device_ks"></span><span id="DDK_SRB_UNINITIALIZE_DEVICE_KS"></span>


类驱动程序将发送此请求发出信号微型驱动程序可以禁用它自己。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

微型驱动程序应设置以下项之一为 SRB 中的状态：

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>状态\_成功  
指示命令成功完成。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>状态\_不\_实现  
指示该函数不受微型驱动程序。

<span id="STATUS_ADAPTER_HARDWARE_ERROR"></span><span id="status_adapter_hardware_error"></span>状态\_适配器\_硬件\_错误  
指示在此时间不能取消初始化微型驱动程序。

### <a name="comments"></a>备注

微型驱动程序应释放它分配的任何资源，并禁用设备的中断。 （在类驱动程序会自动释放它代表微型驱动程序分配的任何资源。）

 

 






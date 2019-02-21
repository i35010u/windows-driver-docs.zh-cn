---
title: SRB\_开放\_设备\_实例
description: SRB\_开放\_设备\_实例
ms.assetid: 71f57abd-7875-4c7a-bbb3-c5c45c9a83ab
keywords:
- SRB_OPEN_DEVICE_INSTANCE 流式处理媒体设备
topic_type:
- apiref
api_name:
- SRB_OPEN_DEVICE_INSTANCE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba54fe8fde7331c633373de02acc54b41aa6af6d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533690"
---
# <a name="srbopendeviceinstance"></a>SRB\_开放\_设备\_实例


## <span id="ddk_srb_open_device_instance_ks"></span><span id="DDK_SRB_OPEN_DEVICE_INSTANCE_KS"></span>


在类驱动程序将发送此请求打开适配器的实例。

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

如果微型驱动程序支持的设备的多个实例，每次打开新的适配器实例的类驱动程序发送此命令。 作为示例，请考虑可以分配的 DSP 解码器*n*的指定流的实例数。 **HwInstanceExtension** SRB 中的字段应然后设置为微型驱动程序的每个实例的工作区的类驱动程序。

大多数适配器不支持多个实例，因此，在这种情况下**FilterInstanceExtensionSize**字段中**HW\_初始化\_数据**结构应设置为零和应永远不会收到此命令。

## <a name="see-also"></a>另请参阅


[**SRB\_CLOSE\_DEVICE\_INSTANCE**](srb-close-device-instance.md)

 

 







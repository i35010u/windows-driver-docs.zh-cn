---
title: SRB \_ 打开 \_ 设备 \_ 实例
description: SRB \_ 打开 \_ 设备 \_ 实例
keywords:
- SRB_OPEN_DEVICE_INSTANCE 流媒体设备
topic_type:
- apiref
api_name:
- SRB_OPEN_DEVICE_INSTANCE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 666fd7e7c589cb4f7e50642a4d994da6a64af425
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840493"
---
# <a name="srb_open_device_instance"></a>SRB \_ 打开 \_ 设备 \_ 实例


## <span id="ddk_srb_open_device_instance_ks"></span><span id="DDK_SRB_OPEN_DEVICE_INSTANCE_KS"></span>


类驱动程序发送此请求以打开适配器的实例。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

微型驱动程序应将以下内容之一设置为 SRB 中的状态：

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>状态 \_ 成功  
指示命令成功完成。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>状态 \_ 未 \_ 实现  
指示微型驱动程序不支持该函数。

<span id="STATUS_TOO_MANY_NODES"></span><span id="status_too_many_nodes"></span>状态 \_ 太 \_ 多 \_ 节点  
指示没有足够的资源来打开此流。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>状态 \_ IO \_ 设备 \_ 错误  
指示出现硬件故障。

### <a name="comments"></a>注释

如果微型驱动程序支持设备的多个实例，则每次打开新的适配器实例时，该类驱动程序都会发送此命令。 例如，假设有一个 DSP 解码器，该解码器可分配指定的流的 *n* 个实例。 然后，应将 SRB 中的 **HwInstanceExtension** 字段设置为类驱动程序的微型驱动程序每实例工作区。

大多数适配器不支持多个实例，因此在这种情况下， **HW \_ 初始化 \_ 数据** 结构中的 **FilterInstanceExtensionSize** 字段应设置为零，且永远不会收到此命令。

## <a name="see-also"></a>请参阅


[**SRB \_ 关闭 \_ 设备 \_ 实例**](srb-close-device-instance.md)

 

 







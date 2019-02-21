---
title: 实现 USB 空闲请求 IRP 回调例程
description: 实现 USB 空闲请求 IRP 回调例程
ms.assetid: B3F843CD-E9D8-4ABD-9BC9-08C5AB7CDB98
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c6670eb750287ea1937b883aca2554066302734
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534474"
---
# <a name="implementing-a-usb-idle-request-irp-callback-routine"></a>实现 USB 空闲请求 IRP 回调例程


当[ *MiniportIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464092)调用时，USB 微型端口驱动程序调用[ **IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336)发出 I/O 请求数据包 (IRP)USB 空闲请求 ([**IOCTL\_内部\_USB\_提交\_空闲\_通知**](https://msdn.microsoft.com/library/windows/hardware/ff537270)) 到基础 USB 总线驱动程序。 微型端口驱动程序将发出此 IRP 的网络适配器处于空闲状态，且必须挂起通知 USB 总线驱动程序。

USB 微型端口驱动程序必须提供 USB 空闲请求 IRP IRP 的回调例程。 它确定可以挂起和转换为低功耗状态的网络适配器时，USB 总线驱动程序将调用此例程。

**请注意**  后 USB 总线驱动程序处理 USB 空闲请求 IRP，调用回调例程的调用上下文中以同步方式[ **IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336)或后，将异步[ *MiniportIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464092)返回。

 

回调例程仅有调用[ **NdisMIdleNotificationConfirm** ](https://msdn.microsoft.com/library/windows/hardware/hh451492)为了通知它可以继续低功耗状态转换的网络适配器的 NDIS。 当驱动程序调用**NdisMIdleNotificationConfirm**，它还必须指定网络适配器可以转换到的最低设备电源状态。

对调用的上下文中[ **NdisMIdleNotificationConfirm**](https://msdn.microsoft.com/library/windows/hardware/hh451492)，NDIS 执行转换到低功耗状态的网络适配器所需的步骤。 有关详细信息，请参阅[处理 NDIS 选择性挂起空闲通知](handling-the-ndis-selective-suspend-idle-notification.md)。

下面是 USB 空闲请求 IRP 的回调例程的示例。

```C++
//
// MiniportUsbIdleRequestCallback()
//
// This is the USB selective suspend idle notification.  All that is 
// needed is to inform NDIS that the USB stack is ready to go to a 
// low-power state.  Be aware that USB devices will always be requested
// to transition to a power state of NdisDeviceStateD2.
//
VOID MiniportUsbIdleRequestCallback(PVOID AdapterContext)
{
    NdisMIdleNotificationConfirm(
        AdapterContext->MiniportAdapterHandle,
        NdisDeviceStateD2
        );

    return;
}
```

有关 USB 空闲请求回调例程的详细信息，请参阅 USB 空闲请求 IRP 回调例程。

 

 






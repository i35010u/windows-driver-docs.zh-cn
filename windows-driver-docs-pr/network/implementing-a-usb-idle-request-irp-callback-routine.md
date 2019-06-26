---
title: 实现 USB 空闲请求 IRP 回调例程
description: 实现 USB 空闲请求 IRP 回调例程
ms.assetid: B3F843CD-E9D8-4ABD-9BC9-08C5AB7CDB98
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be55e45fb984ac53b29cec8048bd694172e45394
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382670"
---
# <a name="implementing-a-usb-idle-request-irp-callback-routine"></a>实现 USB 空闲请求 IRP 回调例程


当[ *MiniportIdleNotification* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_idle_notification)调用时，USB 微型端口驱动程序调用[ **IoCallDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)发出 I/O 请求数据包 (IRP)USB 空闲请求 ([**IOCTL\_内部\_USB\_提交\_空闲\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification)) 到基础 USB 总线驱动程序。 微型端口驱动程序将发出此 IRP 的网络适配器处于空闲状态，且必须挂起通知 USB 总线驱动程序。

USB 微型端口驱动程序必须提供 USB 空闲请求 IRP IRP 的回调例程。 它确定可以挂起和转换为低功耗状态的网络适配器时，USB 总线驱动程序将调用此例程。

**请注意**  后 USB 总线驱动程序处理 USB 空闲请求 IRP，调用回调例程的调用上下文中以同步方式[ **IoCallDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)或后，将异步[ *MiniportIdleNotification* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_idle_notification)返回。

 

回调例程仅有调用[ **NdisMIdleNotificationConfirm** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismidlenotificationconfirm)为了通知它可以继续低功耗状态转换的网络适配器的 NDIS。 当驱动程序调用**NdisMIdleNotificationConfirm**，它还必须指定网络适配器可以转换到的最低设备电源状态。

对调用的上下文中[ **NdisMIdleNotificationConfirm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismidlenotificationconfirm)，NDIS 执行转换到低功耗状态的网络适配器所需的步骤。 有关详细信息，请参阅[处理 NDIS 选择性挂起空闲通知](handling-the-ndis-selective-suspend-idle-notification.md)。

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

 

 






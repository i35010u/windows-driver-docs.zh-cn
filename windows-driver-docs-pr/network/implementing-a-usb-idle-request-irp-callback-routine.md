---
title: 实现 USB 空闲请求 IRP 回调例程
description: 实现 USB 空闲请求 IRP 回调例程
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 186641989ec2a4ba804316c83f7a4de23b14a673
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821317"
---
# <a name="implementing-a-usb-idle-request-irp-callback-routine"></a>实现 USB 空闲请求 IRP 回调例程


调用 [*MiniportIdleNotification*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification) 时，usb 微型端口驱动程序会调用 [**IOCALLDRIVER**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) ，为 usb 空闲请求发出 I/O 请求数据包 (IRP) ， ([**IOCTL \_ 内部 \_ usb \_ \_ \_**](/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification) 向底层 usb 总线驱动程序提供) 。 微型端口驱动程序会发出此 IRP，通知 USB 总线驱动程序网络适配器处于空闲状态，必须挂起。

USB 微型端口驱动程序必须为 USB 空闲请求 IRP 提供 IRP 回调例程。 USB 总线驱动程序在确定网络适配器可以挂起并转换为低功耗状态时调用此例程。

**注意**  USB 总线驱动程序处理 USB idle 请求 IRP 后，它会在调用 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) 的上下文中以同步方式调用回调例程，或在 [*MiniportIdleNotification*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification) 返回后异步调用。

 

回调例程只需要调用 [**NdisMIdleNotificationConfirm**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationconfirm) ，以便通知 NDIS 它可以继续进行网络适配器的低功耗状态转换。 当驱动程序调用 **NdisMIdleNotificationConfirm** 时，它还必须指定网络适配器可以转换到的最小设备电源状态。

在对 [**NdisMIdleNotificationConfirm**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationconfirm)的调用上下文中，NDIS 执行将网络适配器转换为低功耗状态所需的步骤。 有关详细信息，请参阅 [处理 NDIS 选择性挂起空闲通知](handling-the-ndis-selective-suspend-idle-notification.md)。

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

 


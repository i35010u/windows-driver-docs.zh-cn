---
title: 实现 USB 空闲请求 IRP 回调例程
description: 实现 USB 空闲请求 IRP 回调例程
ms.assetid: B3F843CD-E9D8-4ABD-9BC9-08C5AB7CDB98
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a3e4575f069e878f9b905ce9d6725c44a87db9d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843437"
---
# <a name="implementing-a-usb-idle-request-irp-callback-routine"></a>实现 USB 空闲请求 IRP 回调例程


调用[*MiniportIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification)时，usb 微型端口驱动程序会调用[**IOCALLDRIVER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) ，为 Usb 空闲请求（[**IOCTL\_内部\_usb\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification)向基础 USB 总线驱动程序提交\_空闲\_通知）发出 i/o 请求数据包（IRP）。 微型端口驱动程序会发出此 IRP，通知 USB 总线驱动程序网络适配器处于空闲状态，必须挂起。

USB 微型端口驱动程序必须为 USB 空闲请求 IRP 提供 IRP 回调例程。 USB 总线驱动程序在确定网络适配器可以挂起并转换为低功耗状态时调用此例程。

**注意**  在 usb 总线驱动程序处理 usb IDLE 请求 IRP 后，它会在调用[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)或在[*MiniportIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification)返回后异步调用回调例程。

 

回调例程只需要调用[**NdisMIdleNotificationConfirm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationconfirm) ，以便通知 NDIS 它可以继续进行网络适配器的低功耗状态转换。 当驱动程序调用**NdisMIdleNotificationConfirm**时，它还必须指定网络适配器可以转换到的最小设备电源状态。

在对[**NdisMIdleNotificationConfirm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationconfirm)的调用上下文中，NDIS 执行将网络适配器转换为低功耗状态所需的步骤。 有关详细信息，请参阅[处理 NDIS 选择性挂起空闲通知](handling-the-ndis-selective-suspend-idle-notification.md)。

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

 

 






---
title: 实现 MiniportCancelIdleNotification 处理程序函数
description: 实现 MiniportCancelIdleNotification 处理程序函数
ms.assetid: 51C25573-5723-44F9-B498-EBEF6756F3B0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c087647e463e6179293e529d73e97218482217ad
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206461"
---
# <a name="implementing-a-miniportcancelidlenotification-handler-function"></a>实现 MiniportCancelIdleNotification 处理程序函数


NDIS 调用微型端口驱动程序的 [*MiniportCancelIdleNotification*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_idle_notification) 处理程序函数以便取消空闲通知进程，并将网络适配器转换为完全电源状态。 调用此函数时，微型端口驱动程序必须执行以下步骤：

1.  微型端口驱动程序必须取消任何特定于总线的 Irp，该 Irp 先前可能已针对空闲通知发出。

2.  微型端口驱动程序调用 [**NdisMIdleNotificationComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationcomplete)。 此调用会通知 NDIS 空闲通知已完成。 然后，NDIS 会通过将网络适配器转换为完全电源状态来复杂选择性挂起操作。

例如，当调用 [*MiniportCancelIdleNotification*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_idle_notification) 时，usb 微型端口驱动程序调用 [**IOCANCELIRP**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocancelirp) 来取消 usb 空闲请求的 I/O 请求数据包 (IRP)  ([**IOCTL \_ 内部 \_ usb \_ 提交 \_ 空闲 \_ 通知**](/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification)) 。 USB 微型端口驱动程序以前在其 [*MiniportIdleNotification*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification) 处理程序函数中颁发了此 IRP。 一旦 USB 总线驱动程序取消了 IRP，就会调用 IRP 的完成例程。 当 USB 总线驱动程序调用完成例程时，它将确认 IRP 已取消，并且设备可以恢复到全电源状态。 在完成例程的上下文中，微型端口驱动程序调用 [**NdisMIdleNotificationComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationcomplete)。

**注意**   USB 总线驱动程序可以在对[**IoCancelIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocancelirp)的调用的上下文中以同步方式调用完成例程，也可以在[*MiniportCancelIdleNotification*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_idle_notification)返回后异步调用。

 

下面是一个用于 USB 微型端口驱动程序的 [*MiniportCancelIdleNotification*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_idle_notification) 处理程序函数的示例。 此示例显示了取消 USB 空闲请求 IRP 所涉及的步骤。

```C++
//
// MiniportCancelIdleNotification()
//
// This routine is called if NDIS has to cancel an idle notification.
// All that is needed is to cancel the selective suspend IRP.
//
VOID MiniportCancelIdleNotification(
    _In_ NDIS_HANDLE MiniportAdapterContext
    )
{
    IoCancelIrp(Adapter->UsbSsIrp);
}
```

有关为 USB 空闲请求 IRP 实现完成例程的指导，请参阅 [实现 Usb 空闲请求 Irp 完成例程](implementing-a-usb-idle-request-irp-completion-routine.md)。

 


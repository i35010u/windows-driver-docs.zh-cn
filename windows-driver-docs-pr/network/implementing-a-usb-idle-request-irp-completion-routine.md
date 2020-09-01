---
title: 实现 USB 空闲请求 IRP 完成例程
description: 实现 USB 空闲请求 IRP 完成例程
ms.assetid: C9435A1D-031B-4F67-B968-66534C48A9BC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 05c54a7a266e607bfb00b4614e47d6f0d0ea8b54
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206437"
---
# <a name="implementing-a-usb-idle-request-irp-completion-routine"></a>实现 USB 空闲请求 IRP 完成例程


调用 [*MiniportIdleNotification*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification) 时，usb 微型端口驱动程序会调用 [**IOCALLDRIVER**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) ，为 usb 空闲请求发出 I/O 请求数据包 (IRP) ， ([**IOCTL \_ 内部 \_ usb \_ \_ \_ **](/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification) 向底层 usb 总线驱动程序提供) 。 微型端口驱动程序会发出此 IRP，通知 USB 总线驱动程序网络适配器处于空闲状态，必须挂起。

USB 微型端口驱动程序还必须调用 [**IoSetCompletionRoutineEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutineex) ，以便为 USB 空闲请求 IRP 注册完成例程。 USB 总线驱动程序在由 USB 微型端口驱动程序取消后，在完成 IRP 后调用完成例程。 当 NDIS 取消空闲通知时，USB 微型端口驱动程序会取消 IRP，方法是调用 [*MiniportCancelIdleNotification*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_idle_notification)。

完成例程只需要调用 [**NdisMIdleNotificationComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationconfirm) ，以便通知 NDIS 它可以继续通过网络适配器的完整电源状态转换。

**注意**   \_ \_ \_ 如果 USB 微型端口驱动程序将在另一个空闲通知中从 NDIS 重新使用 IRP 资源，则完成例程必须返回状态更多所需的处理。

 

下面是 USB 空闲请求 IRP 的完成例程的示例。

```C++
//
// MiniportUsbIdleRequestCompletion()
//
// This is the IO_COMPLETION_ROUTINE for the selective suspend IOCTL.
// All that is needed is to inform NDIS that the IdleNotification
// operation is complete.
//
VOID MiniportUsbIdleRequestCompletion(PVOID AdapterContext)
{
    NdisMIdleNotificationComplete(Adapter->MiniportAdapterHandle);

    // We will be reusing the IRP later, so do not let the IO manager delete it.
    return STATUS_MORE_PROCESSING_REQUIRED;
}
```

有关 USB 空闲请求回调例程的详细信息，请参阅 USB 空闲请求 IRP 完成例程。

 


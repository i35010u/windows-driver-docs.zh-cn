---
title: 实现 USB 空闲请求 IRP 完成例程
description: 实现 USB 空闲请求 IRP 完成例程
ms.assetid: C9435A1D-031B-4F67-B968-66534C48A9BC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2bfa2fa81066ae977de62ce30662dca643c2aa47
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382680"
---
# <a name="implementing-a-usb-idle-request-irp-completion-routine"></a>实现 USB 空闲请求 IRP 完成例程


当[ *MiniportIdleNotification* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_idle_notification)调用时，USB 微型端口驱动程序调用[ **IoCallDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)发出 I/O 请求数据包 (IRP)USB 空闲请求 ([**IOCTL\_内部\_USB\_提交\_空闲\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification)) 到基础 USB 总线驱动程序。 微型端口驱动程序将发出此 IRP 的网络适配器处于空闲状态，且必须挂起通知 USB 总线驱动程序。

USB 微型端口驱动程序还必须调用[ **IoSetCompletionRoutineEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutineex)才能注册 USB 空闲请求 IRP 完成例程。 USB 总线驱动程序在其完成后 IRP，取消通过 USB 微型端口驱动程序后调用完成例程。 USB 微型端口驱动程序在 NDIS 取消通过调用发出的空闲通知时取消 IRP [ *MiniportCancelIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_cancel_idle_notification)。

完成例程仅有调用[ **NdisMIdleNotificationComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismidlenotificationconfirm)为了通知它可以继续全功率状态转换的网络适配器的 NDIS。

**请注意**  完成例程必须返回状态\_详细\_处理\_所需如果 USB 微型端口驱动程序将 IRP 资源可在重新使用 NDIS 从另一个空闲通知。

 

下面是 USB 空闲请求 IRP 完成例程的示例。

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

 

 






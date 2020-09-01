---
title: 实现 MiniportIdleNotification 处理程序函数
description: 实现 MiniportIdleNotification 处理程序函数
ms.assetid: F2F8C98F-D8B3-49A6-819D-BC0EC936F41E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0744d96add191680a96d535ae129942fe33ebdb9
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206455"
---
# <a name="implementing-a-miniportidlenotification-handler-function"></a>实现 MiniportIdleNotification 处理程序函数


NDIS 调用微型端口驱动程序的 [*MiniportIdleNotification*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification) 处理程序函数以便有选择地挂起网络适配器。 当 NDIS 将适配器转换为低功耗状态时，适配器将挂起。

如果仍在使用网络适配器，微型端口驱动程序可以拒绝空闲通知。 驱动程序通过 \_ \_ 从 [*MiniportIdleNotification*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification) 处理程序函数返回 NDIS 状态繁忙来实现此功能。

**注意**   如果[*MiniportIdleNotification*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification)处理程序函数的*ForceIdle*参数设置为**TRUE**，则微型端口驱动程序无法否决空闲通知。

 

如果微型端口驱动程序不会拒绝空闲通知，则可能必须将 (Irp) 的特定于总线的 i/o 请求数据包发送到基础总线驱动程序。 这些 Irp 通知总线驱动程序适配器的空闲状态，并请求确认适配器可以转换为低功耗状态。

例如，当调用 [*MiniportIdleNotification*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification) 时，usb 微型端口驱动程序会为 usb 空闲请求准备一个 i/o 请求数据包 (IRP)  ([**IOCTL \_ 内部 \_ usb \_ 提交 \_ 空闲 \_ 通知**](/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification)) 。 当微型端口驱动程序准备 IRP 时，它必须指定回调函数。 驱动程序还必须调用 [**IoSetCompletionRoutine**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine) 或 [**IOSETCOMPLETIONROUTINEEX**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutineex) 来指定 IRP 的完成例程。 然后，微型端口驱动程序调用 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) 将 IRP 颁发给 USB 总线驱动程序。

**注意**   USB 总线驱动程序不会立即完成 IRP。 IRP 通过低功耗转换保持处于挂起状态。 只有微型端口驱动程序或硬件事件（例如从 USB 集线器中删除网络适配器）取消时，总线驱动程序才会完成 IRP。

 

下面是一个用于 USB 微型端口驱动程序的 [*MiniportIdleNotification*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification) 处理程序函数的示例。 此示例显示了向基础 USB 驱动程序发出 USB 空闲请求 IRP 所涉及的步骤。 此示例还演示了如何为 IRP 重用以前在 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)中分配的 IRP 资源。

```C++
//
// MiniportIdleNotification()
//
// This routine is invoked by NDIS when it has detected that the miniport
// is idle.  The miniport must prepare to issue its selective suspend IRP
// to the USB stack.  The driver can return NDIS_STATUS_BUSY if it is
// unwilling to become idle at this moment; NDIS will then retry later.
// Otherwise, the miniport should return NDIS_STATUS_PENDING.
//
NDIS_STATUS MiniportIdleNotification(
    _In_ NDIS_HANDLE MiniportAdapterContext,
    _In_ BOOLEAN ForceIdle
    )
{
    PIO_STACK_LOCATION IoSp;

    IoReuseIrp(Adapter->UsbSsIrp, STATUS_NOT_SUPPORTED);

    IoSp = IoGetNextIrpStackLocation(Adapter->UsbSsIrp);
    IoSp->MajorFunction = IRP_MJ_INTERNAL_DEVICE_CONTROL;
    IoSp->Parameters.DeviceIoControl.IoControlCode 
            = IOCTL_INTERNAL_USB_SUBMIT_IDLE_NOTIFICATION;
    IoSp->Parameters.DeviceIoControl.InputBufferLength 
            = sizeof(Adapter->UsbSsCallback);
    IoSp->Parameters.DeviceIoControl.Type3InputBuffer 
            = Adapter->UsbSsCallback;

    IoSetCompletionRoutine(
            Adapter->UsbSsIrp,
            MiniportUsbIdleRequestCompletion,
            Adapter,
            TRUE,
            TRUE,
            TRUE);

    NtStatus = IoCallDriver(Adapter->Fdo, Adapter->UsbSsIrp);
    if (!NT_SUCCESS(NtStatus))
    {
       return NDIS_STATUS_FAILURE;
    }

    return NDIS_STATUS_PENDING;
}
```

有关为 USB idle 请求 IRP 实现回调例程的指南，请参阅 [实现 Usb 空闲请求 Irp 回调例程](implementing-a-usb-idle-request-irp-callback-routine.md)。

 


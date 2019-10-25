---
title: 实现 MiniportIdleNotification 处理程序函数
description: 实现 MiniportIdleNotification 处理程序函数
ms.assetid: F2F8C98F-D8B3-49A6-819D-BC0EC936F41E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe85f744696038eba9f94d782445f2b3f9fce084
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843440"
---
# <a name="implementing-a-miniportidlenotification-handler-function"></a>实现 MiniportIdleNotification 处理程序函数


NDIS 调用微型端口驱动程序的[*MiniportIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification)处理程序函数以便有选择地挂起网络适配器。 当 NDIS 将适配器转换为低功耗状态时，适配器将挂起。

如果仍在使用网络适配器，微型端口驱动程序可以拒绝空闲通知。 驱动程序通过从[*MiniportIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification)处理程序函数返回 NDIS\_状态\_繁忙来实现此功能。

**请注意**  如果[*MiniportIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification)处理程序函数的*ForceIdle*参数设置为**TRUE**，则微型端口驱动程序无法否决空闲通知。

 

如果微型端口驱动程序不拒绝空闲通知，则可能必须将特定于总线的 i/o 请求数据包（Irp）颁发给基础总线驱动程序。 这些 Irp 通知总线驱动程序适配器的空闲状态，并请求确认适配器可以转换为低功耗状态。

例如，当调用[*MiniportIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification)时，usb 微型端口驱动程序会为 usb 空闲请求准备 i/o 请求数据包（IRP）（[**IOCTL\_内部\_usb\_提交\_空闲\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification)）。 当微型端口驱动程序准备 IRP 时，它必须指定回调函数。 驱动程序还必须调用[**IoSetCompletionRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)或[**IOSETCOMPLETIONROUTINEEX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutineex)来指定 IRP 的完成例程。 然后，微型端口驱动程序调用[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)将 IRP 颁发给 USB 总线驱动程序。

**请注意**  USB 总线驱动程序不会立即完成 IRP。 IRP 通过低功耗转换保持处于挂起状态。 只有微型端口驱动程序或硬件事件（例如从 USB 集线器中删除网络适配器）取消时，总线驱动程序才会完成 IRP。

 

下面是一个用于 USB 微型端口驱动程序的[*MiniportIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification)处理程序函数的示例。 此示例显示了向基础 USB 驱动程序发出 USB 空闲请求 IRP 所涉及的步骤。 此示例还演示了如何为 IRP 重用以前在[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)中分配的 IRP 资源。

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

有关为 USB idle 请求 IRP 实现回调例程的指南，请参阅[实现 Usb 空闲请求 Irp 回调例程](implementing-a-usb-idle-request-irp-callback-routine.md)。

 

 






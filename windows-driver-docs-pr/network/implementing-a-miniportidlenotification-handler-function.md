---
title: 实现 MiniportIdleNotification 处理程序函数
description: 实现 MiniportIdleNotification 处理程序函数
ms.assetid: F2F8C98F-D8B3-49A6-819D-BC0EC936F41E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d3fb7e273094f3f7c6d89834c52d30ebe58796d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383647"
---
# <a name="implementing-a-miniportidlenotification-handler-function"></a>实现 MiniportIdleNotification 处理程序函数


NDIS 调用微型端口驱动程序[ *MiniportIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464092)处理程序函数，从而有选择地挂起的网络适配器。 当 NDIS 转换到低功耗状态适配器挂起适配器。

如果仍在使用的网络适配器来微型端口驱动程序可以禁止空闲通知。 该驱动程序执行此通过返回 NDIS\_状态\_从忙[ *MiniportIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464092)处理程序函数。

**请注意**  微型端口驱动程序无能空闲通知如果*ForceIdle*参数[ *MiniportIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464092)处理程序函数设置为 **，则返回 TRUE**。

 

如果微型端口驱动程序不能阻止空闲通知，它可能需要向基础总线驱动程序发出特定于总线的 I/O 请求数据包 (Irp)。 这些 Irp 通知有关适配器的空闲状态，适配器可以切换为低功耗状态的请求确认总线驱动程序。

例如，当[ *MiniportIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464092)调用时，USB 微型端口驱动程序准备的 I/O 请求数据包 (IRP) USB 空闲请求 ([**IOCTL\_内部\_USB\_提交\_空闲\_通知**](https://msdn.microsoft.com/library/windows/hardware/ff537270))。 当微型端口驱动程序准备 IRP 时，它必须指定一个回调函数。 该驱动程序还必须调用任一[ **IoSetCompletionRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff549679)或[ **IoSetCompletionRoutineEx** ](https://msdn.microsoft.com/library/windows/hardware/ff549686)指定完成例程有关 IRP。 然后调用微型端口驱动程序[ **IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336)将 IRP 发送到 USB 总线驱动程序。

**请注意**  USB 总线驱动程序不会立即完成 IRP。 IRP 处于挂起状态通过低电源转变。 总线驱动程序完成 IRP，仅当它被取消的微型端口驱动程序或硬件事件发生，例如从 USB 集线器的网络适配器被意外删除时。

 

以下是一种[ *MiniportIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464092) USB 微型端口驱动程序的处理程序函数。 此示例演示了对基础 USB 驱动程序发出 USB 空闲请求 IRP 的步骤。 此示例还演示如何中以前分配的 IRP 资源[ *MiniportInitializeEx*](https://msdn.microsoft.com/library/windows/hardware/ff559389)，可以重复使用的 IRP。

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

有关实现 USB 空闲请求 IRP 的回调例程的指南，请参阅[实现一个 USB 空闲请求 IRP 的回调例程](implementing-a-usb-idle-request-irp-callback-routine.md)。

 

 






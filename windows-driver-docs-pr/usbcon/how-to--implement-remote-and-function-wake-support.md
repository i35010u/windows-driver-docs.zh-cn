---
description: 本主题概述了适用于通用串行总线的函数挂起和函数远程唤醒功能 (USB) 3.0 多功能设备 (复合设备) 。
title: 如何在复合驱动程序中实现函数挂起
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a94975c4d8e051dbfd98b800422ebea823e0ac1c
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90010317"
---
# <a name="how-to-implement-function-suspend-in-a-composite-driver"></a>如何在复合驱动程序中实现函数挂起


本主题概述了适用于通用串行总线的函数挂起和函数远程唤醒功能 (USB) 3.0 多功能设备 (复合设备) 。 在本主题中，你将了解如何在控制复合设备的驱动程序中实现这些功能。 本主题适用于替换 Usbccgp.sys 的复合驱动程序。

通用串行总线 (USB) 3.0 规范定义了一个名为 " *函数挂起*" 的新功能。 此功能使复合设备的单个功能能够进入低功耗状态，这与其他功能无关。 考虑为键盘定义函数的复合设备和用于鼠标的另一个函数。 用户使键盘功能处于工作状态，但不会在一段时间内移动鼠标。 鼠标的客户端驱动程序可以检测函数的空闲状态，并在键盘功能处于工作状态时将该函数发送到挂起状态。

当所有单个函数都处于挂起状态时，整个复合设备将转换为挂起状态。 但是，无论设备内的任何功能的电源状态如何，整个设备都可以过渡到 "挂起" 状态。 如果特定的功能和整个设备进入挂起状态，则在设备处于挂起状态时将保留该功能的挂起状态，并且在整个设备的挂起进入和退出过程中保留。

类似于 USB 2.0 设备的远程唤醒功能 (参阅) [远程唤醒 Usb 设备](remote-wakeup-of-usb-devices.md) ，usb 3.0 复合设备中的单个功能可以从低功耗状态唤醒，而不会影响其他功能的电源状态。 此功能称为 " *函数远程唤醒*"。 此功能由主机显式启用，方法是发送一个协议请求，用于设置设备固件中的远程唤醒位。 此过程称为 *远程唤醒功能的武装*。 有关远程唤醒相关位的信息，请参阅官方 USB 规范中的图9-6。

如果某个函数用于远程唤醒，则该函数在处于挂起状态时 () 会保留足够的能力，以便在物理设备上发生用户事件时生成唤醒的 *恢复信号* 。 由于该恢复信号的原因，客户端驱动程序可以退出相关函数的挂起状态。 在复合设备中鼠标函数的示例中，当用户摆动处于空闲状态的鼠标时，鼠标函数会将恢复信号发送到主机。 在主机上，USB 驱动程序堆栈检测唤醒的函数，并将通知传播到相应函数的客户端驱动程序。 然后，客户端驱动程序可以唤醒函数并进入工作状态。

对于客户端驱动程序，用于将函数发送到挂起状态并唤醒函数的步骤类似于将整个设备发送到挂起状态的单功能设备驱动程序。 以下过程总结了这些步骤。

1.  在关联的函数处于空闲状态时进行检测。
2.   (IRP) 发送空闲 i/o 请求包。
3.  通过向 (IRP) 发送等待唤醒 i/o 请求数据包，将请求提交到 arm 用于远程唤醒的函数。
4.  通过向 (**D2**或**D3**) 发送**Dx**电源 irp，将该函数转换为低功率状态。

有关上述步骤的详细信息，请参阅 [USB 选择性挂起](usb-selective-suspend.md)中的 "发送 Usb 空闲请求 IRP"。
复合驱动程序为复合设备中的每个函数创建 (PDO) 的物理设备对象，并处理客户端驱动程序发送的电源请求 (函数设备堆栈) 的 FDO。 为了使客户端驱动程序成功进入和退出其功能的挂起状态，复合驱动程序必须支持函数挂起和远程唤醒功能，并处理收到的 power 请求。

在 Windows 8 中，USB 3.0 设备的 USB 驱动程序堆栈支持这些功能。 此外，函数挂起和函数远程唤醒实现已添加到 Microsoft 提供的 [USB 通用父驱动程序](usb-common-class-generic-parent-driver.md) ( # A0) ，这是 Windows 默认复合驱动程序。 如果要编写自定义复合驱动程序，则驱动程序必须根据以下过程处理与函数挂起和远程唤醒请求相关的请求。

<a name="instructions"></a>Instructions
------------

### <a name="step-1-determine-whether-the-usb-driver-stack-supports-function-suspend"></a><a href="" id="determine-whether-the-usb-driver-stack-supports-function-suspend"></a>步骤1：确定 USB 驱动程序堆栈是否支持函数挂起

在启动设备例程中 ([**IRP \_ MN \_ 启动 \_ 设备**](../kernel/irp-mn-start-device.md)) 复合驱动程序，请执行以下步骤：

1.  调用 [**USBD \_ QueryUsbCapability**](/previous-versions/windows/hardware/drivers/hh406230(v=vs.85)) 例程来确定基础 USB 驱动程序堆栈是否支持函数挂起功能。 此调用需要有效的 USBD 句柄，该句柄是在之前对 [**USBD \_ CreateHandle**](/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_createhandle) 例程的调用中获取的。

    成功调用 [**USBD \_ QueryUsbCapability**](/previous-versions/windows/hardware/drivers/hh406230(v=vs.85)) 会确定基础 USB 驱动程序堆栈是否支持函数挂起。 调用可能会返回一个错误代码，指示 USB 驱动程序堆栈不支持函数挂起，或者连接的设备不是 USB 3.0 多功能设备。

2.  如果 [**USBD \_ QueryUsbCapability**](/previous-versions/windows/hardware/drivers/hh406230(v=vs.85)) 调用指示支持函数挂起，请将复合设备注册到基础 USB 驱动程序堆栈。 若要注册复合设备，必须发送 [**IOCTL \_ 内部 \_ USB \_ 注册 \_ 复合 \_ 设备**](/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_register_composite_device) i/o 控制请求。 有关此请求的详细信息，请参阅 [如何注册复合设备](register-a-composite-driver.md)。

    注册请求使用 [**注册 \_ 复合 \_ 设备**](/windows-hardware/drivers/ddi/usbdlib/ns-usbdlib-_register_composite_device) 结构来指定有关复合驱动程序的信息。 请确保将 **CapabilityFunctionSuspend** 设置为1，以指示复合驱动程序支持函数挂起。

有关演示如何确定 USB 驱动程序堆栈是否支持函数挂起的代码示例，请参阅 [**USBD \_ QueryUsbCapability**](/previous-versions/windows/hardware/drivers/hh406230(v=vs.85))。

### <a name="step-2-handle-the-idle-irp"></a><a href="" id="handle-the-idle-irp"></a>步骤2：处理空闲 IRP

客户端驱动程序可以发送空闲 IRP (请参阅 [**IOCTL \_ 内部 \_ USB \_ 提交 \_ 空闲 \_ 通知**](/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification)) 。 当客户端驱动程序检测到该函数的空闲状态后，将发送该请求。 IRP 包含指向回调完成例程的指针， (称为 *空闲回调*) ，由客户端驱动程序实现。 在空闲回叫内，客户端会在将该函数发送到挂起状态之前执行任务，例如取消挂起的 i/o 传输。

**注意**   空闲 IRP 机制对于 USB 3.0 设备的客户端驱动程序是可选的。 但是，大多数客户端驱动程序都是为了支持 USB 2.0 和 USB 3.0 设备而编写的。 为了支持 USB 2.0 设备，驱动程序必须发送空闲 IRP，因为复合驱动程序依赖于该 IRP 跟踪每个函数的电源状态。 如果所有函数都处于空闲状态，则复合驱动程序会将整个设备发送到挂起状态。

 

在从客户端驱动程序接收到空闲 IRP 后，复合驱动程序必须立即调用空闲回调，以通知客户端驱动程序，客户端驱动程序可能会将该函数发送到挂起状态。

### <a name="step-3-send-a-request-for-remote-wake-up-notification"></a><a href="" id="send-a-request-for-remote-wake-up-notification"></a>步骤3：发送远程唤醒通知请求

客户端驱动程序可以通过将 [**irp \_ MJ \_ POWER**](../kernel/irp-mj-power.md) IRP 提交到 [**irp \_ MN \_ wait \_ 唤醒**](../kernel/irp-mn-wait-wake.md) (等待唤醒 IRP) ，将请求提交到 arm 用于远程唤醒的功能。 仅当驱动程序要通过用户事件输入工作状态时，客户端驱动程序才会提交此请求。

接收到等待唤醒 IRP 后，复合驱动程序必须将 [**IOCTL \_ 内部 \_ USB \_ 请求 \_ 远程 \_ 唤醒 \_ 通知**](/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_request_remote_wake_notification) i/o 控制请求发送到 USB 驱动程序堆栈。 当堆栈接收到有关恢复信号的通知时，该请求允许 USB 驱动程序堆栈通知复合驱动程序。 **IOCTL \_ 内部 \_ USB \_ 请求 \_ 远程 \_ 唤醒 \_ 通知**使用[**请求 \_ 远程 \_ 唤醒 \_ 通知**](/windows-hardware/drivers/ddi/usbdlib/ns-usbdlib-_request_remote_wake_notification)结构来指定请求参数。 复合驱动程序必须指定的值之一是为远程唤醒提供的函数的函数句柄。 复合驱动程序在以前的请求中获取了该句柄，以便将复合设备注册到 USB 驱动程序堆栈。 有关复合驱动程序注册请求的详细信息，请参阅 [如何注册复合设备](register-a-composite-driver.md)。

在请求的 IRP 中，复合驱动程序提供一个指向 (远程唤醒) 完成例程的指针，该例程由复合驱动程序实现。

下面的示例代码演示如何发送远程唤醒请求。

```ManagedCPlusPlus
/*++

Description: 
    This routine sends a IOCTL_INTERNAL_USB_REQUEST_REMOTE_WAKE_NOTIFICATION request
    to the USB driver stack. The IOCTL is completed by the USB driver stack 
    when the function wakes up from sleep.

    Parameters:
    parentFdoExt: The device context associated with the FDO for the
    composite driver.

    functionPdoExt: The device context associated with the PDO (created by 
    the composite driver) for the client driver.
--*/

VOID
SendRequestForRemoteWakeNotification(
    __inout PPARENT_FDO_EXT parentFdoExt,
    __inout PFUNCTION_PDO_EXT functionPdoExt
)

{
    PIRP                                irp;
    REQUEST_REMOTE_WAKE_NOTIFICATION    remoteWake;
    PIO_STACK_LOCATION                  nextStack;
    NTSTATUS                            status;

    // Allocate an IRP
    irp =  IoAllocateIrp(parentFdoExt->topDevObj->StackSize, FALSE); 

    if (irp)
    {
 
        //Initialize the USBDEVICE_REMOTE_WAKE_NOTIFICATION structure
        remoteWake.Version = 0;
        remoteWake.Size = sizeof(REQUEST_REMOTE_WAKE_NOTIFICATION);
        remoteWake.UsbdFunctionHandle = functionPdoExt->functionHandle;
        remoteWake.Interface = functionPdoExt->baseInterfaceNumber;

        nextStack = IoGetNextIrpStackLocation(irp);

        nextStack->MajorFunction = IRP_MJ_INTERNAL_DEVICE_CONTROL;   
        nextStack->Parameters.DeviceIoControl.IoControlCode = IOCTL_INTERNAL_USB_REQUEST_REMOTE_WAKE_NOTIFICATION;

        nextStack->Parameters.Others.Argument1 = &remoteWake;
        
        // Caller's completion routine will free the IRP when it completes.
 
        SetCompletionRoutine(functionPdoExt->debugLog,
                             parentFdoExt->fdo,
                             irp, 
                             CompletionRemoteWakeNotication, 
                             (PVOID)functionPdoExt, 
                             TRUE, TRUE, TRUE);

        // Pass the IRP
        IoCallDriver(parentFdoExt->topDevObj, irp);

    }

    return;
}
```

[**IOCTL \_ 内部 \_ usb \_ 请求 \_ 远程 \_ 唤醒 \_ 通知**](/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_request_remote_wake_notification)请求在唤醒过程收到有关恢复信号的通知时，由 usb 驱动程序堆栈完成。 在此期间，USB 驱动程序堆栈还会调用远程唤醒完成例程。

复合驱动程序必须保持等待唤醒 IRP 处于挂起状态，并将其排队等待以后处理。 当驱动程序的远程唤醒完成例程被 USB 驱动程序堆栈调用时，复合驱动程序必须完成 IRP。

### <a name="step-4-send-a-request-to-arm-the-function-for-remote-wake-up"></a><a href="" id="send-a-request-to-arm-the-function-for-remote-wake-up"></a>步骤4：向 Arm 发送用于远程唤醒功能的请求

若要将该函数发送到低功耗状态，客户端驱动程序会提交 [**IRP \_ MN \_ SET \_ power**](../kernel/irp-mn-set-power.md) IRP，其中包含将 Windows 驱动模型 (WDM) 设备电源状态更改为 **D2** 或 **D3**的请求。 通常，如果驱动程序之前发送了等待唤醒 IRP 来请求远程唤醒，则客户端驱动程序将发送 **D2** irp。 否则，客户端驱动程序将发送 **D3** IRP。

收到 **D2** IRP 后，复合驱动程序必须首先确定等待唤醒 IRP 是否是由客户端驱动程序发送的前一请求挂起的。 如果该 IRP 处于挂起状态，则复合驱动程序必须将该函数 arm 用于远程唤醒。 为此，复合驱动程序必须将设置的 \_ 功能控制请求发送到函数的第一个接口，以使设备能够发送恢复信号。 若要发送控制请求，请调用[**USBD \_ UrbAllocate**](/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_urballocate)例程来分配[**URB**](/windows-hardware/drivers/ddi/usb/ns-usb-_urb)结构，并调用[**UsbBuildFeatureRequest**](/previous-versions/ff538932(v=vs.85))宏来格式化设置功能请求的**URB** \_ 。 在调用中，将 URB \_ 函数 \_ SET \_ 功能指定 \_ 为 \_ INTERFACE 作为操作代码，并将 USB \_ 功能 \_ 函数 \_ 挂起作为功能选择器。 在 *Index* 参数中，设置最高有效字节的 **第1位** 。 该值会复制到传输的安装包中的 **wIndex** 字段。

下面的示例演示如何发送设置的 \_ 功能控制请求。

```ManagedCPlusPlus
/*++

Routine Description:

Sends a SET_FEATURE for REMOTE_WAKEUP to the device using a standard control request.

Parameters:
parentFdoExt: The device context associated with the FDO for the
composite driver.

functionPdoExt: The device context associated with the PDO (created by 
the composite driver) for the client driver.

Returns:

NTSTATUS code.

--*/
VOID
    NTSTATUS SendSetFeatureControlRequestToSuspend(
    __inout PPARENT_FDO_EXT parentFdoExt,
    __inout PFUNCTION_PDO_EXT functionPdoExt,
    )

{
    PURB                            urb
    PIRP                            irp;
    PIO_STACK_LOCATION              nextStack;
    NTSTATUS                        status;

    status = USBD_UrbAllocate(parentFdoExt->usbdHandle, &urb);

    if (!NT_SUCCESS(status))
    {    
        //USBD_UrbAllocate failed.
        goto Exit;
    }

    //Format the URB structure.
    UsbBuildFeatureRequest (
        urb,
        URB_FUNCTION_SET_FEATURE_TO_INTERFACE, // Operation code
        USB_FEATURE_FUNCTION_SUSPEND,          // feature selector
        functionPdoExt->firstInterface,           // first interface of the function
        NULL);

    irp =  IoAllocateIrp(parentFdoExt->topDevObj->StackSize, FALSE); 

    if (!irp)
    {
        // IoAllocateIrp failed.
        status = STATUS_INSUFFICIENT_RESOURCES;

        goto Exit;
    }

    nextStack = IoGetNextIrpStackLocation(irp);

    nextStack->MajorFunction = IRP_MJ_INTERNAL_DEVICE_CONTROL;  

    nextStack->Parameters.DeviceIoControl.IoControlCode = IOCTL_INTERNAL_USB_SUBMIT_URB;  

    //  Attach the URB to the IRP.
    USBD_AssignUrbToIoStackLocation(nextStack, (PURB)urb);

    // Caller's completion routine will free the IRP when it completes.
    SetCompletionRoutine(functionPdoExt->debugLog,
        parentFdoExt->fdo,
        irp, 
        CompletionForSuspendControlRequest, 
        (PVOID)functionPdoExt, 
        TRUE, TRUE, TRUE);


    // Pass the IRP
    IoCallDriver(parentFdoExt->topDevObj, irp);


Exit:
    if (urb)
    {
        USBD_UrbFree( parentFdoExt->usbdHandle, urb); 
    }

    return status;

}
```

然后，复合驱动程序将 **D2** IRP 发送到 USB 驱动程序堆栈。 如果其他所有函数都处于挂起状态，则 USB 驱动程序堆栈通过操纵控制器上的某些端口寄存器来挂起端口。

<a name="remarks"></a>备注
-------

在鼠标函数示例中，由于启用了远程唤醒功能 (请参阅步骤 4) ，当用户摆动鼠标时，鼠标函数将在上游到主控制器的网络上生成一个恢复信号。 然后，控制器会发送包含有关唤醒的函数的信息的通知数据包，通知 USB 驱动程序堆栈。 有关函数唤醒通知的信息，请参阅 USB 3.0 规范中的图8-17。

收到通知数据包后，USB 驱动程序堆栈完成挂起的 [**IOCTL \_ 内部 \_ USB \_ 请求 \_ 远程 \_ 唤醒 \_ 通知**](/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_request_remote_wake_notification) 请求 (参见步骤 3) ，并调用在请求中指定并由复合驱动程序实现的 (远程唤醒) 完成回调例程。 当通知到达复合驱动程序时，它会通过完成客户端驱动程序之前发送的等待唤醒 IRP，通知相应的客户端驱动程序该函数已进入工作状态。

在 (远程唤醒) 完成例程中，复合驱动程序应将工作项排队，以完成挂起的等待唤醒 IRP。 对于 USB 3.0 设备，复合驱动程序仅唤醒发送恢复信号并使其他功能处于挂起状态的函数。 对工作项进行排队可确保与 USB 2.0 设备的函数驱动程序的现有实现兼容。 有关对工作项进行排队的信息，请参阅 [**IoQueueWorkItem**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioqueueworkitem)。

工作线程完成等待唤醒 IRP，并调用客户端驱动程序的完成例程。 然后，完成例程将发送 **D0** IRP 以进入工作状态。 在完成 wait-唤醒 IRP 之前，复合驱动程序应调用 [**PoSetSystemWake**](/windows-hardware/drivers/ddi/wdm/nf-wdm-posetsystemwake) ，将等待唤醒 irp 标记为使系统从挂起状态中唤醒。 Power manager 会记录 Windows (ETW) 事件的事件跟踪 (可在全局系统通道) 查看，其中包括有关唤醒系统的设备的信息。

## <a name="related-topics"></a>相关主题
[USB 电源管理](usb-power-management.md)  
[USB 选择性挂起](usb-selective-suspend.md)
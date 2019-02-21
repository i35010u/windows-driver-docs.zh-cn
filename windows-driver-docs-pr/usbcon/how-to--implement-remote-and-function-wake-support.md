---
Description: This topic provides an overview of function suspend and function remote wake-up features for Universal Serial Bus (USB) 3.0 multi-function devices (composite devices).
title: 如何实现复合的驱动程序中函数挂起
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfa7d517aec6c957a903c245d8cdcedb8f2dad27
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555834"
---
# <a name="how-to-implement-function-suspend-in-a-composite-driver"></a>如何实现复合的驱动程序中函数挂起


本主题提供的函数概述挂起和函数远程唤醒功能的通用串行总线 (USB) 3.0 的多功能设备 （复合设备）。 本主题中将学习如何在控制复合设备的驱动程序中实现这些功能。 本主题适用于复合替换 Usbccgp.sys 的驱动程序。

通用串行总线 (USB) 3.0 规范定义了名为的新功能*函数挂起*。 功能，单个复合设备进入低功耗状态，独立于其他函数的函数。 请考虑定义的函数键盘和鼠标的另一个函数的复合设备。 用户在工作状态中保持键盘功能，但不会为一段时间内移动鼠标。 鼠标的客户端驱动程序可以检测函数的空闲状态，并将发送键盘功能仍处于工作状态时暂停状态的函数。

当所有各个函数处于挂起状态时，整个复合设备转换到挂起状态。 但是，可以在转换整个设备来挂起状态而不考虑任何函数中设备的电源状态。 如果特定函数和整个设备进入挂起状态，设备处于挂起状态，并在整个设备的挂起进入和退出流程时保留该函数的挂起状态。

类似于 USB 2.0 设备的远程唤醒功能 (请参阅[USB 设备的远程唤醒](remote-wakeup-of-usb-devices.md))，USB 3.0 复合设备中的单个函数可唤醒从低功耗状态而不会影响其他函数的电源状态。 此功能被称为*函数远程唤醒*。 启用此功能是显式由宿主远程唤醒位设置设备的固件中的协议请求发送。 此过程称为*武装远程唤醒函数*。 有关唤醒相关的远程位的信息，请参阅官方的 USB 规范中的图 9-6。

如果为远程唤醒函数有一个函数 （当在挂起的状态） 将保留足够的电源来生成唤醒*恢复信号*物理设备上发生用户事件时。 由于该恢复信号，而客户端驱动程序可以则退出挂起关联函数的状态。 在复合设备中的鼠标函数的示例中，，当用户 wiggles 处于空闲状态，鼠标鼠标函数将恢复信号发送到主机。 在主机上的 USB 驱动程序堆栈检测到哪个函数中唤醒，并将传播到客户端驱动程序的相应函数的通知。 客户端驱动程序可以然后唤醒函数并进入工作状态。

客户端驱动程序发送挂起状态和唤醒此函数的函数的步骤是类似于单函数设备驱动程序将发送整个设备以挂起状态。 以下过程总结了这些步骤。

1.  检测关联的函数时处于空闲状态。
2.  发送到空闲的 I/O 请求数据包 (IRP)。
3.  提交请求以通过发送唤醒等待 I/O 请求数据包 (IRP) 的 arm 远程唤醒其功能。
4.  转换到低功耗状态函数通过发送**Dx** Irp 的 power (**D2**或**D3**)。

有关上述步骤的详细信息，请参阅"发送 USB 空闲请求 IRP"中[USB 选择性挂起](usb-selective-suspend.md)。
复合驱动程序中发送的客户端驱动程序 (函数设备堆栈的 FDO) 复合设备和句柄 power 请求创建的每个函数的物理设备对象 (PDO)。 为了使客户端驱动程序已成功进入和退出时挂起其功能的状态、 复合驱动程序必须支持功能挂起并远程唤醒功能和进程接收的强大功能请求。

在 Windows 8 中，USB 3.0 设备的 USB 驱动程序堆栈支持这些功能。 此外，函数挂起和已添加到 Microsoft 提供函数远程唤醒实施[USB 泛型父驱动程序](usb-common-class-generic-parent-driver.md)(Usbccgp.sys)，这是 Windows 默认复合驱动程序。 如果你正在编写自定义复合驱动程序，您的驱动程序必须处理与函数相关的请求挂起和远程唤醒请求时，按照以下过程。

<a name="instructions"></a>说明
------------

### <a href="" id="determine-whether-the-usb-driver-stack-supports-function-suspend"></a>步骤 1:确定是否挂起 USB 驱动程序堆栈支持函数

在开始设备例程 ([**IRP\_MN\_启动\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551749)) 的复合驱动程序，请执行以下步骤：

1.  调用[ **USBD\_QueryUsbCapability** ](https://msdn.microsoft.com/library/windows/hardware/hh406230)例程，以确定基础的 USB 驱动程序堆栈是否支持该函数挂起功能。 调用需要有效 USBD 处理你在上一个调用中获取[ **USBD\_CreateHandle** ](https://msdn.microsoft.com/library/windows/hardware/hh406241)例程。

    在成功调用[ **USBD\_QueryUsbCapability** ](https://msdn.microsoft.com/library/windows/hardware/hh406230)确定基础的 USB 驱动程序堆栈支持函数是否挂起。 该调用可以返回一个错误代码，指示 USB 驱动程序堆栈不支持函数挂起或所连接的设备不是 USB 3.0 多功能设备。

2.  如果[ **USBD\_QueryUsbCapability** ](https://msdn.microsoft.com/library/windows/hardware/hh406230)调用指示函数挂起支持，复合设备注册到底层的 USB 驱动程序堆栈。 若要注册复合设备，必须将发送[ **IOCTL\_内部\_USB\_注册\_复合\_设备**](https://msdn.microsoft.com/library/windows/hardware/hh450854) I/O控制请求。 有关此请求的详细信息，请参阅[如何注册复合设备](register-a-composite-driver.md)。

    注册请求使用[**注册\_复合\_设备**](https://msdn.microsoft.com/library/windows/hardware/hh450898)结构，以指定的复合的驱动程序的信息。 请确保您设置**CapabilityFunctionSuspend**为 1，表示复合驱动程序支持函数挂起。

有关代码示例，演示如何确定 USB 驱动程序堆栈是否支持函数挂起，请参阅[ **USBD\_QueryUsbCapability**](https://msdn.microsoft.com/library/windows/hardware/hh406230)。

### <a href="" id="handle-the-idle-irp"></a>步骤 2:句柄空闲的 IRP

客户端驱动程序可以发送空闲 IRP (请参阅[ **IOCTL\_内部\_USB\_提交\_空闲\_通知**](https://msdn.microsoft.com/library/windows/hardware/ff537270))。 客户端驱动程序已检测到该函数的空闲状态后，发送请求。 IRP 包含回调完成例程的指针 (称为*空闲回调*)，其由客户端驱动程序。 在空闲状态的回调中，客户端将执行任务，例如，取消挂起的 I/O 传输之前发送要挂起状态的函数。

**请注意**  空闲的 IRP 机制取决于您的 USB 3.0 设备的客户端驱动程序。 但是，大多数客户端驱动程序都编写为支持 USB 2.0 和 USB 3.0 设备。 若要支持 USB 2.0 设备，驱动程序必须发送空闲 IRP，，因为复合驱动程序依赖于该 IRP 来跟踪每个函数的电源状态。 如果所有函数都都处于空闲状态，复合的驱动程序将发送整个设备以挂起状态。

 

一旦收到来自客户端驱动程序空闲 IRP，复合的驱动程序必须立即调用空闲的回调，以通知客户端驱动程序，客户端驱动程序可能会发送要挂起状态的函数。

### <a href="" id="send-a-request-for-remote-wake-up-notification"></a>步骤 3:将请求发送远程唤醒通知

客户端驱动程序可以提交请求以提交 arm 其功能的远程唤醒[ **IRP\_MJ\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff550784) IRP 次要功能代码设置为[**IRP\_MN\_等待\_唤醒**](https://msdn.microsoft.com/library/windows/hardware/ff551766) (等待唤醒 IRP)。 仅当该驱动程序想要输入由于用户事件的工作状态，客户端驱动程序将提交此请求。

一旦收到等待唤醒 IRP，复合的驱动程序必须发送[ **IOCTL\_内部\_USB\_请求\_远程\_唤醒\_通知** ](https://msdn.microsoft.com/library/windows/hardware/hh450856)到 USB 驱动程序堆栈的 I/O 控制请求。 请求启用 USB 驱动程序堆栈，以通知复合驱动程序，当堆栈收到有关恢复信号通知。 **IOCTL\_内部\_USB\_请求\_远程\_唤醒\_通知**使用[**请求\_远程\_唤醒\_通知**](https://msdn.microsoft.com/library/windows/hardware/hh406227)结构，以指定的请求参数。 复合驱动程序必须指定的值之一是了解有关远程唤醒的函数的函数句柄。 复合驱动程序获得复合设备注册到 USB 驱动程序堆栈的前一个请求中该句柄。 有关复合驱动程序的注册请求的详细信息，请参阅[如何注册复合设备](register-a-composite-driver.md)。

在请求 IRP，复合的驱动程序提供一个指向 （远程唤醒） 完成例程，由复合驱动程序实现。

下面的代码示例演示如何将远程唤醒请求发送。

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
        
        // Caller&#39;s completion routine will free the IRP when it completes.
 
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

[ **IOCTL\_内部\_USB\_请求\_远程\_唤醒\_通知**](https://msdn.microsoft.com/library/windows/hardware/hh450856)请求完成的在唤醒过程中收到有关恢复信号通知时 USB 驱动程序堆栈。 在此期间，USB 驱动程序堆栈还调用远程唤醒完成例程。

复合的驱动程序必须保留挂起的等待唤醒 IRP，队列供以后处理。 USB 驱动程序堆栈获取调用驱动程序的远程唤醒完成例程时，复合的驱动程序必须完成该 IRP。

### <a href="" id="send-a-request-to-arm-the-function-for-remote-wake-up"></a>步骤 4:发送请求以 Arm 远程唤醒的函数

若要将该函数发送到低功耗状态，客户端驱动程序提交[ **IRP\_MN\_设置\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff551744)与请求后，若要更改的 Windows 驱动程序模型 （IRPWDM) 设备的电源状态更改为**D2**或**D3**。 通常情况下，客户端驱动程序发送**D2** IRP 如果驱动程序发送等待唤醒 IRP，更低，以便请求远程唤醒。 否则，客户端驱动程序将发送**D3** IRP。

在接收时**D2** IRP，复合的驱动程序必须首先确定等待唤醒 IRP 处于挂起状态的客户端驱动程序发送的前一个请求。 如果该 IRP 处于挂起状态，复合的驱动程序必须 arm 远程唤醒的函数。 若要执行此操作，复合的驱动程序必须发送一组\_功能控制请求的函数的第一个接口以允许设备将恢复信号发送。 若要发送控制请求，分配[ **URB** ](https://msdn.microsoft.com/library/windows/hardware/ff538923)结构通过调用[ **USBD\_UrbAllocate** ](https://msdn.microsoft.com/library/windows/hardware/hh406250)例程并调用[ **UsbBuildFeatureRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff538932)若要设置格式的宏**URB**针对一\_功能请求。 在调用中，指定 URB\_函数\_设置\_功能\_TO\_作为操作代码和 USB 接口\_功能\_函数\_挂起功能选择器。 在中*索引*参数，设置**位 1**的最高有效字节。 将值复制到**wIndex**安装数据包的传输中的字段。

下面的示例演示如何将发送一组\_功能控制请求。

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

    // Caller&#39;s completion routine will free the IRP when it completes.
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

然后，复合的驱动程序将发送**D2** irp USB 驱动程序堆栈向下的传递。 如果所有其他函数中挂起状态，USB 驱动程序堆栈通过操作在控制器上的某些端口寄存器将挂起该端口。

<a name="remarks"></a>备注
-------

在鼠标函数示例中，因为启用远程唤醒功能 （请参阅步骤 4），用户 wiggles 鼠标时，鼠标函数将生成上游到主控制器在网络上的恢复信号。 然后，控制器通过发送通知的数据包，其中包含有关唤醒函数的信息通知 USB 驱动程序堆栈。 有关函数唤醒通知的信息，请参阅 USB 3.0 规范中的图 8-17。

USB 驱动程序堆栈完成时接收通知数据包，挂起[ **IOCTL\_内部\_USB\_请求\_远程\_唤醒\_通知**](https://msdn.microsoft.com/library/windows/hardware/hh450856)请求 （请参阅步骤 3），并调用 （远程唤醒） 完成回调例程请求中指定并由复合驱动程序实现。 当通知到达复合驱动程序时，它通知相应客户端驱动程序函数已通过完成等待唤醒 IRP 之前发送客户端驱动程序进入工作状态。

（远程唤醒） 完成例程，复合的驱动程序应将工作项排队以完成挂起的等待唤醒 IRP。 适用于 USB 3.0 设备仅发出继续信号并离开中的其他函数的函数会复合驱动程序被唤醒挂起状态。 队列工作项可确保与现有实现的 USB 2.0 设备功能的驱动程序的兼容性。 有关队列的工作项的信息，请参阅[ **IoQueueWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff549466)。

工作线程完成等待唤醒 IRP，并调用客户端驱动程序的完成例程。 然后将发送完成例程**D0** IRP 在工作状态中输入该函数。 在完成之前等待唤醒 IRP，复合的驱动程序应调用[ **PoSetSystemWake** ](https://msdn.microsoft.com/library/windows/hardware/ff559770)标记等待唤醒 IRP 与参与唤醒从系统挂起状态。 电源管理器记录的事件跟踪 Windows (ETW) 事件 （可在全球系统通道中查看），其中包含有关设备的系统中唤醒的信息。

## <a name="related-topics"></a>相关主题
[USB 电源管理](usb-power-management.md)  
[USB 选择性挂起](usb-selective-suspend.md)  




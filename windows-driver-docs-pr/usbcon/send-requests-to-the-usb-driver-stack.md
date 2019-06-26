---
Description: 本主题介绍提交初始化的 URB USB 驱动程序堆栈处理特定请求所需的步骤。
title: 如何提交 URB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad3fb4d37b57997fcf3897307a046aca624fe456
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358340"
---
# <a name="how-to-submit-an-urb"></a>如何提交 URB


本主题介绍提交初始化的 URB USB 驱动程序堆栈处理特定请求所需的步骤。

客户端驱动程序通过使用传递给类型的 I/O 请求数据包 (Irp) 中的设备的 I/O 控制 (IOCTL) 的代码请求其设备与通信[ **IRP\_MJ\_内部\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)。 对于特定的设备的请求，如选择配置请求，请求将介绍与 IRP USB 请求块 (URB) 中。 将 URB IRP，与相关联并将请求发送到 USB 驱动程序堆栈的过程称为提交 URB。 若要提交 URB，客户端驱动程序必须使用[ **IOCTL\_内部\_USB\_提交\_URB** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_urb)作为设备控制代码。 IOCTL 是提供客户端驱动程序使用来管理其设备和设备连接到的端口的 I/O 接口的"内部"控制代码之一。 用户模式应用程序无权访问这些内部的 I/O 接口。 有关更多内核模式驱动程序的控制代码，请参阅[USB 客户端驱动程序的内核模式 Ioctl](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/#km-ioctl)。

### <a name="prerequisites"></a>系统必备

将请求发送到通用串行总线 (USB) 驱动程序堆栈之前, 的客户端驱动程序必须分配[ **URB** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb)结构并格式化该结构，具体取决于请求的类型。 有关详细信息，请参阅[Allocating 和构建 URBs](how-to-add-xrb-support-for-client-drivers.md)和[最佳实践：使用 URBs](usb-client-driver-contract-in-windows-8.md)。

<a name="instructions"></a>说明
------------

1.  通过调用为 URB 分配 IRP [ **IoAllocateIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateirp)例程。 必须提供接收 IRP 的设备对象的堆栈大小。 对上一个调用中接收到该设备对象的指针[ **IoAttachDeviceToDeviceStack** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioattachdevicetodevicestack)例程。 堆栈大小存储在**StackSize**的成员[**设备\_对象**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_object)结构。
2.  获取一个指向 IRP 的第一个堆栈位置 ([**IO\_堆栈\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)) 通过调用[ **IoGetNextIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetnextirpstacklocation).
3.  设置**MajorFunction**的成员[ **IO\_堆栈\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)结构[ **IRP\_MJ\_内部\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)。
4.  设置**Parameters.DeviceIoControl.IoControlCode**的成员[ **IO\_堆栈\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)结构[**IOCTL\_内部\_USB\_提交\_URB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_urb)。
5.  设置**Parameters.Others.Argument1**的成员[ **IO\_堆栈\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)初始化的地址的结构[**URB** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb)结构。 若要将关联到 URB IRP，或者可以调用[ **USBD\_AssignUrbToIoStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbd_assignurbtoiostacklocation)仅当由分配 URB [ **USBD\_UrbAllocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbd_urballocate)， [ **USBD\_SelectConfigUrbAllocateAndBuild**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbd_selectconfigurballocateandbuild)，或[ **USBD\_SelectInterfaceUrbAllocateAndBuild**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbd_selectinterfaceurballocateandbuild)。
6.  通过调用设置完成例程[ **IoSetCompletionRoutineEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutineex)。

    如果以异步方式提交 URB，将指针传递给调用方实现完成例程和其上下文中。 调用方释放在其完成例程 IRP。

    如果要以同步方式提交 IRP，实现完成例程，并将指针传递到在调用该例程[ **IoSetCompletionRoutineEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutineex)。 调用还需要在初始化的 KEVENT 对象*上下文*参数。 在您完成例程中，将事件设置为终止状态。

7.  调用[ **IoCallDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)转发填充的 IRP 设备堆栈中较低的下一个设备对象。 为同步调用，在调用**IoCallDriver**，等待事件对象，通过调用[ **KeWaitForSingleObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitforsingleobject)若要获取的事件通知。
8.  完成后 IRP，检查**IoStatus.Status** IRP 的成员和评估结果。 如果**IoStatus.Status**是状态\_成功后，请求已成功。

## <a name="complete-example"></a>完整示例


下面的示例演示如何以同步方式提交 URB。

```ManagedCPlusPlus
// The SubmitUrbSync routine submits an URB synchronously.
//
// Parameters:
//      DeviceExtension: Pointer to the caller's device extension. The
//                       device extension must have a pointer to 
//                       the next lower device object in the device stacks.  
//
//      Irp: Pointer to an IRP allocated by the caller.
//
//      Urb: Pointer to an URB that is allocated by  USBD_UrbAllocate, 
//           USBD_IsochUrbAllocate, USBD_SelectConfigUrbAllocateAndBuild, 
//           or USBD_SelectInterfaceUrbAllocateAndBuild.

//      CompletionRoutine: Completion routine.
//
// Return Value:                                                       
//                                                                      
//      NTSTATUS  

NTSTATUS SubmitUrbSync( PDEVICE_EXTENSION DeviceExtension,
                       PIRP Irp,
                       PURB Urb,  
                       PIO_COMPLETION_ROUTINE SyncCompletionRoutine)  

{

    NTSTATUS  ntStatus;  
    KEVENT    kEvent;

    PIO_STACK_LOCATION nextStack;

    // Get the next stack location.
    nextStack = IoGetNextIrpStackLocation(Irp);  

    // Set the major code.
    nextStack->MajorFunction = IRP_MJ_INTERNAL_DEVICE_CONTROL;  

    // Set the IOCTL code for URB submission.
    nextStack->Parameters.DeviceIoControl.IoControlCode = IOCTL_INTERNAL_USB_SUBMIT_URB;  

    // Attach the URB to this IRP.
    // The URB must be allocated by USBD_UrbAllocate, USBD_IsochUrbAllocate, 
    // USBD_SelectConfigUrbAllocateAndBuild, or USBD_SelectInterfaceUrbAllocateAndBuild.
    USBD_AssignUrbToIoStackLocation (DeviceExtension->UsbdHandle, nextStack, Urb);

    KeInitializeEvent(&kEvent, NotificationEvent, FALSE);

    ntStatus = IoSetCompletionRoutineEx ( DeviceExtension->NextDeviceObject,  
        Irp,  
        SyncCompletionRoutine,  
        (PVOID) &kEvent,  
        TRUE, 
        TRUE, 
        TRUE);

    if (!NT_SUCCESS(ntStatus))
    {
        KdPrintEx(( DPFLTR_IHVDRIVER_ID, DPFLTR_INFO_LEVEL, "IoSetCompletionRoutineEx failed. \n" ));
        goto Exit;
    }

    ntStatus = IoCallDriver(DeviceExtension->NextDeviceObject, Irp);  

    if (ntStatus == STATUS_PENDING) 
    {
        KeWaitForSingleObject ( &kEvent,
            Executive,
            KernelMode,
            FALSE,
            NULL);
    }

    ntStatus = Irp->IoStatus.Status;

Exit:

    if (!NT_SUCCESS(ntStatus))
    {
        // We hit a failure condition, 
        // We will free the IRP

        IoFreeIrp(Irp);
        Irp = NULL;
    }


    return ntStatus;
}

// The SyncCompletionRoutine routine is the completion routine 
// for the synchronous URB submit request.          
//
// Parameters:
//
//      DeviceObject: Pointer to the device object. 
//      Irp:          Pointer to an I/O Request Packet. 
//      CompletionContext: Context for the completion routine.
//
// Return Value:                                                       
//                                                                      
//      NTSTATUS  

NTSTATUS SyncCompletionRoutine ( PDEVICE_OBJECT DeviceObject,
                                PIRP           Irp,
                                PVOID          Context)
{
    PKEVENT kevent;

    kevent = (PKEVENT) Context;

    if (Irp->PendingReturned == TRUE)
    {
        KeSetEvent(kevent, IO_NO_INCREMENT, FALSE);
    }

    KdPrintEx(( DPFLTR_IHVDRIVER_ID, DPFLTR_INFO_LEVEL, "Request completed. \n" ));


    return STATUS_MORE_PROCESSING_REQUIRED;
} 
```

## <a name="complete-example"></a>完整示例


下面的示例演示如何以异步方式提交 URB。

```ManagedCPlusPlus
// The SubmitUrbASync routine submits an URB asynchronously.
//
// Parameters:
//
// Parameters:
//      DeviceExtension: Pointer to the caller's device extension. The
//                       device extension must have a pointer to 
//                       the next lower device object in the device stacks.  
//
//      Irp: Pointer to an IRP allocated by the caller.
//
//      Urb: Pointer to an URB that is allocated by  USBD_UrbAllocate, 
//           USBD_IsochUrbAllocate, USBD_SelectConfigUrbAllocateAndBuild, 
//           or USBD_SelectInterfaceUrbAllocateAndBuild.

//      CompletionRoutine: Completion routine.
//
//      CompletionContext: Context for the completion routine.
//
//
// Return Value:                                                       
//                                                                      
//      NTSTATUS      

NTSTATUS SubmitUrbASync ( PDEVICE_EXTENSION DeviceExtension,
                         PIRP Irp,
                         PURB Urb,  
                         PIO_COMPLETION_ROUTINE CompletionRoutine,  
                         PVOID CompletionContext)  
{
    // Completion routine is required if the URB is submitted asynchronously.
    // The caller's completion routine releases the IRP when it completes.


    NTSTATUS ntStatus = -1;  

    PIO_STACK_LOCATION nextStack = IoGetNextIrpStackLocation(Irp);  

    // Attach the URB to this IRP.
    nextStack->MajorFunction = IRP_MJ_INTERNAL_DEVICE_CONTROL;  

    // Attach the URB to this IRP.
    nextStack->Parameters.DeviceIoControl.IoControlCode = IOCTL_INTERNAL_USB_SUBMIT_URB;  

    // Attach the URB to this IRP.
    (void) USBD_AssignUrbToIoStackLocation (DeviceExtension->UsbdHandle, nextStack, Urb);  

    // Caller's completion routine will free the irp when it completes.
    ntStatus = IoSetCompletionRoutineEx ( DeviceExtension->NextDeviceObject,
        Irp,  
        CompletionRoutine,  
        CompletionContext,  
        TRUE, 
        TRUE, 
        TRUE);

    if (!NT_SUCCESS(ntStatus))
    {
        goto Exit;
    }

    (void) IoCallDriver(DeviceExtension->NextDeviceObject, Irp);

Exit:
    if (!NT_SUCCESS(ntStatus))
    {
        // We hit a failure condition, 
        // We will free the IRP

        IoFreeIrp(Irp);
        Irp = NULL;
    }

    return ntStatus;
}
```

## <a name="related-topics"></a>相关主题
[将请求发送到 USB 设备](communicating-with-a-usb-device.md)  




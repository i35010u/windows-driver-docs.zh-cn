---
description: 本主题介绍将已初始化的 URB 提交到 USB 驱动程序堆栈以处理特定请求所需的步骤。
title: 如何提交 URB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2e4f00bf28346b5688a51daf5b83d2a82268f55
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90010603"
---
# <a name="how-to-submit-an-urb"></a>如何提交 URB


本主题介绍将已初始化的 URB 提交到 USB 驱动程序堆栈以处理特定请求所需的步骤。

客户端驱动程序通过使用 i/o 控制代码 (IOCTL) 请求传递到 (irp [** \_ MJ \_ 内部 \_ 设备 \_ 控制**](../kernel/irp-mj-internal-device-control.md)的 irp) 中传递到设备的请求，与设备进行通信。 对于特定于设备的请求，例如选择配置请求，会在与 IRP 关联 (URB) 的 USB 请求块中描述请求。 将 URB 与 IRP 关联并将请求发送到 USB 驱动程序堆栈的过程称为提交 URB。 若要提交 URB，客户端驱动程序必须使用 [**IOCTL \_ 内部 \_ USB \_ 提交 \_ URB**](/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_urb) 作为设备控制代码。 IOCTL 是一个 "内部" 控制代码，它提供了一个 i/o 接口，客户端驱动程序使用该接口管理其设备和设备连接到的端口。 用户模式应用程序无权访问这些内部 i/o 接口。 有关内核模式驱动程序的更多控制代码，请参阅 [IOCTLs FOR USB Client 驱动程序的内核模式](/windows-hardware/drivers/ddi/_usbref/#km-ioctl)。

### <a name="prerequisites"></a>先决条件

在将请求发送到通用串行总线 (USB) 驱动程序堆栈之前，客户端驱动程序必须分配 [**URB**](/windows-hardware/drivers/ddi/usb/ns-usb-_urb) 结构并根据请求类型设置该结构的格式。 有关详细信息，请参阅 [分配和生成 URBs](how-to-add-xrb-support-for-client-drivers.md) 和 [最佳做法：使用 URBs](usb-client-driver-contract-in-windows-8.md)。

<a name="instructions"></a>Instructions
------------

1.  通过调用 [**IoAllocateIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp) 例程为 URB 分配 IRP。 必须提供接收 IRP 的设备对象的堆栈大小。 在之前调用 [**IoAttachDeviceToDeviceStack**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevicetodevicestack) 例程时收到指向该设备对象的指针。 堆栈大小存储在[**设备 \_ 对象**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)结构的**StackSize**成员中。
2.  通过调用[**IoGetNextIrpStackLocation**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetnextirpstacklocation)，获取指向 IRP 的第一个堆栈位置 ([**IO \_ 堆栈 \_ 位置**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)) 的指针。
3.  将[**IO \_ 堆栈 \_ 位置**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)结构的**MajorFunction**成员设置为[**IRP \_ MJ \_ 内部 \_ 设备 \_ 控制**](../kernel/irp-mj-internal-device-control.md)。
4.  将[**IO \_ 堆栈 \_ 位置**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)结构的**DeviceIoControl. IoControlCode**成员设置为[**IOCTL \_ 内部 \_ USB \_ SUBMIT \_ URB**](/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_urb)。
5.  将[**IO \_ 堆栈 \_ 位置**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)结构的**Argument1**成员设置为已初始化的[**URB**](/windows-hardware/drivers/ddi/usb/ns-usb-_urb)结构的地址。 若要将 IRP 关联到 URB，仅当 URB 已由[**USBD \_ UrbAllocate**](/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_urballocate)、 [**USBD \_ SelectConfigUrbAllocateAndBuild**](/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_selectconfigurballocateandbuild)或[**USBD \_ SelectInterfaceUrbAllocateAndBuild**](/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_selectinterfaceurballocateandbuild)分配时，才可以调用[**USBD \_ AssignUrbToIoStackLocation**](/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_assignurbtoiostacklocation) 。
6.  通过调用 [**IoSetCompletionRoutineEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutineex)设置完成例程。

    如果异步提交 URB，请将指针传递到调用方实现的完成例程及其上下文。 调用方在其完成例程中释放 IRP。

    如果要同步提交 IRP，请在调用 [**IoSetCompletionRoutineEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutineex)时实现一个完成例程，并将一个指针传递到该例程。 此调用还需要 *上下文* 参数中的已初始化 KEVENT 对象。 在完成例程中，将事件的状态设置为 "已终止"。

7.  调用 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) 将填充的 IRP 转发到设备堆栈中的下一个较低设备对象。 对于同步调用，在调用 **IoCallDriver**之后，通过调用 [**KeWaitForSingleObject**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject) 来等待事件对象，以获取事件通知。
8.  完成 IRP 后，请检查 IRP 的 **IoStatus** 成员并评估结果。 如果 **IOSTATUS** 状态为 "成功" \_ ，则请求成功。

## <a name="complete-example"></a>完整示例


下面的示例演示如何同步提交 URB。

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
[向 USB 设备发送请求](communicating-with-a-usb-device.md)
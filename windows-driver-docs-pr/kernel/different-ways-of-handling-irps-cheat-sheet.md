---
title: 不同的 IRP 处理方法 - 速查表
author: kaushika-msft
description: 不同的方法来处理 Irp
keywords:
- Irp WDK 内核，处理 Irp
ms.date: 12/07/2017
ms.localizationpriority: medium
ms.openlocfilehash: 555dc8d8fb051791959fe6492633481888f1fc87
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342695"
---
# <a name="different-ways-of-handling-irps---cheat-sheet"></a>不同的 IRP 处理方法 - 速查表 

Windows 驱动程序模型 (WDM) 驱动程序通常将输入/输出请求数据包 (Irp) 发送到其他驱动程序。 驱动程序创建其自己 IRP，并将其发送到较低的驱动程序，或该驱动程序将收到来自另一个驱动程序，它上面附加 Irp 转发。 

本文介绍了不同的方式的驱动程序可以将 Irp 发送到较低的驱动程序，并包括带批注的示例代码。

* 方案 1-5 是有关如何从调度例程将 IRP 转发到较低的驱动程序。
* 方案 6 到 12 讨论创建 IRP 和将其发送到另一个驱动程序的不同方法。

检查各种方案之前，请注意，STATUS_MORE_PROCESSING_REQUIRED 或 STATUS_SUCCESS 可以返回的 IRP 完成例程。

它将检查状态时，I/O 管理器将使用以下规则：

* 如果状态为 STATUS_MORE_PROCESSING_REQUIRED，停止完成 IRP，退出的堆栈位置保持不变并返回。
* 如果状态为 STATUS_MORE_PROCESSING_REQUIRED 之外的任何内容，则继续完成 IRP 向上。

由于 I/O 管理器无需知道使用的非 STATUS_MORE_PROCESSING_REQUIRED 值，使用 STATUS_SUCCESS （因为在大多数处理器体系结构上高效地加载的值为 0）。

在阅读下面的代码，请注意，STATUS_CONTINUE_COMPLETION 化名为 STATUS_SUCCESS WDK 中。

```cpp
// This value should be returned from completion routines to continue
// completing the IRP upwards. Otherwise, STATUS_MORE_PROCESSING_REQUIRED
// should be returned.
// 
#define STATUS_CONTINUE_COMPLETION      STATUS_SUCCESS
// 
// Completion routines can also use this enumeration instead of status codes.
// 
typedef enum _IO_COMPLETION_ROUTINE_RESULT {

    ContinueCompletion = STATUS_CONTINUE_COMPLETION,
    StopCompletion = STATUS_MORE_PROCESSING_REQUIRED

} IO_COMPLETION_ROUTINE_RESULT, *PIO_COMPLETION_ROUTINE_RESULT;
```

## <a name="forwarding-an-irp-to-another-driver"></a>转发到另一个驱动程序 IRP

### <a name="scenario-1-forward-and-forget"></a>方案 1：转发并忘记
如果驱动程序只是想要向下转发 IRP 并不执行任何其他操作，请使用下面的代码。 该驱动程序无需在这种情况下设置完成例程。 如果该驱动程序是一个最高级别驱动程序，IRP 可以完成同步或异步，具体取决于较低的驱动程序返回的状态。 

```cpp
NTSTATUS
DispatchRoutine_1(
    IN PDEVICE_OBJECT DeviceObject,
    IN PIRP Irp
    )
{
    // 
    // You are not setting a completion routine, so just skip the stack
    // location because it provides better performance.
    // 
    IoSkipCurrentIrpStackLocation (Irp);
    return IoCallDriver(TopOfDeviceStack, Irp);
} 
```

### <a name="scenario-2-forward-and-wait"></a>方案 2：正向和等待

如果驱动程序想要将转发到较低的驱动程序 IRP 并等待其返回，以便它可以处理 IRP，请使用下面的代码。 这么做通常是处理 PNP Irp 时。 例如，接收[执行了 IRP_MN_START_DEVICE](irp-mn-start-device.md) IRP，您必须转发到总线驱动程序 IRP 并等待它完成，才可以开始你的设备。 您可以调用[ **IoForwardIrpSynchronously** ](https://msdn.microsoft.com/library/windows/hardware/ff549100)要轻松地执行此操作。

```cpp
NTSTATUS
DispatchRoutine_2(
    IN PDEVICE_OBJECT DeviceObject,
    IN PIRP Irp
    )
{
    KEVENT   event;
    NTSTATUS status;

    KeInitializeEvent(&event, NotificationEvent, FALSE);

    // 
    // You are setting completion routine, so you must copy
    // current stack location to the next. You cannot skip a location
    // here.
    // 
    IoCopyCurrentIrpStackLocationToNext(Irp);

    IoSetCompletionRoutine(Irp,
                           CompletionRoutine_2,
                           &event,
                           TRUE,
                           TRUE,
                           TRUE
                           );

    status = IoCallDriver(TopOfDeviceStack, Irp);

    if (status == STATUS_PENDING) {

       KeWaitForSingleObject(&event,
                             Executive, // WaitReason
                             KernelMode, // must be Kernelmode to prevent the stack getting paged out
                             FALSE,
                             NULL // indefinite wait
                             );
       status = Irp->IoStatus.Status;
    }

    // <---- Do your own work here.


    // 
    // Because you stopped the completion of the IRP in the CompletionRoutine
    // by returning STATUS_MORE_PROCESSING_REQUIRED, you must call
    // IoCompleteRequest here.
    // 
    IoCompleteRequest (Irp, IO_NO_INCREMENT);
    return status;

}
NTSTATUS
CompletionRoutine_2(
    IN PDEVICE_OBJECT   DeviceObject,
    IN PIRP             Irp,
    IN PVOID            Context
    )
{ 
  if (Irp->PendingReturned == TRUE) {
    // 
    // You will set the event only if the lower driver has returned
    // STATUS_PENDING earlier. This optimization removes the need to
    // call KeSetEvent unnecessarily and improves performance because the
    // system does not have to acquire an internal lock.  
    // 
    KeSetEvent ((PKEVENT) Context, IO_NO_INCREMENT, FALSE);
  }
  // This is the only status you can return. 
  return STATUS_MORE_PROCESSING_REQUIRED;  
} 
```

### <a name="scenario-3-forward-with-a-completion-routine"></a>方案 3：转发与完成例程

在这种情况下，该驱动程序设置完成例程，将 IRP 转发，然后返回较低的驱动程序原样的状态。 设置完成例程的目的是在其返回途中 IRP 的内容进行修改。 

```cpp
NTSTATUS
DispathRoutine_3(
    IN PDEVICE_OBJECT DeviceObject,
    IN PIRP Irp
    )
{
    NTSTATUS status;

    // 
    // Because you are setting completion routine, you must copy the
    // current stack location to the next. You cannot skip a location
    // here.
    // 
    IoCopyCurrentIrpStackLocationToNext(Irp); 

    IoSetCompletionRoutine(Irp,
                           CompletionRoutine_31,// or CompletionRoutine_32
                           NULL,
                           TRUE,
                           TRUE,
                           TRUE
                           );

    return IoCallDriver(TopOfDeviceStack, Irp);
}
```

如果从调度例程返回较低的驱动程序的状态：

* 不得更改中完成例程 IRP 的状态。 这是为了确保 IRP 的 IoStatus 块 (Irp-> IoStatus.Status) 中设置的状态值将与低级驱动程序的返回状态相同。
* 必须将 IRP 的挂起状态的传播由 Irp PendingReturned->。
* 不得更改 IRP 项的工作。

因此，仅有 2 个有效的版本，在此方案中 （31 和 32） 完成例程的：

```cpp
NTSTATUS
CompletionRoutine_31 (
    IN PDEVICE_OBJECT   DeviceObject,
    IN PIRP             Irp,
    IN PVOID            Context
    )
{   

    // 
    // Because the dispatch routine is returning the status of lower driver
    // as is, you must do the following:
    // 
    if (Irp->PendingReturned) {

        IoMarkIrpPending( Irp );
    }

    return STATUS_CONTINUE_COMPLETION ; // Make sure of same synchronicity 
}

NTSTATUS
CompletionRoutine_32 (
    IN PDEVICE_OBJECT   DeviceObject,
    IN PIRP             Irp,
    IN PVOID            Context
    )
{   
    // 
    // Because the dispatch routine is returning the status of lower driver
    // as is, you must do the following:
    // 
    if (Irp->PendingReturned) {

        IoMarkIrpPending( Irp );
    }

    //    
    // To make sure of the same synchronicity, complete the IRP here.
    // You cannot complete the IRP later in another thread because the 
    // the dispatch routine is returning the status returned by the lower
    // driver as is.
    // 
    IoCompleteRequest( Irp,  IO_NO_INCREMENT);  

    // 
    // Although this is an unusual completion routine that you rarely see,
    // it is discussed here to address all possible ways to handle IRPs.  
    // 
    return STATUS_MORE_PROCESSING_REQUIRED; 
} 
```

### <a name="scenario-4-queue-for-later-or-forward-and-reuse"></a>方案 4:队列供稍后使用，或转发和重复使用

在驱动程序要排队 IRP 和更高版本对其进行处理，或转发到较低的驱动程序 IRP 和重用超过特定的次数之前完成 IRP 的情况下使用以下代码片段。 调度例程将挂起的 IRP 标记，并返回 STATUS_PENDING，因为将 IRP 更高版本在不同的线程中完成。 在这里，完成例程可以更改 IRP 的状态，如有必要 （与前面的方案）。 

```cpp
NTSTATUS
DispathRoutine_4(
    IN PDEVICE_OBJECT DeviceObject,
    IN PIRP Irp
    )
{
    NTSTATUS status;

    // 
    // You mark the IRP pending if you are intending to queue the IRP
    // and process it later. If you are intending to forward the IRP 
    // directly, use one of the methods discussed earlier in this article.
    // 
    IoMarkIrpPending( Irp );    

    // 
    // For demonstration purposes: this IRP is forwarded to the lower driver.
    // 
    IoCopyCurrentIrpStackLocationToNext(Irp); 

    IoSetCompletionRoutine(Irp,
                           CompletionRoutine_41, // or CompletionRoutine_42
                           NULL,
                           TRUE,
                           TRUE,
                           TRUE
                           ); 
    IoCallDriver(TopOfDeviceStack, Irp);

    // 
    // Because you marked the IRP pending, you must return pending,
    // regardless of the status of returned by IoCallDriver.
    // 
    return STATUS_PENDING ;

}
```

完成例程可以返回 STATUS_CONTINUE_COMPLETION 或 STATUS_MORE_PROCESSING_REQUIRED。 仅当你想要重复使用另一个线程从 IRP 和更高版本完成时，才返回 STATUS_MORE_PROCESSING_REQUIRED。

```cpp
NTSTATUS
CompletionRoutine_41(
    IN PDEVICE_OBJECT   DeviceObject,
    IN PIRP             Irp,
    IN PVOID            Context
    )
{ 
    // 
    // By returning STATUS_CONTINUE_COMPLETION , you are relinquishing the 
    // ownership of the IRP. You cannot touch the IRP after this.
    // 
    return STATUS_CONTINUE_COMPLETION ; 
} 


NTSTATUS
CompletionRoutine_42 (
    IN PDEVICE_OBJECT   DeviceObject,
    IN PIRP             Irp,
    IN PVOID            Context
    )
{  
    // 
    // Because you are stopping the completion of the IRP by returning the
    // following status, you must complete the IRP later.
    // 
    return STATUS_MORE_PROCESSING_REQUIRED ; 
}
```

### <a name="scenario-5-complete-the-irp-in-the-dispatch-routine"></a>方案 5:完成中的调度例程 IRP

此方案显示了如何完成中的调度例程 IRP。 

**重要**调度例程的返回状态时完成中的调度例程 IRP，应与匹配的 IRP IoStatus 块中设置的值的状态 (Irp-> IoStatus.Status)。

```cpp
NTSTATUS
DispatchRoutine_5(
    IN PDEVICE_OBJECT DeviceObject,
    IN PIRP Irp
    )
{
    // 
    // <-- Process the IRP here.
    // 
    Irp->IoStatus.Status = STATUS_XXX;
    Irp->IoStatus.Information = YYY;
    IoCompletRequest(Irp, IO_NO_INCREMENT);
    return STATUS_XXX;
}
```

## <a name="creating-irps-and-sending-them-to-another-driver"></a>创建 Irp，并将它们发送到另一个驱动程序

### <a name="introduction"></a>简介

检查这些方案之前，必须了解创建驱动程序的同步输入/输出请求数据包 (IRP) 和异步请求之间的差异。 

|    同步 （线程） 的 IRP                                                                                                                        |    异步 （非线程） 的 IRP                                                                                                                       |
|--------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    创建使用 IoBuildSynchronousFsdRequest 或 IoBuildDeviceIoControlRequest。                                                                  |    创建使用 IoBuildAsynchronousFsdRequest 或 IoAllocateIrp。 这适用于驱动程序的通信。                                 |
|    线程必须等待 IRP 才能完成。                                                                                                         |    线程不必等待 IRP 才能完成。                                                                                                 |
|    与创建它的线程相关联，因此，名称线程 Irp。 因此，如果在线程退出，I/O 管理器将取消 IRP。     |    未与创建它的线程关联。                                                                                                       |
|    不能在任意线程上下文中创建。                                                                                                 |    由于该线程不会等待 IRP 才能完成，可以在任意线程上下文中创建。                                             |
|    I/O 管理器执行 post 完成来释放与 IRP 相关联的缓冲区。                                                     |    I/O 管理器不能执行清理操作。 该驱动程序必须提供完成例程，并释放与 IRP 相关联的缓冲区。          |
|    必须在 IRQL 级别等于 passive_level 调用发送。                                                                                                |    可以在 IRQL 发送 DISPATCH_LEVEL 如果目标驱动程序的调度例程可以处理请求时 DISPATCH_LEVEL 小于或等于。     |

### <a name="scenario-6-send-a-synchronous-device-control-request-irpmjinternaldevicecontrolirpmjdevicecontrol-by-using-iobuilddeviceiocontrolrequest"></a>方案 6:使用 IoBuildDeviceIoControlRequest 发送同步的设备控制请求 (IRP_MJ_INTERNAL_DEVICE_CONTROL/IRP_MJ_DEVICE_CONTROL)

下面的代码演示如何调用[ **IoBuildDeviceIoControlRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548318)请求以进行同步的 IOCTL 请求。  有关详细信息，请参阅[IRP_MJ_INTERNAL_DEVICE_CONTROL](irp-mj-internal-device-control.md)并[IRP_MJ_DEVICE_CONTROL](irp-mj-device-control.md)。

```cpp
NTSTATUS
MakeSynchronousIoctl(
    IN PDEVICE_OBJECT    TopOfDeviceStack,
    IN ULONG         IoctlControlCode,
    PVOID             InputBuffer,
    ULONG             InputBufferLength,
    PVOID             OutputBuffer,
    ULONG             OutputBufferLength
    )
/*++

Arguments:

    TopOfDeviceStack- 

    IoctlControlCode              - Value of the IOCTL request

    InputBuffer        - Buffer to be sent to the TopOfDeviceStack

    InputBufferLength  - Size of buffer to be sent to the TopOfDeviceStack

    OutputBuffer       - Buffer for received data from the TopOfDeviceStack

    OutputBufferLength - Size of receive buffer from the TopOfDeviceStack

Return Value:

    NT status code

--*/ 
{
    KEVENT              event;
    PIRP                irp;
    IO_STATUS_BLOCK     ioStatus;
    NTSTATUS status;

    // 
    // Creating Device control IRP and send it to the another
    // driver without setting a completion routine.
    // 

    KeInitializeEvent(&event, NotificationEvent, FALSE);

    irp = IoBuildDeviceIoControlRequest (
                            IoctlControlCode,
                            TopOfDeviceStack,
                            InputBuffer,
                            InputBufferLength,
                            OutputBuffer,
                            OutputBufferLength,
                            FALSE, // External
                            &event,
                            &ioStatus);

    if (NULL == irp) {
        return STATUS_INSUFFICIENT_RESOURCES;
    }


    status = IoCallDriver(TopOfDeviceStack, irp);

    if (status == STATUS_PENDING) {
        // 
        // You must wait here for the IRP to be completed because:
        // 1) The IoBuildDeviceIoControlRequest associates the IRP with the
        //     thread and if the thread exits for any reason, it would cause the IRP
        //     to be canceled. 
        // 2) The Event and IoStatus block memory is from the stack and we
        //     cannot go out of scope.
        // This event will be signaled by the I/O manager when the
        // IRP is completed.
        // 
        status = KeWaitForSingleObject(
                     &event,
                     Executive, // wait reason
                     KernelMode, // To prevent stack from being paged out.
                     FALSE,     // You are not alertable
                     NULL);     // No time out !!!!

        status = ioStatus.Status;                     
    }

    return status;
}
```

### <a name="scenario-7-send-a-synchronous-device-control-ioctl-request-and-cancel-it-if-not-completed-in-a-certain-time-period"></a>方案 7:发送同步设备控制 (IOCTL) 请求并取消它，如果在某段时间内未完成 
此方案中是类似于前面的方案中，不同之处在于而不是无限期等待完成请求，它会等待某些用户指定的时间，并安全地取消 IOCTL 请求，如果等待超时。 

```cpp
typedef enum {

   IRPLOCK_CANCELABLE,
   IRPLOCK_CANCEL_STARTED,
   IRPLOCK_CANCEL_COMPLETE,
   IRPLOCK_COMPLETED

} IRPLOCK;
// 
// An IRPLOCK allows for safe cancellation. The idea is to protect the IRP
// while the canceller is calling IoCancelIrp. This is done by wrapping the
// call in InterlockedExchange(s). The roles are as follows:
// 
// Initiator/completion: Cancelable --> IoCallDriver() --> Completed
// Canceller: CancelStarted --> IoCancelIrp() --> CancelCompleted
// 
// No cancellation:
//   Cancelable-->Completed
// 
// Cancellation, IoCancelIrp returns before completion:
//   Cancelable --> CancelStarted --> CancelCompleted --> Completed
// 
// Canceled after completion:
//   Cancelable --> Completed -> CancelStarted
// 
// Cancellation, IRP completed during call to IoCancelIrp():
//   Cancelable --> CancelStarted -> Completed --> CancelCompleted
// 
//  The transition from CancelStarted to Completed tells the completer to block
//  postprocessing (IRP ownership is transferred to the canceller). Similarly,
//  the canceller learns it owns IRP postprocessing (free, completion, etc)
//  during a Completed->CancelCompleted transition.
// 


NTSTATUS
MakeSynchronousIoctlWithTimeOut(
    IN PDEVICE_OBJECT    TopOfDeviceStack,
    IN ULONG         IoctlControlCode,
    PVOID             InputBuffer,
    ULONG             InputBufferLength,
    PVOID             OutputBuffer,
    ULONG             OutputBufferLength,
    IN  ULONG               Milliseconds
    )
/*++

Arguments:

    TopOfDeviceStack   - 

    IoctlControlCode   - Value of the IOCTL request.

    InputBuffer        - Buffer to be sent to the TopOfDeviceStack.

    InputBufferLength  - Size of buffer to be sent to the TopOfDeviceStack.

    OutputBuffer       - Buffer for received data from the TopOfDeviceStack.

    OutputBufferLength - Size of receive buffer from the TopOfDeviceStack.

    Milliseconds       - Timeout value in Milliseconds

Return Value:

    NT status code

--*/ 
{
    NTSTATUS status;
    PIRP irp;
    KEVENT event;
    IO_STATUS_BLOCK ioStatus;
    LARGE_INTEGER dueTime;
    IRPLOCK lock;

    KeInitializeEvent(&event, NotificationEvent, FALSE);

    irp = IoBuildDeviceIoControlRequest (
                    IoctlControlCode,
                    TopOfDeviceStack,
                    InputBuffer,
                    InputBufferLength,
                    OutputBuffer,
                    OutputBufferLength,
                    FALSE, // External ioctl
                    &event,
                    &ioStatus);



    if (irp == NULL) {
        return STATUS_INSUFFICIENT_RESOURCES;
    }

    lock = IRPLOCK_CANCELABLE;

    IoSetCompletionRoutine(
                    irp,
                    MakeSynchronousIoctlWithTimeOutCompletion,
                    &lock,
                    TRUE,
                    TRUE,
                    TRUE
                    );

    status = IoCallDriver(TopOfDeviceStack, irp);

    if (status == STATUS_PENDING) {

        dueTime.QuadPart = -10000 * Milliseconds;

        status = KeWaitForSingleObject(
                            &event,
                            Executive,
                            KernelMode,
                            FALSE,
                            &dueTime
                            );

        if (status == STATUS_TIMEOUT) {

            if (InterlockedExchange((PVOID)&lock, IRPLOCK_CANCEL_STARTED) == IRPLOCK_CANCELABLE) {

                // 
                // You got it to the IRP before it was completed. You can cancel
                // the IRP without fear of losing it, because the completion routine
                // does not let go of the IRP until you allow it.
                // 
                IoCancelIrp(irp);

                // 
                // Release the completion routine. If it already got there,
                // then you need to complete it yourself. Otherwise, you got
                // through IoCancelIrp before the IRP completed entirely.
                // 
                if (InterlockedExchange(&lock, IRPLOCK_CANCEL_COMPLETE) == IRPLOCK_COMPLETED) {
                    IoCompleteRequest(irp, IO_NO_INCREMENT);
                }
            }

            KeWaitForSingleObject(&event, Executive, KernelMode, FALSE, NULL);

            ioStatus.Status = status; // Return STATUS_TIMEOUT

        } else {

            status = ioStatus.Status;
        }
    }

    return status;
}

NTSTATUS
MakeSynchronousIoctlWithTimeOutCompletion(
    IN PDEVICE_OBJECT   DeviceObject,
    IN PIRP             Irp,
    IN PVOID            Context
    )
{
    PLONG lock;

    lock = (PLONG) Context;

    if (InterlockedExchange(lock, IRPLOCK_COMPLETED) == IRPLOCK_CANCEL_STARTED) {
        // 
        // Main line code has got the control of the IRP. It will
        // now take the responsibility of completing the IRP. 
        // Therefore...
        return STATUS_MORE_PROCESSING_REQUIRED;
    }

    return STATUS_CONTINUE_COMPLETION ;
}
```

### <a name="scenario-8-send-a-synchronous-non-ioctl-request-by-using-iobuildsynchronousfsdrequest---completion-routine-returns-statuscontinuecompletion"></a>方案 8:使用 IoBuildSynchronousFsdRequest 发送同步的非 IOCTL 请求-完成例程返回 STATUS_CONTINUE_COMPLETION
下面的代码演示如何通过调用来同步的非 IOCTL 请求[ **IoBuildSynchronousFsdRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548330)。 方案 6 类似如下所示的方法。

```cpp
NTSTATUS
MakeSynchronousNonIoctlRequest (
    PDEVICE_OBJECT   TopOfDeviceStack,
    PVOID               WriteBuffer,
    ULONG               NumBytes
    )
/*++
Arguments:

    TopOfDeviceStack - 

    WriteBuffer       - Buffer to be sent to the TopOfDeviceStack.

    NumBytes  - Size of buffer to be sent to the TopOfDeviceStack.

Return Value:

    NT status code


--*/ 
{
    NTSTATUS        status;
    PIRP            irp;
    LARGE_INTEGER   startingOffset;
    KEVENT          event;
    IO_STATUS_BLOCK     ioStatus;
    PVOID context;

    startingOffset.QuadPart = (LONGLONG) 0;
    // 
    // Allocate memory for any context information to be passed
    // to the completion routine.
    // 
    context = ExAllocatePoolWithTag(NonPagedPool, sizeof(ULONG), 'ITag');
    if(!context) {
        return STATUS_INSUFFICIENT_RESOURCES;
    }

    KeInitializeEvent(&event,  NotificationEvent,   FALSE);

    irp = IoBuildSynchronousFsdRequest(
                IRP_MJ_WRITE,
                TopOfDeviceStack,
                WriteBuffer,
                NumBytes,


                &startingOffset, // Optional
                &event,
                &ioStatus
                ); 

    if (NULL == irp) {
        ExFreePool(context);
        return STATUS_INSUFFICIENT_RESOURCES;
    }

    IoSetCompletionRoutine(irp,
                   MakeSynchronousNonIoctlRequestCompletion,
                   context,
                   TRUE,
                   TRUE,
                   TRUE);

    status = IoCallDriver(TopOfDeviceStack, irp);

    if (status == STATUS_PENDING) {

       status = KeWaitForSingleObject(
                            &event,
                            Executive,
                            KernelMode,
                            FALSE, // Not alertable
                            NULL);
        status = ioStatus.Status;
    }

    return status;
}
NTSTATUS
MakeSynchronousNonIoctlRequestCompletion(
    IN PDEVICE_OBJECT   DeviceObject,
    IN PIRP             Irp,
    IN PVOID            Context
    )
{
    if (Context) {
        ExFreePool(Context);
    }
    return STATUS_CONTINUE_COMPLETION ;

}
```

### <a name="scenario-9-send-a-synchronous-non-ioctl-request-by-using-iobuildsynchronousfsdrequest---completion-routine-returns-statusmoreprocessingrequired"></a>方案 9:使用 IoBuildSynchronousFsdRequest 发送同步的非 IOCTL 请求-完成例程返回 STATUS_MORE_PROCESSING_REQUIRED 
此方案以及方案 8 之间的唯一区别是完成例程返回 STATUS_MORE_PROCESSING_REQUIRED。 

```cpp
NTSTATUS MakeSynchronousNonIoctlRequest2(
    PDEVICE_OBJECT TopOfDeviceStack,
    PVOID WriteBuffer,
    ULONG NumBytes
    )
/*++ Arguments:
    TopOfDeviceStack

    WriteBuffer     - Buffer to be sent to the TopOfDeviceStack.

    NumBytes        - Size of buffer to be sent to the TopOfDeviceStack.

Return Value:
    NT status code
--*/
{
    NTSTATUS        status;
    PIRP            irp;
    LARGE_INTEGER   startingOffset;
    KEVENT          event;
    IO_STATUS_BLOCK ioStatus;
    BOOLEAN         isSynchronous = TRUE;

    startingOffset.QuadPart = (LONGLONG) 0;
    KeInitializeEvent(&event, NotificationEvent, FALSE);
    irp = IoBuildSynchronousFsdRequest(
                IRP_MJ_WRITE,
                TopOfDeviceStack,
                WriteBuffer,
                NumBytes,
                &startingOffset, // Optional
                &event,
                &ioStatus
                );

    if (NULL == irp) {
        return STATUS_INSUFFICIENT_RESOURCES;
    }

    IoSetCompletionRoutine(irp,
                MakeSynchronousNonIoctlRequestCompletion2,
                (PVOID)&event,
                TRUE,
                TRUE,
                TRUE);

    status = IoCallDriver(TopOfDeviceStack, irp);

    if (status == STATUS_PENDING) {

        KeWaitForSingleObject(&event,
                              Executive,
                              KernelMode,
                              FALSE, // Not alertable
                              NULL);
        status = irp->IoStatus.Status;
        isSynchronous = FALSE;
    }

    //
    // Because you have stopped the completion of the IRP, you must
    // complete here and wait for it to be completed by waiting
    // on the same event again, which will be signaled by the I/O
    // manager.
    // NOTE: you cannot queue the IRP for
    // reuse by calling IoReuseIrp because it does not break the
    // association of this IRP with the current thread.
    //

    KeClearEvent(&event);
    IoCompleteRequest(irp, IO_NO_INCREMENT);

    //
    // We must wait here to prevent the event from going out of scope.
    // I/O manager will signal the event and copy the status to our
    // IoStatus block for synchronous IRPs only if the return status is not
    // an error. For asynchronous IRPs, the above mentioned copy operation
    // takes place regardless of the status value.
    //

    if (!(NT_ERROR(status) && isSynchronous)) {
        KeWaitForSingleObject(&event,
                              Executive,
                              KernelMode,
                              FALSE, // Not alertable
                              NULL);
    }
    return status;
}

NTSTATUS MakeSynchronousNonIoctlRequestCompletion2(
    IN PDEVICE_OBJECT   DeviceObject,
    IN PIRP             Irp,
    IN PVOID            Context )
{
    if (Irp->PendingReturned) {
        KeSetEvent ((PKEVENT) Context, IO_NO_INCREMENT, FALSE);
    }
    return STATUS_MORE_PROCESSING_REQUIRED;
}
```

### <a name="scenario-10-send-an-asynchronous-request-by-using-iobuildasynchronousfsdrequest"></a>方案 10:使用 IoBuildAsynchronousFsdRequest 发送的异步请求 
此方案显示了如何通过调用发出异步请求[ **IoBuildAsynchronousFsdRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548310)。 

在异步请求中，发出请求的线程不必等待 IRP 才能完成。 可以在任意线程上下文中创建 IRP，因为 IRP 不是与线程关联。 必须提供完成例程，并完成例程释放缓冲区和 IRP，如果你不想要重复使用 IRP。 这是因为 I/O 管理器不能执行后完成清理的驱动程序创建异步 Irp (使用创建**IoBuildAsynchronousFsdRequest**并**IoAllocateIrp**)。 

```cpp
NTSTATUS
MakeAsynchronousRequest (
    PDEVICE_OBJECT   TopOfDeviceStack,
    PVOID               WriteBuffer,
    ULONG               NumBytes
    )
/*++
Arguments:

    TopOfDeviceStack - 

    WriteBuffer       - Buffer to be sent to the TopOfDeviceStack.

    NumBytes  - Size of buffer to be sent to the TopOfDeviceStack.

--*/ 
{
    NTSTATUS        status;
    PIRP            irp;
    LARGE_INTEGER   startingOffset;
    PIO_STACK_LOCATION  nextStack;
    PVOID context;

    startingOffset.QuadPart = (LONGLONG) 0;

    irp = IoBuildAsynchronousFsdRequest(
                IRP_MJ_WRITE,
                TopOfDeviceStack,
                WriteBuffer,
                NumBytes,
                &startingOffset, // Optional
                NULL
                ); 

    if (NULL == irp) {

        return STATUS_INSUFFICIENT_RESOURCES;
    }

    // 
    // Allocate memory for context structure to be passed to the completion routine.
    // 
    context = ExAllocatePoolWithTag(NonPagedPool, sizeof(ULONG_PTR), 'ITag');
    if (NULL == context) {
        IoFreeIrp(irp);   
        return STATUS_INSUFFICIENT_RESOURCES;
    }

    IoSetCompletionRoutine(irp,
                   MakeAsynchronousRequestCompletion,
                   context,
                   TRUE,
                   TRUE,
                   TRUE);
    // 
    // If you want to change any value in the IRP stack, you must
    // first obtain the stack location by calling IoGetNextIrpStackLocation.
    // This is the location that is initialized by the IoBuildxxx requests and  
    // is the one that the target device driver is going to view.
    // 
    nextStack = IoGetNextIrpStackLocation(irp);
    // 
    // Change the MajorFunction code to something appropriate.
    // 
    nextStack->MajorFunction = IRP_MJ_SCSI;

    (void) IoCallDriver(TopOfDeviceStack, irp);

    return STATUS_SUCCESS;
}
NTSTATUS
MakeAsynchronousRequestCompletion(
    IN PDEVICE_OBJECT   DeviceObject,
    IN PIRP             Irp,
    IN PVOID            Context
    )
{
    PMDL mdl, nextMdl;

    // 
    // If the target device object is set up to do buffered i/o 
    // (TopOfDeviceStack->Flags and DO_BUFFERED_IO), then 
    // IoBuildAsynchronousFsdRequest request allocates a system buffer
    // for read and write operation. If you stop the completion of the IRP
    // here, you must free that buffer.
    // 

    if(Irp->AssociatedIrp.SystemBuffer && (Irp->Flags & IRP_DEALLOCATE_BUFFER) ) {
            ExFreePool(Irp->AssociatedIrp.SystemBuffer);
    }

    // 
    // If the target device object is set up do direct i/o (DO_DIRECT_IO), then 
    // IoBuildAsynchronousFsdRequest creates an MDL to describe the buffer
    // and locks the pages. If you stop the completion of the IRP, you must unlock
    // the pages and free the MDL.
    // 

    else if (Irp->MdlAddress != NULL) {
        for (mdl = Irp->MdlAddress; mdl != NULL; mdl = nextMdl) {
            nextMdl = mdl->Next;
            MmUnlockPages( mdl ); IoFreeMdl( mdl ); // This function will also unmap pages.
        }
        Irp->MdlAddress = NULL;
    }

    if(Context) {
        ExFreePool(Context);
    }



    // 
    // If you intend to queue the IRP and reuse it for another request,
    // make sure you call IoReuseIrp(Irp, STATUS_SUCCESS) before you reuse.
    // 
    IoFreeIrp(Irp);

    // 
    // NOTE: this is the only status that you can return for driver-created asynchronous IRPs.
    // 
    return STATUS_MORE_PROCESSING_REQUIRED;
}
```

### <a name="scenario-11-send-an-asynchronous-request-by-using-ioallocateirp"></a>方案 11:使用 IoAllocateIrp 发送的异步请求

此方案中是类似于前面的方案中不同之处在于而不是调用[ **IoBuildAsynchronousFsdRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548310)，这种情况下使用[ **IoAllocateIrp**](https://msdn.microsoft.com/library/windows/hardware/ff548257)函数来创建 IRP。

```cpp
NTSTATUS
MakeAsynchronousRequest2(
    PDEVICE_OBJECT   TopOfDeviceStack,
    PVOID               WriteBuffer,
    ULONG               NumBytes
    )
/*++
Arguments:

    TopOfDeviceStack - 

    WriteBuffer       - Buffer to be sent to the TopOfDeviceStack.

    NumBytes  - Size of buffer to be sent to the TopOfDeviceStack.

--*/ 
{
    NTSTATUS        status;
    PIRP            irp;
    LARGE_INTEGER   startingOffset;
    KEVENT          event;
    PIO_STACK_LOCATION  nextStack;

    startingOffset.QuadPart = (LONGLONG) 0;

    // 
    // Start by allocating the IRP for this request.  Do not charge quota
    // to the current process for this IRP.
    // 

    irp = IoAllocateIrp( TopOfDeviceStack->StackSize, FALSE );
    if (NULL == irp) {

        return STATUS_INSUFFICIENT_RESOURCES;
    }

     // 
    // Obtain a pointer to the stack location of the first driver that will be
    // invoked.  This is where the function codes and the parameters are set.
    // 

    nextStack = IoGetNextIrpStackLocation( irp );
    nextStack->MajorFunction = IRP_MJ_WRITE;
    nextStack->Parameters.Write.Length = NumBytes;
    nextStack->Parameters.Write.ByteOffset= startingOffset;


    if(TopOfDeviceStack->Flags & DO_BUFFERED_IO) {

        irp->AssociatedIrp.SystemBuffer = WriteBuffer;
        irp->MdlAddress = NULL;

    } else if (TopOfDeviceStack->Flags & DO_DIRECT_IO) {
        // 
        // The target device supports direct I/O operations.  Allocate
        // an MDL large enough to map the buffer and lock the pages into
        // memory.
        // 
        irp->MdlAddress = IoAllocateMdl( WriteBuffer,
                                         NumBytes,
                                         FALSE,
                                         FALSE,
                                         (PIRP) NULL );
        if (irp->MdlAddress == NULL) {
            IoFreeIrp( irp );
            return STATUS_INSUFFICIENT_RESOURCES;
        }

        try {

            MmProbeAndLockPages( irp->MdlAddress,
                                 KernelMode,
                                 (LOCK_OPERATION) (nextStack->MajorFunction == IRP_MJ_WRITE ? IoReadAccess : IoWriteAccess) );

        } except(EXCEPTION_EXECUTE_HANDLER) {

              if (irp->MdlAddress != NULL) {
                  IoFreeMdl( irp->MdlAddress );
              }
              IoFreeIrp( irp );
              return  GetExceptionCode();

        }
    }   

    IoSetCompletionRoutine(irp,
                   MakeAsynchronousRequestCompletion2,
                   NULL,
                   TRUE,
                   TRUE,
                   TRUE);

    (void) IoCallDriver(TargetDeviceObject, irp);

    return STATUS_SUCCESS;
}

NTSTATUS
MakeAsynchronousRequestCompletion2(
    IN PDEVICE_OBJECT   DeviceObject,
    IN PIRP             Irp,
    IN PVOID            Context
    )
{
    PMDL mdl, nextMdl;

    // 
    // Free any associated MDL.
    // 

    if (Irp->MdlAddress != NULL) {
        for (mdl = Irp->MdlAddress; mdl != NULL; mdl = nextMdl) {
            nextMdl = mdl->Next;
            MmUnlockPages( mdl ); IoFreeMdl( mdl ); // This function will also unmap pages.
        }
        Irp->MdlAddress = NULL;
    }

    // 
    // If you intend to queue the IRP and reuse it for another request,
    // make sure you call IoReuseIrp(Irp, STATUS_SUCCESS) before you reuse.
    // 

    IoFreeIrp(Irp);

    return STATUS_MORE_PROCESSING_REQUIRED;
}
```

### <a name="scenario-12-send-an-asynchronous-request-and-cancel-it-in-a-different-thread"></a>方案 12:发送异步请求并在不同线程中取消 
此方案说明了如何发送一个请求一次到较低的驱动程序而无需等待请求完成，并且您可以随时从另一个线程取消请求。 

您可以记住 IRP 和其他变量来执行此操作在设备扩展或设备，如下所示的全局上下文结构中。 与设备扩展在 IRPLOCK 变量跟踪 IRP 的状态。 IrpEvent 用于确保 IRP 是完全完成 （或释放） 进行的下一个请求之前。 

在处理时，此事件也很有用[IRP_MN_REMOVE_DEVICE](irp-mn-remove-device.md)并[IRP_MN_STOP_DEVICE 即插即用](irp-mn-stop-device.md)需要确保在完成这些请求之前没有任何挂起的 Irp 的请求。 在初始化为同步事件 AddDevice 或某些其他初始化例程时，此事件的效果最佳。

```cpp
typedef struct _DEVICE_EXTENSION{
    ..
    PDEVICE_OBJECT TopOfDeviceStack;
    PIRP PendingIrp; 
    IRPLOCK IrpLock; // You need this to track the state of the IRP.
    KEVENT IrpEvent; // You need this to synchronize various threads.
    ..
} DEVICE_EXTENSION, *PDEVICE_EXTENSION;
                 </pre><pre class="code">
InitializeDeviceExtension( PDEVICE_EXTENSION  DeviceExtension)
{
    KeInitializeEvent(&DeviceExtension->IrpEvent, SynchronizationEvent, TRUE); 
}

NTSTATUS
MakeASynchronousRequest3(
    PDEVICE_EXTENSION  DeviceExtension,
    PVOID               WriteBuffer,
    ULONG               NumBytes
    )
/*++
Arguments:

    DeviceExtension - 

    WriteBuffer       - Buffer to be sent to the TargetDeviceObject.

    NumBytes  - Size of buffer to be sent to the TargetDeviceObject.

--*/ 
{
    NTSTATUS        status;
    PIRP            irp;
    LARGE_INTEGER   startingOffset;
    PIO_STACK_LOCATION  nextStack;

    // 
    // Wait on the event to make sure that PendingIrp
    // field is free to be used for the next request. If you do
    // call this function in the context of the user thread,
    // make sure to call KeEnterCriticialRegion before the wait to protect 
    // the thread from getting suspended while holding a lock.
    // 
    KeWaitForSingleObject( &DeviceExtension->IrpEvent,
                           Executive,
                           KernelMode,
                           FALSE,
                           NULL );

    startingOffset.QuadPart = (LONGLONG) 0;
    // 
    // If the IRP is used for the same purpose every time, you can just create the IRP in the
    // Initialization routine one time and reuse it by calling IoReuseIrp. 
    // The only thing that you have to do in the routines in this article 
    // is remove the lines that call IoFreeIrp and set the PendingIrp
    // field to NULL. If you do so, make sure that you free the IRP 
    // in the PNP remove handler.
    // 
    irp = IoBuildAsynchronousFsdRequest(
                IRP_MJ_WRITE,
                DeviceExtension->TopOfDeviceStack,
                WriteBuffer,
                NumBytes,
                &startingOffset, // Optional
                NULL
                ); 

    if (NULL == irp) {

        return STATUS_INSUFFICIENT_RESOURCES;
    }

    // 
    // Initialize the fields relevant fields in the DeviceExtension
    // 
    DeviceExtension->PendingIrp = irp;
    DeviceExtension->IrpLock = IRPLOCK_CANCELABLE;

    IoSetCompletionRoutine(irp,
                   MakeASynchronousRequestCompletion3,
                   DeviceExtension,
                   TRUE,
                   TRUE,
                   TRUE);
    // 
    // If you want to change any value in the IRP stack, you must
    // first obtain the stack location by calling IoGetNextIrpStackLocation.
    // This is the location that is initialized by the IoBuildxxx requests and  
    // is the one that the target device driver is going to view.
    // 

    nextStack = IoGetNextIrpStackLocation(irp);

    // 
    // You could change the MajorFunction code to something appropriate.
    // 
    nextStack->MajorFunction = IRP_MJ_SCSI;

    (void) IoCallDriver(DeviceExtension->TopOfDeviceStack, irp);

    return STATUS_SUCCESS;
}

NTSTATUS
MakeASynchronousRequestCompletion3(
    IN PDEVICE_OBJECT   DeviceObject,
    IN PIRP             Irp,
    IN PVOID            Context
    )
{
    PMDL mdl, nextMdl;
    PDEVICE_EXTENSION deviceExtension = Context;

    // 
    // If the target device object is set up to do buffered i/o 
    // (TargetDeviceObject->Flags & DO_BUFFERED_IO), then 
    // IoBuildAsynchronousFsdRequest request allocates a system buffer
    // for read and write operation. If you stop the completion of the IRP
    // here, you must free that buffer.
    // 

    if(Irp->AssociatedIrp.SystemBuffer && (Irp->Flags & IRP_DEALLOCATE_BUFFER) ) {
            ExFreePool(Irp->AssociatedIrp.SystemBuffer);
    }

    // 
    // If the target device object is set up to do direct i/o (DO_DIRECT_IO), then 
    // IoBuildAsynchronousFsdRequest creates an MDL to describe the buffer
    // and locks the pages. If you stop the completion of the IRP, you must unlock
    // the pages and free the MDL.
    // 

    if (Irp->MdlAddress != NULL) {
        for (mdl = Irp->MdlAddress; mdl != NULL; mdl = nextMdl) {
            nextMdl = mdl->Next;
            MmUnlockPages( mdl ); IoFreeMdl( mdl ); // This function will also unmap pages.
        }
        Irp->MdlAddress = NULL;
    }

    if (InterlockedExchange((PVOID)&deviceExtension->IrpLock, IRPLOCK_COMPLETED) 
                    == IRPLOCK_CANCEL_STARTED) {
        // 
        // Main line code has got the control of the IRP. It will
        // now take the responsibility of freeing the IRP. 
        // Therefore...
        return STATUS_MORE_PROCESSING_REQUIRED;
    }

    // 
    // If you intend to queue the IRP and reuse it for another request, make
    // sure you call IoReuseIrp(Irp, STATUS_SUCCESS) before you reuse.
    // 
    IoFreeIrp(Irp);
    deviceExtension->PendingIrp = NULL; // if freed
    // 
    // Signal the event so that the next thread in the waiting list
    // can send the next request.
    // 
    KeSetEvent (&deviceExtension->IrpEvent, IO_NO_INCREMENT, FALSE);

    return STATUS_MORE_PROCESSING_REQUIRED;
}

VOID
CancelPendingIrp(
    PDEVICE_EXTENSION DeviceExtension
    )
/*++
    This function tries to cancel the PendingIrp if it is not already completed.
    Note that the IRP may not be completed and freed when the
    function returns. Therefore, if you are calling this from your PNP Remove device handle,
    you must wait on the IrpEvent to make sure the IRP is indeed completed
    before successfully completing the remove request and allowing the driver to unload.
--*/ 
{ 
     if (InterlockedExchange((PVOID)&DeviceExtension->IrpLock, IRPLOCK_CANCEL_STARTED) == IRPLOCK_CANCELABLE) {

        // 
        // You got it to the IRP before it was completed. You can cancel
        // the IRP without fear of losing it, as the completion routine
        // will not let go of the IRP until you say so.
        // 
        IoCancelIrp(DeviceExtension->PendingIrp);
        // 
        // Release the completion routine. If it already got there,
        // then you need to free it yourself. Otherwise, you got
        // through IoCancelIrp before the IRP completed entirely.
        // 
        if (InterlockedExchange((PVOID)&DeviceExtension->IrpLock, IRPLOCK_CANCEL_COMPLETE) == IRPLOCK_COMPLETED) {
            IoFreeIrp(DeviceExtension->PendingIrp);
            DeviceExtension->PendingIrp = NULL;
            KeSetEvent(&DeviceExtension->IrpEvent, IO_NO_INCREMENT, FALSE);
        }

     }

    return ;
}
```

## <a name="references"></a>参考 
* Walter Oney。 Windows 驱动程序模型，第二个版本，第 5 章编程。

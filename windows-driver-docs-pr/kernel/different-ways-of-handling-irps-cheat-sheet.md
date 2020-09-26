---
title: 不同的 IRP 处理方法 - 速查表
description: 处理 Irp 的不同方法
keywords:
- Irp WDK 内核，处理 Irp
ms.date: 12/07/2017
ms.localizationpriority: medium
ms.openlocfilehash: f63a9e86105e7eee294f3fd68e344f77853e71f8
ms.sourcegitcommit: ee3e2259aafc844cc43cce62299a72649cf89212
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2020
ms.locfileid: "91353636"
---
# <a name="different-ways-of-handling-irps---cheat-sheet"></a>不同的 IRP 处理方法 - 速查表 

Windows 驱动模型 (WDM) 驱动程序通常会将 () Irp 的输入/输出请求数据包发送到其他驱动程序。 驱动程序创建自己的 IRP，并将其发送到较低的驱动程序，或驱动程序将从上面附加的其他驱动程序接收的 Irp 转发到该驱动程序。 

本文讨论了驱动程序可以将 Irp 发送到较低的驱动程序的不同方式，并包括带批注的示例代码。

* 方案1-5 介绍了如何从调度例程将 IRP 转发到较低版本的驱动程序。
* 方案6-12 讨论创建 IRP 并将其发送到另一个驱动程序的不同方式。

在检查各种方案之前，请注意，IRP 完成例程可以返回 STATUS_MORE_PROCESSING_REQUIRED 或 STATUS_SUCCESS。

在检查状态时，i/o 管理器使用以下规则：

* 如果状态为 "STATUS_MORE_PROCESSING_REQUIRED"，则停止完成 IRP，使堆栈位置保持不变并返回。
* 如果状态不是 STATUS_MORE_PROCESSING_REQUIRED，请继续向上完成 IRP。

因为 i/o 管理器不必知道使用的是哪个非 STATUS_MORE_PROCESSING_REQUIRED 值，所以请使用 STATUS_SUCCESS (，因为值0会在大多数处理器体系结构) 上高效加载。

阅读以下代码时，请注意，STATUS_CONTINUE_COMPLETION 已化名为 WDK 中 STATUS_SUCCESS。

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

## <a name="forwarding-an-irp-to-another-driver"></a>将 IRP 转发到另一个驱动程序

### <a name="scenario-1-forward-and-forget"></a>方案1：转发和遗忘
如果驱动程序只是想要向下转发 IRP 并且不执行其他操作，请使用以下代码。 在这种情况下，驱动程序不必设置完成例程。 如果该驱动程序是顶级驱动程序，则可以同步或异步完成 IRP，这取决于由低级驱动程序返回的状态。 

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

### <a name="scenario-2-forward-and-wait"></a>方案2：前进并等待

如果驱动程序要将 IRP 转发到较低的驱动程序并等待其返回以使其能够处理 IRP，请使用以下代码。 这通常在处理 PNP Irp 时完成。 例如，当你收到 [IRP_MN_START_DEVICE](irp-mn-start-device.md) IRP 时，必须将 irp 转发到总线驱动程序并等待其完成，然后才能启动设备。 可以调用 [**IoForwardIrpSynchronously**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioforwardirpsynchronously) 轻松完成此操作。

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

### <a name="scenario-3-forward-with-a-completion-routine"></a>方案3：使用完成例程前进

在这种情况下，驱动程序将设置一个完成例程，将 IRP 向下转发，然后按原样返回较低驱动程序的状态。 设置完成例程的目的是在后台修改 IRP 的内容。 

```cpp
NTSTATUS
DispatchRoutine_3(
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

如果从调度例程返回低级驱动程序的状态：

* 不能在完成例程中更改 IRP 的状态。 这是为了确保 IRP 的 IoStatus 块中设置的状态值 (Irp->IoStatus) 与较低驱动程序的返回状态一致。
* 必须按照 Irp >PendingReturned 中所示传播 IRP 的挂起状态。
* 不得更改 IRP 的 synchronicity。

因此，在此方案中，只有2个有效版本的完成例程 (31 和 32) ：

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

### <a name="scenario-4-queue-for-later-or-forward-and-reuse"></a>方案4：排队供以后使用或转发和重复使用

如果驱动程序要将 IRP 排队并稍后处理 IRP，或将 IRP 转发到较低的驱动程序，并在完成 IRP 之前将其重复用于特定次数，请使用以下代码片段。 调度例程会将 IRP 标记为挂起并返回 STATUS_PENDING，因为 IRP 稍后将在另一个线程中完成。 在此处，完成例程可以更改 IRP 的状态（如有必要）， (与前面的方案) 不同。 

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

完成例程可以返回 STATUS_CONTINUE_COMPLETION 或 STATUS_MORE_PROCESSING_REQUIRED。 仅当你想要从另一个线程重用 IRP 并在以后完成时，才返回 STATUS_MORE_PROCESSING_REQUIRED。

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

### <a name="scenario-5-complete-the-irp-in-the-dispatch-routine"></a>方案5：在调度例程中完成 IRP

此方案说明如何在调度例程中完成 IRP。 

**重要提示** 在调度例程中完成 IRP 后，调度例程的返回状态应与 IRP (Irp->IoStatus) 的 IoStatus 块中设置的值的状态相匹配。

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

## <a name="creating-irps-and-sending-them-to-another-driver"></a>创建 Irp 并将其发送到另一个驱动程序

### <a name="introduction"></a>简介

在检查方案之前，必须了解驱动程序创建的同步输入/输出请求数据包 (IRP) 和异步请求之间的差异。 

|    同步 (线程) IRP                                                                                                                        |    异步 (非线程) IRP                                                                                                                       |
|--------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    使用 IoBuildSynchronousFsdRequest 或 IoBuildDeviceIoControlRequest 创建。                                                                  |    使用 IoBuildAsynchronousFsdRequest 或 IoAllocateIrp 创建。 这适用于驱动程序到驱动程序的通信。                                 |
|    线程必须等待 IRP 完成。                                                                                                         |    线程不必等待 IRP 完成。                                                                                                 |
|    与创建它的线程关联，因此是线程 Irp 的名称。 因此，如果线程退出，i/o 管理器将取消 IRP。     |    不与创建它的线程关联。                                                                                                       |
|    不能在任意线程上下文中创建。                                                                                                 |    可在任意线程上下文中创建，因为该线程不会等待 IRP 完成。                                             |
|    I/o 管理器执行 post 完成，以释放与 IRP 关联的缓冲区。                                                     |    I/o 管理器无法执行清除操作。 驱动程序必须提供完成例程，并释放与 IRP 关联的缓冲区。          |
|    必须以 IRQL 级别发送到 PASSIVE_LEVEL。                                                                                                |    如果目标驱动程序的调度例程可以在 DISPATCH_LEVEL 处理请求，则可以在 IRQL 小于或等于 DISPATCH_LEVEL。     |

### <a name="scenario-6-send-a-synchronous-device-control-request-irp_mj_internal_device_controlirp_mj_device_control-by-using-iobuilddeviceiocontrolrequest"></a>方案6：通过使用 IoBuildDeviceIoControlRequest 发送同步设备控制请求 (IRP_MJ_INTERNAL_DEVICE_CONTROL/IRP_MJ_DEVICE_CONTROL) 

下面的代码演示如何调用 [**IoBuildDeviceIoControlRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest) 请求以发出同步 IOCTL 请求。  有关详细信息，请参阅 [IRP_MJ_INTERNAL_DEVICE_CONTROL](irp-mj-internal-device-control.md) 和 [IRP_MJ_DEVICE_CONTROL](irp-mj-device-control.md)。

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

### <a name="scenario-7-send-a-synchronous-device-control-ioctl-request-and-cancel-it-if-not-completed-in-a-certain-time-period"></a>方案7：发送同步设备控制 (IOCTL) 请求，如果在某个时间段内未完成，则将其取消 
此方案类似于前面的方案，只不过它会等待一些用户指定的时间，并在等待超时的情况下安全取消 IOCTL 请求。 

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

### <a name="scenario-8-send-a-synchronous-non-ioctl-request-by-using-iobuildsynchronousfsdrequest---completion-routine-returns-status_continue_completion"></a>方案8：通过使用 IoBuildSynchronousFsdRequest 例程发送同步非 IOCTL 请求返回 STATUS_CONTINUE_COMPLETION
下面的代码演示如何通过调用 [**IoBuildSynchronousFsdRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildsynchronousfsdrequest)来执行同步非 IOCTL 请求。 此处所示的方法类似于方案6。

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

### <a name="scenario-9-send-a-synchronous-non-ioctl-request-by-using-iobuildsynchronousfsdrequest---completion-routine-returns-status_more_processing_required"></a>方案9：使用 IoBuildSynchronousFsdRequest 例程发送同步非 IOCTL 请求返回 STATUS_MORE_PROCESSING_REQUIRED 
此方案与方案8之间唯一的区别是完成例程返回 STATUS_MORE_PROCESSING_REQUIRED。 

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

### <a name="scenario-10-send-an-asynchronous-request-by-using-iobuildasynchronousfsdrequest"></a>方案10：使用 IoBuildAsynchronousFsdRequest 发送异步请求 
此方案说明如何通过调用 [**IoBuildAsynchronousFsdRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildasynchronousfsdrequest)进行异步请求。 

在异步请求中，发出请求的线程不必等待 IRP 完成。 可以在任意线程上下文中创建 IRP，因为 IRP 不与线程关联。 如果不打算重用 IRP，则必须提供完成例程并在完成例程中释放缓冲区和 IRP。 这是因为，i/o 管理器无法完成通过 **IoBuildAsynchronousFsdRequest** 和 **IoAllocateIrp**) 创建的驱动程序创建的异步 (irp 的完成后清理。 

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

### <a name="scenario-11-send-an-asynchronous-request-by-using-ioallocateirp"></a>方案11：使用 IoAllocateIrp 发送异步请求

此方案类似于前述 [**方案，只不过**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildasynchronousfsdrequest)此方案使用 [**IoAllocateIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp) 函数来创建 IRP。

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

### <a name="scenario-12-send-an-asynchronous-request-and-cancel-it-in-a-different-thread"></a>方案12：发送异步请求并在另一个线程中取消它 
此方案说明了如何一次将一个请求发送到较低的驱动程序，而无需等待请求完成，还可以随时从另一个线程取消请求。 

在设备扩展或全局到设备的上下文结构中，可以记住 IRP 和其他变量，如下所示。 使用设备扩展中的 IRPLOCK 变量跟踪 IRP 的状态。 IrpEvent 用于确保在进行下一个请求之前) 完全完成 IRP (或释放。 

当你处理 [IRP_MN_REMOVE_DEVICE](irp-mn-remove-device.md) 和 [IRP_MN_STOP_DEVICE PNP](irp-mn-stop-device.md) 请求时，如果必须确保在完成这些请求之前没有任何挂起的 irp，此事件也很有用。 当你在 AddDevice 中或在其他某个初始化例程中将其作为同步事件进行初始化时，此事件的效果最佳。

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
* Walter Oney。 编程 Windows 驱动模型，第5版，第5章。
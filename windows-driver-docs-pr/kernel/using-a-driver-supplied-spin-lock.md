---
title: 使用驱动程序提供的自旋锁
description: 使用驱动程序提供的自旋锁
ms.assetid: e81d5c93-47d6-407c-80a2-b2d55f9eb717
keywords:
- 数值调节钮锁 WDK 内核
- 驱动程序所提供的自旋锁 WDK 内核
- 全局取消自旋锁 WDK 内核
ms.date: 05/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 226e3c6245b2a337167b1fc36ab8cc0fc16298ac
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383718"
---
# <a name="using-a-driver-supplied-spin-lock"></a>使用驱动程序提供的自旋锁





管理他们自己队列 Irp 的驱动程序可以使用驱动程序所提供的旋转锁，而不是系统取消自旋锁来同步对队列的访问。 可以通过在绝对必要时避免使用除取消自旋锁来提高性能。 由于系统只有一个取消自旋锁，驱动程序有时可能需要等待该数值调节钮锁变为可用。 使用驱动程序所提供的旋转锁可消除此潜在延迟并使取消自旋锁对 I/O 管理器和其他驱动程序。 尽管系统仍获取取消自旋锁时调用的驱动程序[*取消*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_cancel)例程，驱动程序可以使用其自己的自旋锁来保护 Irp 其队列。

即使驱动程序不会挂起的 Irp，排队，但保留以某种其他方式的所有权，必须设置该驱动程序*取消*例程的 IRP 和必须使用旋转锁来保护 IRP 指针。 例如，假设一个驱动程序将标记 IRP 挂起状态，然后将 IRP 指针传递到上下文作为[ *IoTimer* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_timer_routine)例程。 该驱动程序必须设置*取消*取消计时器，并且必须在这种使用相同的旋转锁的例程*取消*例程和计时器回调时访问 IRP。

排队自己 Irp，并使用其自己的自旋锁的任何驱动程序必须执行以下操作：

-   创建使用数值调节钮锁来保证队列。

-   设置和清除*取消*例程只能同时保留此数值调节钮锁定。

-   如果*取消*例程将开始运行时，驱动程序取消排队 IRP，允许*取消*例程，以完成 IRP。

-   获取的锁的保护中的队列*取消*例程。

若要创建旋转锁，驱动程序调用[ **KeInitializeSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinitializespinlock)。 在以下示例中，该驱动程序将保存在旋转锁**设备\_上下文**结构以及已创建的队列：

```cpp
typedef struct {
    LIST_ENTRYirpQueue;
    KSPIN_LOCK irpQueueSpinLock;
    ...
} DEVICE_CONTEXT;

VOID InitDeviceContext(DEVICE_CONTEXT *deviceContext)
{
    InitializeListHead(&deviceContext->irpQueue);
    KeInitializeSpinLock(&deviceContext->irpQueueSpinLock);
}
```

若要进行排队 IRP，驱动程序将获取数值调节钮锁，调用[ **InsertTailList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-inserttaillist)，然后将标记 IRP 挂起状态，如以下示例所示：

```cpp
NTSTATUS QueueIrp(DEVICE_CONTEXT *deviceContext, PIRP Irp)
{
   PDRIVER_CANCEL  oldCancelRoutine;
   KIRQL  oldIrql;
   NTSTATUS  status;

   KeAcquireSpinLock(&deviceContext->irpQueueSpinLock, &oldIrql);

   // Queue the IRP and call IoMarkIrpPending to indicate
   // that the IRP may complete on a different thread.
   // N.B. It is okay to call these inside the spin lock
   // because they are macros, not functions.
   IoMarkIrpPending(Irp);
   InsertTailList(&deviceContext->irpQueue, &Irp->Tail.Overlay.ListEntry);

   // Must set a Cancel routine before checking the Cancel flag.
   oldCancelRoutine = IoSetCancelRoutine(Irp, IrpCancelRoutine);
   ASSERT(oldCancelRoutine == NULL);

   if (Irp->Cancel) {
      // The IRP was canceled. Check whether our cancel routine was called.
      oldCancelRoutine = IoSetCancelRoutine(Irp, NULL);
      if (oldCancelRoutine) {
         // The cancel routine was NOT called.  
         // So dequeue the IRP now and complete it after releasing the spin lock.
         RemoveEntryList(&Irp->Tail.Overlay.ListEntry);
         // Drop the lock before completing the request.
         KeReleaseSpinLock(&deviceContext->irpQueueSpinLock, oldIrql);
         Irp->IoStatus.Status = STATUS_CANCELLED; 
         Irp->IoStatus.Information = 0;
         IoCompleteRequest(Irp, IO_NO_INCREMENT);
         return STATUS_PENDING;

      } else {
         // The Cancel routine WAS called.  
         // As soon as we drop our spin lock, it will dequeue and complete the IRP.
         // So leave the IRP in the queue and otherwise do not touch it.
         // Return pending since we are not completing the IRP here.
         
      }
   }

   KeReleaseSpinLock(&deviceContext->irpQueueSpinLock, oldIrql);

   // Because the driver called IoMarkIrpPending while it held the IRP,
   // it must return STATUS_PENDING from its dispatch routine.
   return STATUS_PENDING;
}
```

如示例所示，该驱动程序保存其旋转锁时它设置并清除*取消*例程。 该示例队列例程包含两次调用[ **IoSetCancelRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcancelroutine)。

第一个调用集*取消*IRP 的例程。 但是，由于队列例程运行时，IRP 可能已取消，驱动程序必须检查**取消**IRP 的成员。

-   如果**取消**设置，已请求取消，并驱动程序必须使第二个调用**IoSetCancelRoutine**若要查看是否以前设置*取消*调用例程。

-   如果已取消 IRP，但*取消*尚未调用例程，则当前例程 IRP 中取消排队并完成后，它与状态\_已取消。

-   如果已取消 IRP 和*取消*已调用例程，则当前返回将挂起的 IRP 标记，并返回状态\_PENDING。 *取消*例程将完成 IRP。

下面的示例演示如何从以前创建的队列中删除 IRP:

```cpp
PIRP DequeueIrp(DEVICE_CONTEXT *deviceContext)
{
   KIRQL oldIrql;
   PIRP nextIrp = NULL;

   KeAcquireSpinLock(&deviceContext->irpQueueSpinLock, &oldIrql);

   while (!nextIrp && !IsListEmpty(&deviceContext->irpQueue)) {
      PDRIVER_CANCEL oldCancelRoutine;
      PLIST_ENTRY listEntry = RemoveHeadList(&deviceContext->irpQueue);

      // Get the next IRP off the queue.
      nextIrp = CONTAINING_RECORD(listEntry, IRP, Tail.Overlay.ListEntry);

      // Clear the IRP's cancel routine.
      oldCancelRoutine = IoSetCancelRoutine(nextIrp, NULL);

      // IoCancelIrp() could have just been called on this IRP. What interests us
      // is not whether IoCancelIrp() was called (nextIrp->Cancel flag set), but
      // whether IoCancelIrp() called (or is about to call) our Cancel routine.
      // For that, check the result of the test-and-set macro IoSetCancelRoutine.
      if (oldCancelRoutine) {
         // Cancel routine not called for this IRP. Return this IRP.
         ASSERT(oldCancelRoutine == IrpCancelRoutine);
      } else {
         // This IRP was just canceled and the cancel routine was (or will be)
         // called. The Cancel routine will complete this IRP as soon as we
         // drop the spin lock, so do not do anything with the IRP.
         // Also, the Cancel routine will try to dequeue the IRP, so make 
         // the IRP's ListEntry point to itself.
         ASSERT(nextIrp->Cancel);
         InitializeListHead(&nextIrp->Tail.Overlay.ListEntry);
         nextIrp = NULL;
      }
   }

   KeReleaseSpinLock(&deviceContext->irpQueueSpinLock, oldIrql);

   return nextIrp;
}
```

在示例中，该驱动程序获取关联的数值调节钮锁，然后才能访问队列。 同时保留数值调节钮锁定，它会检查该队列不为空，并获取下一步从队列 IRP。 然后，调用**IoSetCancelRoutine**重置*取消*IRP 的例程。 因为该驱动程序取消排队 IRP 和重置时，无法取消 IRP*取消*例程，该驱动程序必须检查返回的值**IoSetCancelRoutine**。 如果**IoSetCancelRoutine**返回**NULL**，这指示*取消*例程已经或很快就将调用，然后取消排队的例程允许*取消*例程完成 IRP。 它然后释放锁，可以在队列，并返回。

请注意，使用[ **InitializeListHead** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-initializelisthead)前面例程中。 驱动程序无法将 IRP，重新排队，以便*取消*例程可以取消排队，但以调用会更简单**InitializeListHead**，这会重新初始化 IRP **ListEntry**使其指向 IRP 本身的字段。 使用自引用的指针很重要，因为列表的结构可能会更改之前*取消*例程获取自旋锁。 如果列表结构发生更改，可能生成的原始值和**ListEntry**无效，*取消*例程可能会损坏列表时取消排队 IRP。 但是，如果**ListEntry** IRP 本身，到点则*取消*例程将始终使用正确的 IRP。

*取消*例程，反过来，只需执行以下：

```cpp
VOID IrpCancelRoutine(IN PDEVICE_OBJECT DeviceObject, IN PIRP Irp)
{
   DEVICE_CONTEXT  *deviceContext = DeviceObject->DeviceExtension;
   KIRQL  oldIrql;

   // Release the global cancel spin lock.  
   // Do this while not holding any other spin locks so that we exit at the right IRQL.
   IoReleaseCancelSpinLock(Irp->CancelIrql);

   // Dequeue and complete the IRP.  
   // The enqueue and dequeue functions synchronize properly so that if this cancel routine is called, 
   // the dequeue is safe and only the cancel routine will complete the IRP. Hold the spin lock for the IRP
   // queue while we do this.

   KeAcquireSpinLock(&deviceContext->irpQueueSpinLock, &oldIrql);

   RemoveEntryList(&Irp->Tail.Overlay.ListEntry);

   KeReleaseSpinLock(&deviceContext->irpQueueSpinLock, oldIrql);

   // Complete the IRP. This is a call outside the driver, so all spin locks must be released by this point.
   Irp->IoStatus.Status = STATUS_CANCELLED;
   IoCompleteRequest(Irp, IO_NO_INCREMENT);
   return;
}
```

I/O 管理器之前它将调用始终获取全局取消自旋锁*取消*例程，因此第一个任务*取消*例程是释放此自旋锁。 然后，它获取的自旋锁的保护的 Irp 的驱动程序的队列、 从队列中移除当前 IRP，释放其自旋锁、 完成状态 IRP\_已取消以及没有优先级提升选项，并返回。

有关取消自旋锁的详细信息，请参阅[Windows 驱动程序中的取消逻辑](https://go.microsoft.com/fwlink/p/?linkid=59531)白皮书。

 

 





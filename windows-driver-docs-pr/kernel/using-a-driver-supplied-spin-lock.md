---
title: 使用驱动程序提供的自旋锁
description: 使用驱动程序提供的自旋锁
ms.assetid: e81d5c93-47d6-407c-80a2-b2d55f9eb717
keywords:
- 旋转锁定 WDK 内核
- 驱动程序提供的旋转锁定 WDK 内核
- 全局取消旋转锁定 WDK 内核
ms.date: 05/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: edad6fc43e8e98327821bd0a51ac42f0766a5555
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91733478"
---
# <a name="using-a-driver-supplied-spin-lock"></a>使用驱动程序提供的自旋锁





管理自己的 Irp 队列的驱动程序可以使用驱动程序提供的自旋锁，而不是系统取消旋转锁来同步对队列的访问。 除了绝对必要时，还可以通过避免使用取消旋转锁定来提高性能。 因为系统只有一个 cancel 自旋锁，所以驱动程序有时必须等待该旋转锁定变为可用。 使用驱动程序提供的旋转锁定可消除这种潜在延迟，并使 i/o 管理器和其他驱动程序可以使用取消旋转锁定。 尽管系统在调用驱动程序的 [*取消*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel) 例程时仍获取 cancel 自旋锁，但驱动程序可以使用自己的自旋锁来保护其 irp 队列。

即使驱动程序未将挂起的 Irp 排队，但以其他方式保留所有权，该驱动程序也必须为 IRP 设置 " *取消* " 例程，并且必须使用旋转锁来保护 irp 指针。 例如，假设驱动程序将 IRP 标记为 "正在挂起"，然后将 IRP 指针作为上下文传递到 [*IoTimer*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_timer_routine) 例程。 驱动程序必须设置 *取消* 计时器，并在访问 IRP 时必须在 *cancel* 例程和计时器回调中使用相同的自旋锁。

任何对其自身的 Irp 进行排队并使用其自己的自旋锁的驱动程序都必须执行以下操作：

-   创建旋转锁来保护队列。

-   仅在持有此旋转锁时设置并清除 *取消* 例程。

-   如果当驱动程序出列 IRP 时 *取消* 例程开始运行，则允许 *取消* 例程完成 irp。

-   获取在 *取消* 例程中保护队列的锁。

若要创建旋转锁定，驱动程序将调用 [**KeInitializeSpinLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializespinlock)。 在下面的示例中，驱动程序将旋转锁连同它所创建的队列一起保存在 **设备 \_ 上下文** 结构中：

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

若要将 IRP 排队，驱动程序将获取自旋锁，调用 [**InsertTailList**](/windows-hardware/drivers/ddi/wdm/nf-wdm-inserttaillist)，然后将 IRP 标记为 "挂起"，如以下示例中所示：

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

如示例所示，驱动程序在设置并清除 *取消* 例程时保留其旋转锁。 示例队列例程包含对 [**IoSetCancelRoutine**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcancelroutine)的两次调用。

第一次调用设置 IRP 的 *取消* 例程。 但是，因为在队列例程运行时 IRP 可能已被取消，所以驱动程序必须检查 IRP 的 **Cancel** 成员。

-   如果设置了 **取消** ，则请求取消，并且驱动程序必须对 **IoSetCancelRoutine** 进行第二次调用，以查看是否调用了以前设置的 *取消* 例程。

-   如果 IRP 已被取消，但尚未调用 *取消* 例程，则当前例程取消排队 IRP 并完成，并已 \_ 取消状态。

-   如果已取消 IRP 并且已经调用了 *Cancel* 例程，则当前返回的会将 irp 标记为 "挂起" 并返回 " \_ 挂起" 状态。 *取消*例程将完成 IRP。

下面的示例演示如何从以前创建的队列中删除 IRP：

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

在此示例中，驱动程序在访问队列之前获取关联的自旋锁。 在持有自旋锁时，它会检查队列是否不为空，并从队列中获取下一个 IRP。 然后，它会调用 **IoSetCancelRoutine** 来重置 IRP 的 *取消* 例程。 由于可以在驱动程序取消排队 IRP 并重置 *取消* 例程时取消 irp，因此驱动程序必须检查 **IoSetCancelRoutine**返回的值。 如果 **IoSetCancelRoutine** 返回 **NULL**，表示 *取消* 例程已或即将被调用，则出列例程会使 *取消* 例程完成 IRP。 然后，它会释放保护队列并返回的锁。

请注意，在前面的例程中使用 [**InitializeListHead**](/windows-hardware/drivers/ddi/wdm/nf-wdm-initializelisthead) 。 驱动程序可以重新排队 IRP，以便取消操作可以将其 *取消* 排队，但调用 **InitializeListHead**更简单，后者会重新初始化 IRP 的 **ListEntry** 字段，使其指向 IRP 本身。 使用自引用指针非常重要，因为在 *取消* 例程获取旋转锁之前，列表的结构可能会更改。 如果列表结构发生更改，可能会使 **ListEntry** 的原始值无效，则 *取消* 例程在取消排队 IRP 时可能会损坏列表。 但如果 **ListEntry** 指向 IRP 本身，则 *Cancel* 例程将始终使用正确的 IRP。

而 *取消* 例程则只需执行以下操作：

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

在调用 *取消* 例程之前，i/o 管理器始终获取全局取消旋转锁，因此 *取消* 例程的第一个任务是释放此自旋锁。 然后，它获取保护该驱动程序的 Irp 队列的自旋锁，从队列中删除当前 IRP，释放其旋转锁定，完成已取消状态的 IRP \_ 并且不提升优先级，然后返回。

有关取消旋转锁定的详细信息，请参阅 [Windows 驱动程序中的取消逻辑](/previous-versions/windows/hardware/design/dn653289(v=vs.85)) 白皮书。


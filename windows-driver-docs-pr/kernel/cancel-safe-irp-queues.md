---
title: 可安全取消的 IRP 队列
description: 可安全取消的 IRP 队列
ms.assetid: a759d1e0-120f-4db9-9b84-ff921f2f5ba4
keywords:
- 取消安全 IRP 队列 WDK 内核
- 回调例程 WDK Irp
- 同步 WDK Irp
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 969df87a951b968bdab7c13712275e3786347f2c
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188649"
---
# <a name="cancel-safe-irp-queues"></a>可安全取消的 IRP 队列





实现自己的 IRP 队列的驱动程序应使用 *取消安全 irp 队列* 框架。 取消安全 IRP 队列将 IRP 处理拆分为两个部分：

1. 驱动程序提供一组回调例程，用于实现对驱动程序的 IRP 队列的标准操作。 提供的操作包括插入和删除队列中的 Irp 以及锁定和解锁队列。 请参阅 [实现取消安全 IRP 队列](#ddk-implementing-the-cancel-safe-irp-queue-kg)。

2. 只要驱动程序需要从队列中实际插入或删除 IRP，就会使用系统提供的 **IoCsq * Xxx*** 例程。 这些例程处理驱动程序的所有同步和 IRP 取消逻辑。

使用 "取消安全 IRP 队列" 的驱动程序不会实现 [*取消*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel) 例程来支持 IRP 取消。

该框架可确保驱动程序以原子方式从队列中插入和删除 Irp。 它还确保 IRP 取消正确实现。 不使用框架的驱动程序必须先手动锁定并解锁队列，然后再执行任何插入和删除操作。 它们还必须避免在实现 *取消* 例程时可能导致的争用情况。  (有关可能出现的争用条件的说明，请参阅 [同步 IRP 取消](synchronizing-irp-cancellation.md)。 ) 

Windows XP 和更高版本的 Windows 中包含了 "取消安全 IRP 队列框架"。 还必须与 Windows 2000 和 Windows 98/Me 一起使用的驱动程序可以链接到 Windows 驱动程序工具包 (WDK) 中包含的 Csq 库。 Csq 库提供了此框架的实现。

**IoCsq * Xxx*** 例程是在 Windows XP 和更高版本的 Wdm 和 Ntddk 中声明的。 还必须与 Windows 2000 和 Windows 98/Me 一起使用的驱动程序必须在声明中包括 Csq。

可以在 WDK 的 src 常规 "取消" 目录中查看有关如何使用 "取消安全 IRP 队列" 的完整演示 \\ \\ \\ 。 有关这些队列的详细信息，另请参阅 " [取消安全 IRP 队列](https://go.microsoft.com/fwlink/p/?linkid=57844) " 白皮书的控制流。

### <a name="implementing-the-cancel-safe-irp-queue"></a><a href="" id="ddk-implementing-the-cancel-safe-irp-queue-kg"></a>实现取消安全 IRP 队列

若要实现取消安全 IRP 队列，驱动程序必须提供以下例程：

-   将 Irp 插入队列中的以下例程之一： [*CsqInsertIrp*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_csq_insert_irp) 或 [*CsqInsertIrpEx*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_csq_insert_irp_ex)。 *CsqInsertIrpEx* 是 *CsqInsertIrp*的扩展版本;使用一种来实现队列。

-   从队列中删除指定 IRP 的 [*CsqRemoveIrp*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_csq_remove_irp) 例程。

-   [*CsqPeekNextIrp*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_csq_peek_next_irp)例程，返回指向队列中指定 irp 之后的下一个 IRP 的指针。 这是指系统将从[**IoCsqRemoveNextIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqremovenextirp)接收的*PeekContext*值传递到的位置。 驱动程序可以通过任何方式解释此值。

-   以下两个例程都允许系统锁定和解锁 IRP 队列： [*CsqAcquireLock*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_csq_acquire_lock) 和 [*CsqReleaseLock*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_csq_release_lock)。

-   [*CsqCompleteCanceledIrp*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_csq_complete_canceled_irp)例程，用于完成已取消的 IRP。

指向驱动程序例程的指针存储在描述队列的 [**IO \_ CSQ**](./eprocess.md) 结构中。 驱动程序为 **IO \_ CSQ** 结构分配存储空间。 确保 **IO \_ CSQ** 结构保持固定大小，以便驱动程序能够安全地将结构嵌入其设备扩展中。

驱动程序使用 [**IoCsqInitialize**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqinitialize) 或 [**IoCsqInitializeEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqinitializeex) 来初始化结构。 如果队列实现[*CsqInsertIrp*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_csq_insert_irp)，则使用**IoCsqInitialize** ; 如果队列实现*CsqInsertIrpEx*，则使用**IoCsqInitializeEx** 。

驱动程序只需在每个回调例程中提供基本功能。 例如，只有 *CsqAcquireLock* 和 *CsqReleaseLock* 例程实现锁处理。 系统会根据需要自动调用这些例程来锁定和解锁队列。

只要提供了适当的调度例程，你就可以在驱动程序中实现任何类型的 IRP 排队机制。 例如，驱动程序可以将队列实现为链接列表，或将其作为优先级队列实现。

与[*CsqInsertIrp*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_csq_insert_irp)相比， [*CsqInsertIrpEx*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_csq_insert_irp_ex)提供了更灵活的队列接口。 驱动程序可以使用其返回值来指示操作的结果;如果它返回错误代码，则插入失败。 *CsqInsertIrp*例程不返回值，因此不能通过简单的方法来指示插入操作失败。 另外， *CsqInsertIrpEx* 还需要一个附加的驱动程序定义的 *InsertContext* 参数，该参数可用于指定队列实现使用的其他特定于驱动程序的信息。

驱动程序可以使用 *CsqInsertIrpEx* 来实现更复杂的 IRP 处理。 例如，如果没有挂起的 Irp， *CsqInsertIrpEx* 例程可能会返回错误代码，驱动程序可以立即处理 irp。 同样，如果不能再对 Irp 排队， *CsqInsertIrpEx* 可能会返回错误代码来指示这一事实。

该驱动程序与所有 IRP 取消处理分开。 系统为队列中的 Irp 提供 [*取消*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel) 例程。 此例程调用 [*CsqRemoveIrp*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_csq_remove_irp) ，以从队列中删除 IRP，并调用 [*CSQCOMPLETECANCELEDIRP*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_csq_complete_canceled_irp) 来完成 irp 取消。

下图演示了 IRP 取消的控制流。

![说明 irp 取消控制流的示意图](images/5cancelingirp.png)

[*CsqCompleteCanceledIrp*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_csq_complete_canceled_irp)的基本实现如下所示。

```cpp
VOID CsqCompleteCanceledIrp(PIO_CSQ Csq, PIRP Irp) {
  Irp->IoStatus.Status = STATUS_CANCELLED;
  Irp->IoStatus.Information = 0;

  IoCompleteRequest(Irp, IO_NO_INCREMENT);
}
```

驱动程序可以使用任何操作系统的同步基元来实现其 [*CsqAcquireLock*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_csq_acquire_lock) 和 [*CsqReleaseLock*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_csq_release_lock) 例程。 可用的同步基元包括 [自旋锁](./introduction-to-spin-locks.md) 和 [互斥体对象](mutex-objects.md)。

下面的示例演示了驱动程序如何使用自旋锁实现锁定。

```cpp
/* 
  The driver has previously initialized the SpinLock variable with
  KeInitializeSpinLock.
 */

VOID CsqAcquireLock(PIO_CSQ IoCsq, PKIRQL PIrql)
{
    KeAcquireSpinLock(SpinLock, PIrql);
}

VOID CsqReleaseLock(PIO_CSQ IoCsq, KIRQL Irql)
{
    KeReleaseSpinLock(SpinLock, Irql);
}
```

系统向 *CsqAcquireLock* 和 *CSQRELEASELOCK*传递指向 IRQL 变量的指针。 如果驱动程序使用自旋锁来实现队列的锁定，则该驱动程序可以使用此变量来存储当前的 IRQL，同时锁定队列。

驱动程序无需使用自旋锁。 例如，驱动程序可以使用 mutex 锁定队列。 有关对驱动程序可用的同步技术的说明，请参阅 [同步技术](synchronization-techniques.md)。

### <a name="using-the-cancel-safe-irp-queue"></a><a href="" id="ddk-using-the-cancel-safe-irp-queue-kg"></a>使用取消安全 IRP 队列

在对 Irp 进行排队和出列时，驱动程序使用以下系统例程：

-   以下任意一项操作可将 IRP 插入队列： [**IoCsqInsertIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqinsertirp) 或 [**IoCsqInsertIrpEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqinsertirpex)。

-   [**IoCsqRemoveNextIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqremovenextirp) 删除队列中的下一个 IRP。 驱动程序可以选择指定密钥值。

下图说明了 [**IoCsqRemoveNextIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqremovenextirp)的控制流。

![说明 iocsqremovenextirp 控制流的示意图](images/4iocsqremovenextirp.png)

-   [**IoCsqRemoveIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqremoveirp) 从队列中删除指定的 IRP。

下图说明了 [**IoCsqRemoveIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqremoveirp)的控制流。

![说明 iocsqremoveirp 控制流的示意图](images/3iocsqremoveirp.png)

这些例程又会调度到驱动程序提供的例程。

[**IoCsqInsertIrpEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqinsertirpex)例程提供对*CsqInsertIrpEx*例程的扩展功能的访问。 它将返回 *CsqInsertIrpEx*返回的状态值。 调用方可以使用此值来确定 IRP 是否已成功排队。 **IoCsqInsertIrpEx** 还允许调用方为 *CsqInsertIrpEx*的 InsertContext 参数指定值。

请注意，无论队列具有*CsqInsertIrp*例程还是*CsqInsertIrpEx*例程，都可以在任何取消安全的队列上调用**IoCsqInsertIrp**和**IoCsqInsertIrpEx** 。 **IoCsqInsertIrp** 在这两种情况下的行为相同。 如果向 **IoCsqInsertIrpEx** 传递了一个具有 *CsqInsertIrp* 例程的队列，则其行为与 **IoCsqInsertIrp**相同。

下图说明了 [**IoCsqInsertIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqinsertirp)的控制流。

![说明 iocsqinsertirp 控制流的示意图](images/iocsqinsertirp.png)

下图说明了 [**IoCsqInsertIrpEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqinsertirpex)的控制流。

![说明 iocsqinsertirpex 控制流的示意图](images/2iocsqinitializeex.png)

使用 **IoCsq * Xxx*** 例程对 irp 进行排队和取消排队的方式有多种。 例如，驱动程序可能只是将 Irp 按接收顺序进行排队。 驱动程序可以将 IRP 排队，如下所示：

```cpp
    status = IoCsqInsertIrpEx(IoCsq, Irp, NULL, NULL);
```

如果不需要驱动程序来区分特定的 Irp，则它可能会按照它们的排队顺序将其取消排队，如下所示：

```cpp
    IoCsqRemoveNextIrp(IoCsq, NULL);
```

或者，驱动程序可以对特定的 Irp 进行排队和取消排队。 例程使用不透明 [**IO \_ CSQ \_ IRP \_ 上下文**](./eprocess.md) 结构标识队列中的特定 irp。 驱动程序将 IRP 排队，如下所示：

```cpp
    IO_CSQ_IRP_CONTEXT ParticularIrpInQueue;
    IoCsqInsertIrp(IoCsq, Irp, &ParticularIrpInQueue);
```

然后，该驱动程序可以使用 **IO \_ CSQ \_ IRP \_ 上下文** 值取消对同一 IRP 的排队。

```cpp
    IoCsqRemoveIrp(IoCsq, Irp, &ParticularIrpInQueue);
```

还可能需要驱动程序根据特定条件从队列中删除 Irp。 例如，驱动程序可能会将优先级与每个 IRP 关联起来，以便较高优先级的 Irp 首先进入取消排队。 驱动程序可以将 *PeekContext* 值传递到 [**IoCsqRemoveNextIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqremovenextirp)，系统在请求队列中的下一 IRP 时，系统会将该值传递回驱动程序。

 


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
ms.openlocfilehash: 34bd7a6dd81b0343e3ca6a0dd45f772206791cea
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377239"
---
# <a name="cancel-safe-irp-queues"></a>可安全取消的 IRP 队列





实现其自己 IRP 排队的驱动程序应使用*取消安全 IRP 队列*框架。 取消安全 IRP 队列拆分成两个部分处理 IRP:

1. 该驱动程序提供了一组实现驱动程序的 IRP 队列上的标准操作的回调例程。 提供的操作包括插入和从队列中，并锁定和解锁队列中删除 Irp。 请参阅[实施取消安全 IRP 队列](#ddk-implementing-the-cancel-safe-irp-queue-kg)。

2. 只要该驱动程序必须实际插入或从队列中删除 IRP，它使用系统提供**IoCsq * Xxx*** 例程。 这些例程处理所有同步和 IRP 取消逻辑的驱动程序。

使用取消安全 IRP 队列的驱动程序不实现[*取消*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_cancel)例程以支持 IRP 取消。

框架将确保驱动程序插入和从其队列中以原子方式移除 Irp。 它还确保 IRP 取消已正确实现。 不使用 framework 的驱动程序必须手动锁定和解锁之前执行任何插入和删除队列。 它们还必须避免在实现时可能会导致的争用条件*取消*例程。 (有关可能会出现争用条件的说明，请参阅[同步 IRP 取消](synchronizing-irp-cancellation.md)。)

取消安全 IRP 队列 framework 是 Windows XP 或更高版本的 Windows 中包含了。 此外必须使用 Windows 2000 和 Windows 98 的驱动程序 / 我可以链接到 Csq.lib 库包含 Windows Driver Kit (WDK) 中。 Csq.lib 库提供了此框架的实现。

**IoCsq * Xxx*** 例程中的 Windows XP 和更高版本的 wdm.h 中和 Ntddk.h 声明。 此外必须使用 Windows 2000 和 Windows 98 的驱动程序 / 我必须包括 Csq.h 声明。

您可以看到如何使用中的取消安全 IRP 队列的完整演示\\src\\常规\\取消 WDK 的目录。 有关这些队列的详细信息，另请参阅[流的队列的控制取消安全 IRP](https://go.microsoft.com/fwlink/p/?linkid=57844)白皮书。

### <a href="" id="ddk-implementing-the-cancel-safe-irp-queue-kg"></a>实现取消安全 IRP 队列

若要实现取消安全 IRP 队列，驱动程序必须提供以下例程：

-   下面的例程将 Irp 插入队列之一：[*CsqInsertIrp* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_csq_insert_irp)或[ *CsqInsertIrpEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_csq_insert_irp_ex)。 *CsqInsertIrpEx*是扩展的版本*CsqInsertIrp*; 队列使用一个或另一个实现。

-   一个[ *CsqRemoveIrp* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_csq_remove_irp)从队列中移除指定的 IRP 的例程。

-   一个[ *CsqPeekNextIrp* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_csq_peek_next_irp)将指针返回到下一步 IRP 遵循在队列中指定的 IRP 的例程。 这是系统会将传递*PeekContext*值，它接收来自[ **IoCsqRemoveNextIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqremovenextirp)。 该驱动程序可以将该值以任何方式解释。

-   这两个以下的例程，以允许系统锁定和解锁 IRP 队列：[*CsqAcquireLock* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_csq_acquire_lock)并[ *CsqReleaseLock*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_csq_release_lock)。

-   一个[ *CsqCompleteCanceledIrp* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_csq_complete_canceled_irp)完成取消的 IRP 的例程。

驱动程序的例程的指针存储在[ **IO\_CSQ** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)结构，描述该队列。 该驱动程序分配的存储**IO\_CSQ**结构。 **IO\_CSQ**的结构保证一定保持固定的大小，因此驱动程序可以安全地将嵌入在其设备扩展的结构。

驱动程序使用任一[ **IoCsqInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqinitialize)或[ **IoCsqInitializeEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqinitializeex)初始化结构。 使用**IoCsqInitialize**如果实现了队列[ *CsqInsertIrp*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_csq_insert_irp)，或者**IoCsqInitializeEx**如果队列实现*CsqInsertIrpEx*。

驱动程序只需要提供每个回调例程中的基本功能。 例如，只有*CsqAcquireLock*并*CsqReleaseLock*例程实现锁处理。 系统会自动调用这些例程锁定和解锁根据队列。

只要提供适当的调度例程，您可以在您的驱动程序，实现任何类型的 IRP 排队机制。 例如，驱动程序无法为链接列表，或作为优先级队列实现队列。

[*CsqInsertIrpEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_csq_insert_irp_ex)提供了到队列不超过一个更灵活界面[ *CsqInsertIrp*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_csq_insert_irp)。 该驱动程序可以使用它的返回值以指示该操作; 结果如果它返回一个错误代码，导致插入失败。 一个*CsqInsertIrp*例程不返回一个值，因此没有简单的方法，以指示失败，完成插入操作。 此外， *CsqInsertIrpEx*采用一个附加的驱动程序定义*InsertContext*参数可用于指定使用队列实现的其他特定于驱动程序的信息。

驱动程序可以使用*CsqInsertIrpEx*来实现更复杂的 IRP 处理。 例如，如果不有任何挂起的 Irp *CsqInsertIrpEx*例程可以返回一个错误代码和驱动程序可以立即处理 IRP。 同样，如果不能再将排队 Irp， *CsqInsertIrpEx*可能会返回错误代码指示这一事实。

该驱动程序就会与所有 IRP 取消处理。 系统提供[*取消*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_cancel)例程 Irp 的队列中。 此例程调用[ *CsqRemoveIrp* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_csq_remove_irp)若要从队列中删除 IRP 和[ *CsqCompleteCanceledIrp* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_csq_complete_canceled_irp)完成 IRP取消操作。

下图说明了 IRP 取消控制流。

![说明的 irp 取消控制流关系图](images/5cancelingirp.png)

基本实现[ *CsqCompleteCanceledIrp* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_csq_complete_canceled_irp)如下所示。

```cpp
VOID CsqCompleteCanceledIrp(PIO_CSQ Csq, PIRP Irp) {
  Irp->IoStatus.Status = STATUS_CANCELLED;
  Irp->IoStatus.Information = 0;

  IoCompleteRequest(Irp, IO_NO_INCREMENT);
}
```

驱动程序可以使用任何操作系统的同步基元来实现其[ *CsqAcquireLock* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_csq_acquire_lock)并[ *CsqReleaseLock* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_csq_release_lock)例程。 包括可用的同步基元[旋转锁](spin-locks.md)并[互斥体对象](mutex-objects.md)。

下面是举例说明如何将驱动程序可以实现锁定使用自旋锁。

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

系统将指针传递给 IRQL 变量到*CsqAcquireLock*并*CsqReleaseLock*。 如果驱动程序使用旋转锁实现锁定的队列，该驱动程序可以使用此变量来存储当前 IRQL 队列处于锁定状态时。

驱动程序不需要使用自旋锁。 例如，驱动程序无法使用互斥体锁定队列。 有关可用于驱动程序的同步技术的说明，请参阅[同步技术](synchronization-techniques.md)。

### <a href="" id="ddk-using-the-cancel-safe-irp-queue-kg"></a>使用取消安全 IRP 队列

驱动程序时排队和取消排队 Irp，请使用以下系统例程：

-   以下方法之一将 IRP 插入队列：[**IoCsqInsertIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqinsertirp)或[ **IoCsqInsertIrpEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqinsertirpex)。

-   [**IoCsqRemoveNextIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqremovenextirp)若要删除队列中的下一步 IRP。 该驱动程序可以选择指定的密钥值。

下图说明了的控制流[ **IoCsqRemoveNextIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqremovenextirp)。

![说明 iocsqremovenextirp 的控制流关系图](images/4iocsqremovenextirp.png)

-   [**IoCsqRemoveIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqremoveirp)若要从队列中删除指定的 IRP。

下图说明了的控制流[ **IoCsqRemoveIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqremoveirp)。

![说明 iocsqremoveirp 的控制流关系图](images/3iocsqremoveirp.png)

这些例程，反过来，调度到驱动程序所提供的例程。

[ **IoCsqInsertIrpEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqinsertirpex)例程提供扩展功能的访问权限*CsqInsertIrpEx*例程。 它将返回所返回的状态值*CsqInsertIrpEx*。 调用方可以使用此值以确定是否或不在 IRP 已成功排队。 **IoCsqInsertIrpEx**还允许调用方指定的 InsertContext 参数的值*CsqInsertIrpEx*。

请注意，这两**IoCsqInsertIrp**并**IoCsqInsertIrpEx**队列是否可以取消安全的任何队列，调用*CsqInsertIrp*例程或*CsqInsertIrpEx*例程。 **IoCsqInsertIrp**行为在任一情况下相同。 如果**IoCsqInsertIrpEx**传递队列具有*CsqInsertIrp*例程，它的行为完全相同**IoCsqInsertIrp**。

下图说明了的控制流[ **IoCsqInsertIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqinsertirp)。

![说明 iocsqinsertirp 的控制流关系图](images/iocsqinsertirp.png)

下图说明了的控制流[ **IoCsqInsertIrpEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqinsertirpex)。

![说明 iocsqinsertirpex 的控制流关系图](images/2iocsqinitializeex.png)

有多种自然的方式来使用**IoCsq * Xxx*** 例程来排队和取消排队 Irp。 例如，驱动程序可能只需队列 Irp 中接收它们的顺序处理。 该驱动程序无法排队 IRP，如下所示：

```cpp
    status = IoCsqInsertIrpEx(IoCsq, Irp, NULL, NULL);
```

如果该驱动程序不需要区分特定 Irp，它无法然后只需取消排队它们在其中排队，按如下所示的顺序：

```cpp
    IoCsqRemoveNextIrp(IoCsq, NULL);
```

或者，驱动程序无法排队和取消排队特定 Irp。 例程使用不透明[ **IO\_CSQ\_IRP\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)结构，用于标识特定 Irp 队列中的。 该驱动程序队列 IRP，如下所示：

```cpp
    IO_CSQ_IRP_CONTEXT ParticularIrpInQueue;
    IoCsqInsertIrp(IoCsq, Irp, &ParticularIrpInQueue);
```

该驱动程序然后可以通过使用排队相同 IRP **IO\_CSQ\_IRP\_上下文**值。

```cpp
    IoCsqRemoveIrp(IoCsq, Irp, &ParticularIrpInQueue);
```

该驱动程序可能还需要从基于特定条件的队列中删除 Irp。 例如，驱动程序可能会将关联优先级与每个 IRP，以便更高的优先级 Irp 获取第一次取消排队。 该驱动程序可能会传递*PeekContext*值设置为[ **IoCsqRemoveNextIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqremovenextirp)，它请求在队列中下一步的 IRP 时，系统将传递回该驱动程序。

 

 





---
title: 使用自旋锁的示例
description: 使用自旋锁的示例
ms.assetid: 0f3cd7fe-d3e6-4024-9b2f-7140c6ddd1ea
keywords:
- 旋转锁定 WDK 内核
- 中断自旋锁定 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8330178a5aec7ce4f6d4fcb80a899d163f5c048e
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189257"
---
# <a name="using-spin-locks-an-example"></a>使用自旋锁：示例





最大程度地减少驱动程序持有自旋锁的时间可显著提高驱动程序的性能和整体系统的性能。 例如，请看下图，其中显示了中断旋转锁如何保护特定于设备的数据，这些数据必须在虚拟机中的 ISR 和 [*StartIo*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio) 和 [*DpcForIsr*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine) 例程之间共享。

![说明如何使用中断自旋锁的关系图](images/16ispnlk.png)

1.  尽管驱动程序的 ISR 在一个处理器上的 DIRQL 运行，但其 *StartIo* 例程在 \_ 第二个处理器上的调度级别运行。 内核中断处理程序保存驱动程序的 ISR 的 InterruptSpinLock，该程序会在驱动程序的设备扩展中访问受保护的设备特定数据，如) 的状态或指向设备寄存器 (的指针。 *StartIo*例程（可以访问 SynchronizeContext）调用[**KeSynchronizeExecution**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution)，将指针传递给关联中断对象、共享 SynchronizeContext 和驱动程序的[*SynchCritSection*](/windows-hardware/drivers/ddi/wdm/nc-wdm-ksynchronize_routine) (例程，) 上一个图中的 AccessDevice。

    直到 ISR 返回，从而释放驱动程序的 InterruptSpinLock，**KeSynchronizeExecution * ** * 在第二个处理器上旋转，阻止 AccessDevice 触摸 SynchronizeContext。 但是， **KeSynchronizeExecution** 还会将第二个处理器上的 IRQL 提升为中断对象的 SynchronizeIrql，从而防止在该处理器上发生另一个设备中断，以便 ACCESSDEVICE 在 ISR 返回后就可以在 DIRQL 上运行。 但是，对于其他设备、时钟中断和电源中断中断，更高的 DIRQL 中断仍可能出现在任一处理器上。

2.  当 ISR 排队驱动程序的 *DpcForIsr* 并返回时，AccessDevice 会在关联中断对象的 SynchronizeIrql 上的第二个处理器上运行，并访问 SynchronizeContext。 同时， *DpcForIsr* 在调度级别为 IRQL 的另一个处理器上运行 \_ 。 *DpcForIsr*还可以访问 SynchronizeContext，因此它使用*StartIo*例程在步骤1中执行的相同参数调用**KeSynchronizeExecution** 。

    当 **KeSynchronizeExecution** 获取自旋锁并代表 *StartIo* 例程运行 AccessDevice 时，将为驱动程序提供的同步例程 AccessDevice 提供对 SynchronizeContext 的独占访问权限。 由于 AccessDevice 在 SynchronizeIrql 上运行，因此，驱动程序的 ISR 无法获取旋转锁定，并在释放旋转锁之前访问同一区域，即使在 AccessDevice 执行时，设备会在其他处理器上中断。

3.  AccessDevice 返回，释放旋转锁。 *StartIo*例程在 \_ 第二个处理器上的调度级别继续运行。 **KeSynchronizeExecution** 现在在第三个处理器上运行 AccessDevice，因此它可以代表 *DpcForIsr*访问 SynchronizeContext。 但是，如果在步骤2中的 *DpcForIsr* 调用 **KeSynchronizeExecution** 之前发生了设备中断，则 ISR 可能会在另一个处理器上运行，然后 **KeSynchronizeExecution** 才能获取旋转锁并在第三个处理器上运行 AccessDevice。

如上图所示，虽然在一个处理器上运行的例程持有自旋锁，但每个尝试获取该自旋锁的例程都不会完成任何工作。 尝试获取已持有的旋转锁的每个例程只是在其当前处理器上旋转，直到持有者释放旋转锁。 释放旋转锁后，只能有一个例程获取它;当前尝试获取同一旋转锁定的每个其他例程将继续旋转。

任何自旋锁的持有者都将在引发的 IRQL 处运行：在 \_ 执行人员旋转锁定的调度级别，或在中断旋转锁的 DIRQL 上运行。 [**KeAcquireSpinLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock)和**KeAcquireInStackQueuedSpinLock**的调用方在调度级别运行， \_ 直到它们调用[**KeReleaseSpinLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock)或**KeReleaseInStackQueuedSpinLock**释放该锁。 [**KeSynchronizeExecution**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution)的调用方自动将当前处理器上的 IRQL 引发到中断对象的 SynchronizeIrql，直到调用方提供的*SynchCritSection*例程退出并**KeSynchronizeExecution**返回控制权。 有关详细信息，请参阅 [调用使用自旋锁的支持例程](calling-support-routines-that-use-spin-locks.md)。

**请记住以下关于使用自旋锁的事实：**

以较低的 IRQL 运行的所有代码都不能获取对旋转锁持有者占用的处理器集以及尝试获取同一自旋锁的其他例程所做的任何工作。

因此，最大程度地减少驱动程序持有自旋锁的时间将导致驱动程序性能明显提高，并大大提高系统的整体性能。

如上图所示，内核中断处理程序在第一次提供的基础上，在多处理器计算机中以相同的 IRQL 运行例程。 内核还会执行以下操作：

-   当驱动程序例程调用 **KeSynchronizeExecution**时，内核将导致驱动程序的 *SynchCritSection* 例程在调用 **KeSynchronizeExecution** 的同一处理器上运行 (参见步骤1和 3) 。

-   当驱动程序的 ISR 对其 *DpcForIsr*进行排队时，内核会使 DPC 在依赖低于调度级别的第一个可用处理器上运行 \_ 。 这并不一定是发生 [**IoRequestDpc**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iorequestdpc) 调用的同一处理器 (参阅步骤 2) 。

驱动程序的中断驱动 i/o 操作可能会在单处理器计算机中进行序列化，但在 SMP 计算机中，相同的操作可能是真正的异步操作。 如上图所示，驱动程序的 ISR 可以在 SMP 计算机上的 CPU4 上运行，之后其 *DpcForIsr* 开始处理已在 CPU1 上处理设备中断的 IRP。

换句话说，您不应假定中断旋转锁定可以保护由 isr 在某个处理器上运行时所保存的特定于操作的数据，而当 *DpcForIsr* 或 [*CustomDpc*](/windows-hardware/drivers/ddi/wdm/nc-wdm-kdeferred_routine) 例程运行之前，如果另一个处理器上出现设备中断，则该数据会被 isr 覆盖。

尽管驱动程序可以尝试序列化所有中断驱动的 i/o 操作以保留由 ISR 收集的数据，但是该驱动程序在 SMP 计算机上的运行速度不会比在单处理器计算机上运行得更快。 为了获得最佳的驱动程序性能，同时跨单处理器和多处理器平台实现可移植性，驱动程序应使用其他某种方法来保存由 ISR 获取的特定于操作的数据，以便 *DpcForIsr*进行后续处理。

例如，ISR 可以在它传递给 *DpcForIsr*的 IRP 中保存特定于操作的数据。 此方法的一项改进是实现一个 *DpcForIsr* ，它可以查阅 isr 增加的计数，使用 isr 提供的数据处理该计数的 irp 数量，并在返回之前将计数重置为零。 当然，计数必须受驱动程序的中断自旋锁保护，因为它的 ISR 和 *SynchCritSection* 会动态维护其值。

 


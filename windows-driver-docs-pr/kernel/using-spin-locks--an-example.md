---
title: 使用数值调节钮锁定示例
description: 使用数值调节钮锁定示例
ms.assetid: 0f3cd7fe-d3e6-4024-9b2f-7140c6ddd1ea
keywords:
- 数值调节钮锁 WDK 内核
- 中断自旋锁 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d25aa18c1bfe8cc1b2559ca39013d150d0021cc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547404"
---
# <a name="using-spin-locks-an-example"></a>使用自旋锁：示例





将驱动程序包含自旋锁可以显著提高这两个性能和总体系统的驱动程序的时间降至最低。 例如，考虑下图显示了如何中断旋转锁保护必须 ISR 之间共享的特定于设备的数据并[ *StartIo* ](https://msdn.microsoft.com/library/windows/hardware/ff563858)和[ *DpcForIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff544079) SMP 计算机中的例程。

![关系图说明如何使用中断自旋锁](images/16ispnlk.png)

1.  而在驱动程序 ISR DIRQL 在运行在一个处理器，其*StartIo*例程在调度运行\_级别上的第二个处理器。 内核中断处理程序保存在扩展中的驱动程序的设备驱动程序的 ISR，哪些访问受保护的特定于设备的数据，如状态或指向设备注册 (SynchronizeContext) 的 InterruptSpinLock。 *StartIo*例程，可供访问 SynchronizeContext 时，调用[ **KeSynchronizeExecution**](https://msdn.microsoft.com/library/windows/hardware/ff553302)，指针传递给对象的关联的中断，共享 SynchronizeContext，并在驱动程序[ *SynchCritSection* ](https://msdn.microsoft.com/library/windows/hardware/ff563928)例程 (AccessDevice 在上图中)。

    直到 ISR 返回，从而释放驱动程序的 InterruptSpinLock **KeSynchronizeExecution * * * 旋转*第二个处理器，不接触 SynchronizeContext 阻止 AccessDevice 上。 但是， **KeSynchronizeExecution**还在第二个处理器的对象的中断，从而防止出现在该处理器上，以便 AccessDevice 可以是另一个设备中断 SynchronizeIrql 引发 IRQL在 DIRQL ISR 返回时，就立即运行。 但是，其他设备、 时钟中断和电源故障中断的更高版本 DIRQL 中断仍然会出现在任何一个处理器上。

2.  当 ISR 队列的驱动程序*DpcForIsr*和返回 AccessDevice 的关联的中断对象 SynchronizeIrql 在第二个处理器上运行并访问 SynchronizeContext。 同时， *DpcForIsr*在调度另一个处理器上运行\_级别 IRQL。 *DpcForIsr*也已准备好访问 SynchronizeContext，因此它将调用**KeSynchronizeExecution**使用相同的参数的*StartIo*例程未在步骤 1 中。

    当**KeSynchronizeExecution**获取数值调节钮锁并运行代表 AccessDevice *StartIo*例程、 AccessDevice 提供对独占访问权限的驱动程序提供同步例程SynchronizeContext。 因为 SynchronizeIrql 在运行时 AccessDevice，驱动程序的 ISR 不能获取数值调节钮锁和访问同一个区域之前自旋锁被释放，即使 AccessDevice 执行时，设备将中断另一个处理器上。

3.  返回 AccessDevice，释放自旋锁。 *StartIo*例行恢复在调度运行\_级别上的第二个处理器。 **KeSynchronizeExecution**现在运行第三个处理器，AccessDevice，因此它可以访问代表 SynchronizeContext *DpcForIsr*。 但是，如果设备中断发生之前*DpcForIsr*称为**KeSynchronizeExecution**在步骤 2 中 ISR 可能运行之前的另一个处理器上**KeSynchronizeExecution**无法获得旋转锁和第三个处理器上运行 AccessDevice。

如，如上图所示，持有数值调节钮锁定，在一个处理器上运行的例程，尝试获取该数值调节钮锁的其他每个例程将获取完成任何工作。 每个例程尝试获取的已保存数值调节钮锁只旋转，其当前处理器上直到持有者释放自旋锁。 当释放自旋锁时，且只有一个例程获得该软件;目前正在尝试获得相同的旋转锁的其他每个例程将继续进行旋转。

在引发 IRQL 运行的任何旋转锁持有者： 在调度\_executive 数值调节钮锁定或在中断自旋锁 DIRQL 级别。 调用方[ **KeAcquireSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff551917)并**KeAcquireInStackQueuedSpinLock**在调度运行\_级别直到它们调用[ **KeReleaseSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff553145)或**KeReleaseInStackQueuedSpinLock**才能释放锁。 调用方[ **KeSynchronizeExecution** ](https://msdn.microsoft.com/library/windows/hardware/ff553302)之前的调用方提供的中断对象 SynchronizeIrql 到当前的处理器上会自动引发 IRQL *SynchCritSection*日常退出并**KeSynchronizeExecution**返回控件。 有关详细信息，请参阅[调用支持例程，使用旋转锁](calling-support-routines-that-use-spin-locks.md)。

**请记住使用自旋锁有关的以下事实：**

在较低的 IRQL 运行的所有代码无法获得的一组由自旋锁持有者和由其他例程尝试获取同一个数值调节钮锁占用的处理器上执行任何工作。

因此，最大程度减少驱动程序包含数值调节钮的时间中显著提高驱动程序性能的锁结果和更好的整体系统性能显著影响。

上图所示，内核中断处理程序执行先，先来先服务的基础上运行的多处理器计算机中的相同 IRQL 例程。 内核还执行以下操作：

-   当调用驱动程序例程**KeSynchronizeExecution**，内核会导致驱动程序的*SynchCritSection*例程，以从其运行在同一处理器上调用**KeSynchronizeExecution**发生 （请参阅步骤 1 和 3）。

-   当驱动程序的 ISR 队列及其*DpcForIsr*，内核会导致 DPC 的 IRQL 低于调度第一个可用处理器上运行\_级别。 这不一定是从其在同一处理器[ **IoRequestDpc** ](https://msdn.microsoft.com/library/windows/hardware/ff549657)调用发生 （请参阅步骤 2）。

驱动程序的中断驱动 I/O 操作可能倾向于以进行序列化，以单处理器计算机，但相同的操作可能会在 SMP 机真正实现异步。 上图所示，可以由驱动程序的 ISR 之前 SMP 计算机中运行 CPU4 上其*DpcForIsr*开始处理的 IRP 为其 ISR 已经处理 CPU1 上的设备中断。

换而言之，不应假定中断自旋锁可以保护操作特定数据的一个处理器上运行时设备中断发生在之前的另一个处理器上的 ISR 覆盖时，将保存 ISR *DpcForIsr*或[ *CustomDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542972)日常运行。

尽管驱动程序可能试图进行序列化的所有中断驱动 I/O 操作来保留 ISR 所收集的数据，但该驱动程序将不运行速度快得多的单处理器计算机中，比 SMP 计算机。 若要获取最佳的可能的驱动程序性能，同时保持在单处理器和多处理器平台可移植，驱动程序应使用某些其他方法来保存特定于操作的数据以供后续处理 ISR 通过获取*DpcForIsr*。

例如，ISR 可以将保存特定于操作的数据中将其传递到 IRP *DpcForIsr*。 此技术的优化是实现*DpcForIsr* ，担任顾问 ISR 扩充的计数、 处理计数的数量的 Irp 使用 ISR 提供的数据和将计数重置为零，然后再返回。 当然，计数必须受驱动程序的中断自旋锁因为其 ISR 和一个*SynchCritSection*会动态地维护其值。

 

 





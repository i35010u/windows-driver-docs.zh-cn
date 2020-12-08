---
title: 同步和线程 DPC
description: 同步和线程 DPC
keywords:
- 线程 Dpc WDK 内核
- 同步 WDK 内核，中断
- 排队自旋锁 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a32721cc36aab2ab2fd4ad63b7c88f78b3d67bd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792713"
---
# <a name="synchronization-and-threaded-dpcs"></a>同步和线程 DPC





若要同步对从 [*CustomThreadedDpc*](https://msdn.microsoft.com/library/windows/hardware/ff542976) 例程内部和外部访问的内存位置的访问，驱动程序可以使用普通的旋转锁或排队的自旋锁。 执行此操作时，驱动程序必须遵守某些规则，以便在 IRQL = 被动级别上正确同步， \_ 并在 irql = 调度 \_ 级别执行，因为 *CustomThreadedDpc* 例程可以同时在这两个 IRQLs 上执行。

对于普通旋转锁定，以下规则适用：

-   若要获取和释放旋转锁定，驱动程序可以在 *CustomThreadedDpc* 例程的内部和外部调用 [**KeAcquireSpinLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock)和 [**KeReleaseSpinLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock) 。

-   驱动程序可以从 *CustomThreadedDpc* 例程内调用 [**KeAcquireSpinLockForDpc**](/previous-versions/windows/hardware/drivers/ff551923(v=vs.85))和 [**KeReleaseSpinLockForDpc**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlockfordpc) 。 请注意， *CustomThreadedDpc* 例程不得调用 [**KeAcquireSpinLockAtDpcLevel**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlockatdpclevel) 或 [**KERELEASESPINLOCKFROMDPCLEVEL**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlockfromdpclevel)，因为只能在 IRQL = 调度级别安全地调用这些例程 \_ 。

排队自旋锁的规则如下所示：

-   若要获取和释放旋转锁定，驱动程序可以在 *CustomThreadedDpc* 例程的内部和外部调用 [**KeAcquireInStackQueuedSpinLock**](/previous-versions/windows/hardware/drivers/ff551899(v=vs.85))和 [**KeReleaseInStackQueuedSpinLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlock) 。

-   驱动程序可以从 *CustomThreadedDpc* 例程内调用 [**KeAcquireInStackQueuedSpinLockForDpc**](/previous-versions/windows/hardware/drivers/ff551912(v=vs.85))和 [**KeReleaseInStackQueuedSpinLockForDpc**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlockfordpc) 。 请注意， *CustomThreadedDpc* 例程不得调用 [**KeAcquireInStackQueuedSpinLockAtDpcLevel**](/previous-versions/windows/hardware/drivers/ff551908(v=vs.85)) 或 [**KERELEASEINSTACKQUEUEDSPINLOCKFROMDPCLEVEL**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlockfromdpclevel)，因为只能在 IRQL = 调度级别安全地调用这些例程 \_ 。

由于 **KeAcquireSpinLockForDpc** 和 **KeAcquireInStackQueuedSpinLockForDpc** 在调度级别调用时不会重置 IRQL \_ ，因此它们的执行速度高于 **KeAcquireSpinLock** 和 **KeAcquireInStackQueuedSpinLock**。

有关旋转锁定的详细信息，请参阅 [自旋锁](./introduction-to-spin-locks.md)。

 


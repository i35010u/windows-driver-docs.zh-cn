---
title: 同步和线程 DPC
description: 同步和线程 DPC
ms.assetid: b4f2c77b-226c-4229-bcbb-5eebabdc28a4
keywords:
- 线程 Dpc WDK 内核
- 同步 WDK 内核，中断
- 排队自旋锁 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 89bc7f1685dafc0972c552dc4af28aaa45f2c8bc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838398"
---
# <a name="synchronization-and-threaded-dpcs"></a>同步和线程 DPC





若要同步对从[*CustomThreadedDpc*](https://msdn.microsoft.com/library/windows/hardware/ff542976)例程内部和外部访问的内存位置的访问，驱动程序可以使用普通的旋转锁或排队的自旋锁。 执行此操作时，驱动程序必须遵守某些规则，以便在 IRQL = 被动\_级别上正确同步，并在 IRQL = 调度\_级别，因为*CustomThreadedDpc*例程可以同时在这两个 IRQLs 上执行。

对于普通旋转锁定，以下规则适用：

-   若要获取和释放旋转锁定，驱动程序可以在*CustomThreadedDpc*例程的内部和外部调用[**KeAcquireSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock)和[**KeReleaseSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock) 。

-   驱动程序可以从*CustomThreadedDpc*例程内调用[**KeAcquireSpinLockForDpc**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551923(v=vs.85))和[**KeReleaseSpinLockForDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlockfordpc) 。 请注意， *CustomThreadedDpc*例程不得调用[**KeAcquireSpinLockAtDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlockatdpclevel)或[**KERELEASESPINLOCKFROMDPCLEVEL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlockfromdpclevel)，因为只能在 IRQL = 调度\_级别安全地调用这些例程。

排队自旋锁的规则如下所示：

-   若要获取和释放旋转锁定，驱动程序可以在*CustomThreadedDpc*例程的内部和外部调用[**KeAcquireInStackQueuedSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551899(v=vs.85))和[**KeReleaseInStackQueuedSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlock) 。

-   驱动程序可以从*CustomThreadedDpc*例程内调用[**KeAcquireInStackQueuedSpinLockForDpc**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551912(v=vs.85))和[**KeReleaseInStackQueuedSpinLockForDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlockfordpc) 。 请注意， *CustomThreadedDpc*例程不得调用[**KeAcquireInStackQueuedSpinLockAtDpcLevel**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551908(v=vs.85))或[**KERELEASEINSTACKQUEUEDSPINLOCKFROMDPCLEVEL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlockfromdpclevel)，因为只能在 IRQL = 调度时安全地调用这些例程\_调配.

由于**KeAcquireSpinLockForDpc**和**KeAcquireInStackQueuedSpinLockForDpc**在调度\_级别调用时不会重置 IRQL，因此它们的执行速度快于**KeAcquireSpinLock**和**KeAcquireInStackQueuedSpinLock**。

有关旋转锁定的详细信息，请参阅[自旋锁](spin-locks.md)。

 

 





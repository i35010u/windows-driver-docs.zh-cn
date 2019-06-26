---
title: 同步和线程 DPC
description: 同步和线程 DPC
ms.assetid: b4f2c77b-226c-4229-bcbb-5eebabdc28a4
keywords:
- 线程的 Dpc WDK 内核
- 同步 WDK 内核中断
- 排队自旋锁 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 78273ec2a8baf4a70098b662d45edb91c00bb3a4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385106"
---
# <a name="synchronization-and-threaded-dpcs"></a>同步和线程 DPC





同步是访问从这两个内部和外部内存位置的访问权限[ *CustomThreadedDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542976)例程，驱动程序可以使用普通的自旋锁或排入队列自旋锁。 这样做时，驱动程序必须遵循某些规则来正确同步在 IRQL = 被动\_级别，并在 IRQL = 调度\_级别，因为*CustomThreadedDpc*例程可以在这两个于 Irql 执行。

使用普通的旋转锁，适用以下规则：

-   若要获取和释放自旋锁，该驱动程序可以调用[ **KeAcquireSpinLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keacquirespinlock)并[ **KeReleaseSpinLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleasespinlock)从这两个内部和外部*CustomThreadedDpc*例程。

-   该驱动程序可以调用[ **KeAcquireSpinLockForDpc** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551923(v=vs.85))并[ **KeReleaseSpinLockForDpc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleasespinlockfordpc)从内部*CustomThreadedDpc*例程。 请注意， *CustomThreadedDpc*不能调用例程[ **KeAcquireSpinLockAtDpcLevel** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keacquirespinlockatdpclevel)或者[ **KeReleaseSpinLockFromDpcLevel** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleasespinlockfromdpclevel)，因为这些例程可以安全地调用仅在 IRQL = 调度\_级别。

排队的自旋锁的规则如下：

-   若要获取和释放自旋锁，该驱动程序可以调用[ **KeAcquireInStackQueuedSpinLock** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551899(v=vs.85))并[ **KeReleaseInStackQueuedSpinLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleaseinstackqueuedspinlock)从内部和外部*CustomThreadedDpc*例程。

-   该驱动程序可以调用[ **KeAcquireInStackQueuedSpinLockForDpc** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551912(v=vs.85))并[ **KeReleaseInStackQueuedSpinLockForDpc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleaseinstackqueuedspinlockfordpc)从内部*CustomThreadedDpc*例程。 请注意， *CustomThreadedDpc*不能调用例程[ **KeAcquireInStackQueuedSpinLockAtDpcLevel** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551908(v=vs.85))或者[ **KeReleaseInStackQueuedSpinLockFromDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleaseinstackqueuedspinlockfromdpclevel)，因为这些例程可以安全地调用仅在 IRQL = 调度\_级别。

因为**KeAcquireSpinLockForDpc**并**KeAcquireInStackQueuedSpinLockForDpc**不重置时在调度调用 IRQL\_级别，它们更快地执行比**KeAcquireSpinLock**并**KeAcquireInStackQueuedSpinLock**分别。

数值调节钮的锁有关的详细信息，请参阅[自旋锁](spin-locks.md)。

 

 





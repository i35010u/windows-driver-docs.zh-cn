---
title: 同步和线程 dpc 进行标记
description: 同步和线程 dpc 进行标记
ms.assetid: b4f2c77b-226c-4229-bcbb-5eebabdc28a4
keywords:
- 线程的 Dpc WDK 内核
- 同步 WDK 内核中断
- 排队自旋锁 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 43c99ddab8dde7102ad0ab4fc8d6762c5b4f1709
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524150"
---
# <a name="synchronization-and-threaded-dpcs"></a>同步和线程 dpc 进行标记





同步是访问从这两个内部和外部内存位置的访问权限[ *CustomThreadedDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542976)例程，驱动程序可以使用普通的自旋锁或排入队列自旋锁。 这样做时，驱动程序必须遵循某些规则来正确同步在 IRQL = 被动\_级别，并在 IRQL = 调度\_级别，因为*CustomThreadedDpc*例程可以在这两个于 Irql 执行。

使用普通的旋转锁，适用以下规则：

-   若要获取和释放自旋锁，该驱动程序可以调用[ **KeAcquireSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff551917)并[ **KeReleaseSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff553145)从这两个内部和外部*CustomThreadedDpc*例程。

-   该驱动程序可以调用[ **KeAcquireSpinLockForDpc** ](https://msdn.microsoft.com/library/windows/hardware/ff551923)并[ **KeReleaseSpinLockForDpc** ](https://msdn.microsoft.com/library/windows/hardware/ff553148)从内部*CustomThreadedDpc*例程。 请注意， *CustomThreadedDpc*不能调用例程[ **KeAcquireSpinLockAtDpcLevel** ](https://msdn.microsoft.com/library/windows/hardware/ff551921)或者[ **KeReleaseSpinLockFromDpcLevel** ](https://msdn.microsoft.com/library/windows/hardware/ff553150)，因为这些例程可以安全地调用仅在 IRQL = 调度\_级别。

排队的自旋锁的规则如下：

-   若要获取和释放自旋锁，该驱动程序可以调用[ **KeAcquireInStackQueuedSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff551899)并[ **KeReleaseInStackQueuedSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff553130)从内部和外部*CustomThreadedDpc*例程。

-   该驱动程序可以调用[ **KeAcquireInStackQueuedSpinLockForDpc** ](https://msdn.microsoft.com/library/windows/hardware/ff551912)并[ **KeReleaseInStackQueuedSpinLockForDpc** ](https://msdn.microsoft.com/library/windows/hardware/ff553133)从内部*CustomThreadedDpc*例程。 请注意， *CustomThreadedDpc*不能调用例程[ **KeAcquireInStackQueuedSpinLockAtDpcLevel** ](https://msdn.microsoft.com/library/windows/hardware/ff551908)或者[ **KeReleaseInStackQueuedSpinLockFromDpcLevel**](https://msdn.microsoft.com/library/windows/hardware/ff553137)，因为这些例程可以安全地调用仅在 IRQL = 调度\_级别。

因为**KeAcquireSpinLockForDpc**并**KeAcquireInStackQueuedSpinLockForDpc**不重置时在调度调用 IRQL\_级别，它们更快地执行比**KeAcquireSpinLock**并**KeAcquireInStackQueuedSpinLock**分别。

数值调节钮的锁有关的详细信息，请参阅[自旋锁](spin-locks.md)。

 

 





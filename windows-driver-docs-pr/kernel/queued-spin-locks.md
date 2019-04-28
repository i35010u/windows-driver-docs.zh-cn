---
title: 排队的自旋锁
description: 排队的自旋锁
ms.assetid: 7ccec366-5436-4e69-9fb7-f0090cf2adcb
keywords:
- 排队自旋锁 WDK 内核
- 先来先来先服务自旋锁 WDK 内核
- KeAcquireInStackQueuedSpinLock
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: bce42cba22d0ba89839cc8db85d02dedf144ae5f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338506"
---
# <a name="queued-spin-locks"></a>排队的自旋锁





*排队自旋锁*是对于多处理器计算机上的大量争用锁更加高效的自旋锁的一个变体。 在多处理器计算机上使用排队数值调节钮锁定处理器获取按先来先来先服务的自旋锁的保证。 Windows XP 和更高版本的 Windows 驱动程序应使用排队的自旋锁，而不是普通的自旋锁。

驱动程序为旋转锁，提供存储并初始化与该[ **KeInitializeSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff552160)。 驱动程序使用[ **KeAcquireInStackQueuedSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff551899)获取排队的自旋锁，并且[ **KeReleaseInStackQueuedSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff553130)若要将其释放。

驱动程序分配了[ **KLOCK\_队列\_处理**](https://msdn.microsoft.com/library/windows/hardware/ff554247)按指针，指向将传递的结构**KeAcquireInStackQueuedSpinLock**。 驱动程序通过相同的结构的指针，指向**KeReleaseInStackQueuedSpinLock**时释放自旋锁。 驱动程序通常应分配堆栈上的结构每次它们获取锁。

驱动程序将对排队的自旋锁例程和异常的调用必须混合**Ke*Xxx*旋转锁**例程在同一个旋转锁。

如果该驱动程序已在 IRQL = 调度\_级别，它可以调用[ **KeAcquireInStackQueuedSpinLockAtDpcLevel** ](https://msdn.microsoft.com/library/windows/hardware/ff551908)并[ **KeReleaseInStackQueuedSpinLockFromDpcLevel** ](https://msdn.microsoft.com/library/windows/hardware/ff553137)相反。

 

 





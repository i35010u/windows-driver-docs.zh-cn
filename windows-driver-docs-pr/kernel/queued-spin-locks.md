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
ms.openlocfilehash: 58bbf93eea990f4faad80174daf554af592a773a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378771"
---
# <a name="queued-spin-locks"></a>排队的自旋锁





*排队自旋锁*是对于多处理器计算机上的大量争用锁更加高效的自旋锁的一个变体。 在多处理器计算机上使用排队数值调节钮锁定处理器获取按先来先来先服务的自旋锁的保证。 Windows XP 和更高版本的 Windows 驱动程序应使用排队的自旋锁，而不是普通的自旋锁。

驱动程序为旋转锁，提供存储并初始化与该[ **KeInitializeSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinitializespinlock)。 驱动程序使用[ **KeAcquireInStackQueuedSpinLock** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551899(v=vs.85))获取排队的自旋锁，并且[ **KeReleaseInStackQueuedSpinLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleaseinstackqueuedspinlock)若要将其释放。

驱动程序分配了[ **KLOCK\_队列\_处理**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)按指针，指向将传递的结构**KeAcquireInStackQueuedSpinLock**。 驱动程序通过相同的结构的指针，指向**KeReleaseInStackQueuedSpinLock**时释放自旋锁。 驱动程序通常应分配堆栈上的结构每次它们获取锁。

驱动程序将对排队的自旋锁例程和异常的调用必须混合**Ke*Xxx*旋转锁**例程在同一个旋转锁。

如果该驱动程序已在 IRQL = 调度\_级别，它可以调用[ **KeAcquireInStackQueuedSpinLockAtDpcLevel** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551908(v=vs.85))并[ **KeReleaseInStackQueuedSpinLockFromDpcLevel** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleaseinstackqueuedspinlockfromdpclevel)相反。

 

 





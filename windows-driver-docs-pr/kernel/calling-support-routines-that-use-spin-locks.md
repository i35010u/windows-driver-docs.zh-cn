---
title: 调用使用自旋锁的支持例程
description: 调用使用自旋锁的支持例程
ms.assetid: 89cf1fd4-4f4b-4b82-9e50-e5766918c421
keywords:
- KeAcquireSpinLock
- KeAcquireInStackQueuedSpinLock
- 数值调节钮锁 WDK 内核
- 调用自旋锁支持例程 WDK 内核
- executive 自旋锁 WDK 内核
- 中断自旋锁 WDK 内核
- 排队自旋锁 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0be17e4e695f64b6cc7e10730f6fcc390d9bea3a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385260"
---
# <a name="calling-support-routines-that-use-spin-locks"></a>调用使用自旋锁的支持例程





调用[ **KeAcquireSpinLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keacquirespinlock)或[ **KeAcquireInStackQueuedSpinLock** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551899(v=vs.85))到调度当前处理器上设置IRQL\_级别相应地调用直到[ **KeReleaseSpinLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleasespinlock)或[ **KeReleaseInStackQueuedSpinLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleaseinstackqueuedspinlock)还原以前的 IRQL。 因此，驱动程序必须执行在 IRQL &lt;= 调度\_级别时它们调用**KeAcquireSpinLock**或**KeAcquireInStackQueuedSpinLock**。

调用方[ **KeAcquireSpinLockAtDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keacquirespinlockatdpclevel)， [ **KeAcquireInStackQueuedSpinLockAtDpcLevel**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551908(v=vs.85))， [ **KeReleaseInStackQueuedSpinLockFromDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleaseinstackqueuedspinlockfromdpclevel)，并[ **KeReleaseSpinLockFromDpcLevel** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleasespinlockfromdpclevel)运行得更快，因为它们已运行在 IRQL =调度\_级别，因此这些支持例程需要不会重置 IRQL 当前处理器上。 因此，它是一个错误在大多数 Windows 平台调用上的**KeAcquireSpinLockAtDpcLevel**或**KeAcquireInStackQueuedSpinLockAtDpcLevel** IRQL 小于调度在运行时\_级别。 它也是错误释放已获取与旋转锁**KeAcquireSpinLock**通过调用**KeReleaseSpinLockFromDpcLevel**由于调用方的原始 IRQL 不会还原。

保存主管的例程旋转锁，如<strong>ExInterlocked*Xxx</strong><em>，通常执行在 IRQL = 调度\_级别直到它们释放自旋锁并将控制权返回给调用方。但是，有可能的驱动程序[ </em>InterruptService<em> ](<https://msdn.microsoft.com/library/windows/hardware/ff547958>)例程并[ </em>SynchCritSection<em> ](<https://msdn.microsoft.com/library/windows/hardware/ff563928>)到例程 （这在 DIRQL 运行）调用某些**ExInterlocked</em>Xxx*** 例程，如**ExInterlocked*Xxx*列表**例程，只要数值调节钮传递到例程的锁以独占方式由 ISR 和*SynchCritSection*例程。

持有中断自旋锁的每个例程将在一组相关联的中断对象 DIRQL 执行。 因此，驱动程序必须调用**KeAcquireSpinLock**并**KeReleaseSpinLock**也不使用从其 ISR executive 自旋锁的任何其他例程或*SynchCritSection*例程。 此类调用是一个错误，可能会导致系统死锁，因此需要用户重新启动其自己的计算机。 请注意，如果驱动程序的 ISR 或*SynchCritSection*例程调用**ExInterlocked*Xxx*列表**例程，该驱动程序不能重复使用它将传递给自旋锁**ExInterlocked*Xxx*列表**中调用的例程**Ke*Xxx*旋转锁**或**Ke*Xxx*旋转锁*Xxx*DpcLevel**支持例程。

如果驱动程序包含 multivector ISR 或多个 ISR，可以调用其例程[ **KeSynchronizeExecution** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesynchronizeexecution)时最多执行的任何 irql *SynchronizeIrql*值为关联的中断对象指定何时进行的连接。

 

 





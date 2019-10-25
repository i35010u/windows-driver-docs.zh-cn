---
title: 调用使用自旋锁的支持例程
description: 调用使用自旋锁的支持例程
ms.assetid: 89cf1fd4-4f4b-4b82-9e50-e5766918c421
keywords:
- KeAcquireSpinLock
- KeAcquireInStackQueuedSpinLock
- 旋转锁定 WDK 内核
- 调用自旋锁支持例程 WDK 内核
- executive 旋转锁定 WDK 内核
- 中断自旋锁定 WDK 内核
- 排队自旋锁 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f490804b9045e7488dcee7255e8348eb24e62c1a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837134"
---
# <a name="calling-support-routines-that-use-spin-locks"></a>调用使用自旋锁的支持例程





调用[**KeAcquireSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock)或[**KeAcquireInStackQueuedSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551899(v=vs.85))会将当前处理器上的 IRQL 设置为调度\_级别，直到相应调用[**KeReleaseSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock)或[**KeReleaseInStackQueuedSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlock)还原以前的 IRQL。 因此，在调用**KeAcquireSpinLock**或**KeAcquireInStackQueuedSpinLock**时，驱动程序必须在 IRQL &lt;= 调度\_级别执行。

[**KeAcquireSpinLockAtDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlockatdpclevel)、 [**KeAcquireInStackQueuedSpinLockAtDpcLevel**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551908(v=vs.85))、 [**KeReleaseInStackQueuedSpinLockFromDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlockfromdpclevel)和[**KeReleaseSpinLockFromDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlockfromdpclevel)的调用方运行速度更快，因为它们已以 IRQL = 调度\_级别运行，因此这些支持例程不需要在当前处理器上重置 IRQL。 因此，大多数 Windows 平台在**KeAcquireSpinLockAtDpcLevel**或**KeAcquireInStackQueuedSpinLockAtDpcLevel**上运行时，如果在小于调度\_级别的情况下运行，则会出现严重错误。 调用**KeReleaseSpinLockFromDpcLevel**时，释放通过**KeAcquireSpinLock**获取的旋转锁也是错误的，因为调用方的原始 IRQL 不会还原。

保存执行自旋锁的例程（如<strong>ExInterlocked*Xxx</strong><em>）通常以 IRQL = 调度\_级别执行，直到它们释放自旋锁并将控制返回给调用方。但是，驱动程序[</em>的 InterruptService<em> ](<https://msdn.microsoft.com/library/windows/hardware/ff547958>)例程和[ </em>SynchCritSection<em> ](<https://msdn.microsoft.com/library/windows/hardware/ff563928>)例程（在 DIRQL 中运行）可以调用某些**ExInterlocked</em>Xxx*** 例程，如**ExInterlocked*Xxx*列表**例程，前提是传递到例程的自旋锁由 ISR 和*SynchCritSection*例程独占使用。

保存中断自旋锁的每个例程在一组关联的中断对象的 DIRQL 执行。 因此，驱动程序不能调用**KeAcquireSpinLock**和**KeReleaseSpinLock** ，也不能从其 ISR 或*SynchCritSection*例程调用使用 executive 自旋锁的任何其他例程。 此类调用是一个错误，该错误会导致系统死锁，要求用户重新启动其计算机。 请注意，如果驱动程序的 ISR 或*SynchCritSection*例程调用**ExInterlocked*Xxx*list**例程，则驱动程序无法重复使用在调用 Ke xxx 时传递到**ExInterlocked*xxx*列表**例程的自旋锁。 **旋转锁**或**Ke*xxx*旋转锁*xxx*DpcLevel**支持例程。

如果驱动程序具有 multivector ISR 或多个 ISR，则其例程可以在任何 IRQL 上执行时调用[**KeSynchronizeExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution) ，直到连接时为关联中断对象指定的*SynchronizeIrql*值。

 

 





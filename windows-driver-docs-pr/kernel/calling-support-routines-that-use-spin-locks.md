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
ms.openlocfilehash: 71f742d2d0eaea2dfb1a084c1dc48a98d822ef85
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90102910"
---
# <a name="calling-support-routines-that-use-spin-locks"></a>调用使用自旋锁的支持例程





调用 [**KeAcquireSpinLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock) 或 [**KeAcquireInStackQueuedSpinLock**](/previous-versions/windows/hardware/drivers/ff551899(v=vs.85)) 会将当前处理器上的 IRQL 设置为调度 \_ 级别，直到对 [**KeReleaseSpinLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock) 或 [**KeReleaseInStackQueuedSpinLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlock) 的相应调用还原上一个 IRQL。 因此， &lt; \_ 在调用 **KeAcquireSpinLock** 或 **KeAcquireInStackQueuedSpinLock**时，驱动程序必须在 IRQL = 调度级别执行。

[**KeAcquireSpinLockAtDpcLevel**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlockatdpclevel)、 [**KeAcquireInStackQueuedSpinLockAtDpcLevel**](/previous-versions/windows/hardware/drivers/ff551908(v=vs.85))、 [**KeReleaseInStackQueuedSpinLockFromDpcLevel**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlockfromdpclevel)和[**KeReleaseSpinLockFromDpcLevel**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlockfromdpclevel)的调用方运行速度更快，因为它们已经在 IRQL = 调度级别运行， \_ 因此这些支持例程不需要在当前处理器上重置 IRQL。 因此，在 **KeAcquireSpinLockAtDpcLevel** 或 **KeAcquireInStackQueuedSpinLockAtDpcLevel** 的情况下运行时，大多数 Windows 平台会出现严重错误 \_ 。 调用**KeReleaseSpinLockFromDpcLevel**时，释放通过**KeAcquireSpinLock**获取的旋转锁也是错误的，因为调用方的原始 IRQL 不会还原。

保存执行自旋锁的例程（如<strong>ExInterlocked*Xxx</strong><em>）通常以 IRQL = 调度级别执行， \_ 直到它们释放旋转锁并将控制返回给调用方。但是，只要 ISR 和 ExInterlocked 例程以独占方式使用传递给例程的自旋锁，驱动程序的 [</em> InterruptService <em>](/windows-hardware/drivers/ddi/wdm/nc-wdm-kservice_routine) 例程和 [</em> SynchCritSection 例程就可能 <em>](/windows-hardware/drivers/ddi/wdm/nc-wdm-ksynchronize_routine) (在 DIRQL) 运行的例程和例程调用某些**ExInterlocked</em>Xxx** *例程，如**SynchCritSection*xxx*列表**例程。 *SynchCritSection*

保存中断自旋锁的每个例程在一组关联的中断对象的 DIRQL 执行。 因此，驱动程序不能调用 **KeAcquireSpinLock** 和 **KeReleaseSpinLock** ，也不能从其 ISR 或 *SynchCritSection* 例程调用使用 executive 自旋锁的任何其他例程。 此类调用是一个错误，该错误会导致系统死锁，要求用户重新启动其计算机。 请注意，如果驱动程序的 ISR 或*SynchCritSection*例程调用**ExInterlocked*Xxx*list**例程，则驱动程序无法重复使用在调用**Ke*xxx*旋转锁**或**Ke*xxx*旋转锁*Xxx*DpcLevel**支持例程时传递到**ExInterlocked*Xxx*列表**例程的自旋锁。

如果驱动程序具有 multivector ISR 或多个 ISR，则其例程可以在任何 IRQL 上执行时调用 [**KeSynchronizeExecution**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution) ，直到连接时为关联中断对象指定的 *SynchronizeIrql* 值。


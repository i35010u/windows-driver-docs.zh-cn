---
title: 使用自旋锁时防止错误和死锁
description: 使用自旋锁时防止错误和死锁
ms.assetid: 1df563e6-7ad2-4684-9778-ffa1b845ac31
keywords:
- 死锁 WDK 内核
- 递归 WDK 内核
- 嵌套旋转锁获取 WDK 内核
- 可分页数据锁定 WDK 内核
- 旋转锁定 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3be9f660a1770f2501170681bf8ec367968c20d7
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184989"
---
# <a name="preventing-errors-and-deadlocks-while-using-spin-locks"></a>使用自旋锁时防止错误和死锁





尽管驱动程序例程持有自旋锁，但它在不关闭系统的情况下不会导致硬件例外或引发软件异常。 换句话说，驱动程序的 ISR 和驱动程序在对[**KeSynchronizeExecution**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution)的调用中提供的任何*SynchCritSection*例程不得导致错误或陷阱（如页面错误或算术异常），并且无法引发软件异常。 调用 [**KeAcquireSpinLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock) 或 [**KeAcquireInStackQueuedSpinLock**](/previous-versions/windows/hardware/drivers/ff551899(v=vs.85)) 的例程也不会导致硬件异常或引发软件异常，直到它释放了其 executive 旋转锁，并且不再以 IRQL = 调度 \_ 级别运行。

### <a name="pageable-data-and-support-routines"></a>可分页的数据和支持例程

持有自旋锁时，驱动程序不能调用访问可分页数据的例程。 请记住，当且仅当在严格小于调度级别的 IRQL 执行时，驱动程序可以调用访问可分页数据的某些支持例程 \_ 。 此 IRQL 限制会阻止在持有自旋锁的情况下调用这些支持例程。 对于任何特定支持例程的 IRQL 要求，请参阅例程的参考页。

### <a name="recursion"></a>递归

尝试以递归方式获取旋转锁将保证会导致死锁：在第二个实例化旋转时，尝试获取同一旋转锁时，递归例程的包含实例化无法释放旋转锁。

以下准则说明了如何对递归例程使用自旋锁：

-   在持有自旋锁时，递归例程不能调用自身，也不能尝试在后续调用中获取相同的自旋锁。

-   当递归例程持有自旋锁时，如果递归可能导致死锁或可能导致调用方持有自旋锁的时间超过25微秒，则另一个驱动程序例程不得调用递归例程。

有关递归驱动程序例程的详细信息，请参阅 [使用内核堆栈](using-the-kernel-stack.md)。

### <a name="nested-spin-lock-acquisitions"></a>嵌套旋转锁获取

如果尝试获取第二个旋转锁，同时保持另一个自旋锁，则可能会导致死锁或驱动程序性能不佳。

以下准则说明了驱动程序应如何保存自旋锁：

-   驱动程序不得调用使用旋转锁定的支持例程，除非无法发生死锁。

-   即使不发生死锁，驱动程序也不应调用使用自旋锁的支持例程，除非替代编码技术无法提供类似的驱动程序性能和功能。

-   如果驱动程序进行嵌套调用以获取旋转锁，则必须始终在每次获取自旋锁时按相同顺序获取该锁。 此顺序有助于避免死锁。

一般情况下，应避免使用嵌套自旋锁来保护重叠子集或共享数据和资源的离散集。 考虑当驱动程序使用两个执行自旋锁来保护离散资源（例如一对可能由各种驱动程序例程单独设置并进行设置的计时器对象）时可能发生的情况。 该驱动程序会在 SMP 计算机中间歇性地死锁，每两个例程（每个例程包含一个旋转锁）尝试获取其他旋转锁。

有关获取嵌套自旋锁的详细信息，请参阅 [锁、死锁和同步](https://go.microsoft.com/fwlink/p/?linkid=57456 )。

 


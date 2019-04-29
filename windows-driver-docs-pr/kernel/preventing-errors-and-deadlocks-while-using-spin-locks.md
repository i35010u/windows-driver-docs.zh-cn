---
title: 使用自旋锁时防止错误和死锁
description: 使用自旋锁时防止错误和死锁
ms.assetid: 1df563e6-7ad2-4684-9778-ffa1b845ac31
keywords:
- 死锁 WDK 内核
- 递归 WDK 内核
- 嵌套的自旋锁获取 WDK 内核
- 可分页数据锁定 WDK 内核
- 数值调节钮锁 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: eedd8ec0e6d377870830c91723588da17b1e36ee
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369131"
---
# <a name="preventing-errors-and-deadlocks-while-using-spin-locks"></a>使用自旋锁时防止错误和死锁





驱动程序例程持有旋转锁，虽然它不能导致硬件异常或引发软件异常，而没有导致系统停止运行。 换而言之，驱动程序的 ISR 和任何*SynchCritSection*驱动程序的调用中提供的例程[ **KeSynchronizeExecution** ](https://msdn.microsoft.com/library/windows/hardware/ff553302)必须不会导致错误或陷阱，如页错误或算术异常，并在不能引发软件异常。 调用的例程[ **KeAcquireSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff551917)或[ **KeAcquireInStackQueuedSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff551899)也不会导致硬件异常或引发软件异常，直到它现发布其 executive 旋转锁，已停止运行在 IRQL = 调度\_级别。

### <a name="pageable-data-and-support-routines"></a>可分页的数据和支持例程

同时保留旋转锁，驱动程序不能调用例程，访问可分页的数据。 请记住，驱动程序可以调用访问可分页的数据，当且仅当执行在 IRQL 严格小于调度时出现其调用某些支持例程\_级别。 此 IRQL 限制使该列不能调用这些例程支持在持有自旋锁。 有关任何特定的支持例程的 IRQL 要求，请参阅例程的参考页。

### <a name="recursion"></a>递归

尝试获取数值调节钮锁以递归方式保证导致死锁： 的递归例程的保存实例化不能同时旋转，第二个实例化，尝试获取同一个数值调节钮锁释放自旋锁。

以下准则介绍了如何通过递归例程使用自旋锁：

-   递归例程必须自行调用，同时保留旋转锁，或必须尝试获取同一个数值调节钮锁的后续调用。

-   虽然递归例程持有旋转锁，另一个驱动程序例程如果递归可能会导致死锁不能调用的递归例程，或可能会导致调用方持有的时间超过 25 微秒为单位自旋锁。

有关驱动程序的递归例程的详细信息，请参阅[使用内核堆栈](using-the-kernel-stack.md)。

### <a name="nested-spin-lock-acquisitions"></a>嵌套的自旋锁获得

尝试获取第二个旋转锁按住另一个旋转锁的同时也可能导致死锁或较差的驱动程序性能。

以下指导原则描述如何驱动程序应保存自旋锁：

-   该驱动程序必须调用使用旋转锁，除非不能出现死锁的支持例程。

-   即使不能出现死锁，该驱动程序不应调用使用旋转锁，除非备用编程技术无法提供类似的驱动程序性能和功能的支持例程。

-   如果驱动程序进行嵌套的调用以获取数值调节钮的锁，则始终必须获取的相同顺序自旋锁获得每个时间。 此顺序有助于避免死锁。

一般情况下，避免使用嵌套的自旋锁来保护重叠的子集或离散共享的数据集和资源。 请考虑会发生什么如果驱动程序使用两个 executive 自旋锁来保护离散的资源，如对计时器对象的可能设置单独和共同的各种驱动程序例程。 该驱动程序会导致死锁间歇性地在 SMP 计算机中，只要两个例程，每个持有一个数值调节钮锁，使任一尝试获取其他自旋锁。

获取嵌套的自旋锁的详细信息，请参阅[锁、 死锁和同步](https://go.microsoft.com/fwlink/p/?linkid=57456 )。

 

 





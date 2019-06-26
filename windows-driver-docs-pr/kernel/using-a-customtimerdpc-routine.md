---
title: 使用 CustomTimerDpc 例程
description: 使用 CustomTimerDpc 例程
ms.assetid: e95d01a2-4d13-40d2-aeb0-44c45e4a49f5
keywords:
- 计时器对象 WDK 内核，CustomTimerDpc 例程
- CustomTimerDpc
- 禁用计时器对象
- 计时器对象 WDK 内核，禁用
- 定期计时器 WDK 内核
- 队列计时器对象
- 计时器对象 WDK 内核，过期时间
- 计时器过期 WDK 内核
- 过期的计时器 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 81dde0f2ffee24e2e0e0bef4cbed206bd3fe2df8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382934"
---
# <a name="using-a-customtimerdpc-routine"></a>使用 CustomTimerDpc 例程





若要禁用以前设置计时器对象时，驱动程序调用[ **KeCancelTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kecanceltimer)。 此例程从系统的计时器队列中移除计时器对象。 通常情况下，计时器对象未设置为终止状态并*CustomTimerDpc*例程不排队等待执行。 但是，如果即将过期的计时器时**KeCancelTimer**调用时，可能会发生到期之前**KeCancelTimer**有机会访问队列的时间，在这种情况下将发出信号和 DPC 队列会出现。

撤回[ **KeSetTimer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesettimer)或[ **KeSetTimerEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesettimerex)，与以前指定*计时器*和*Dpc*指针之前以前指定的时间间隔到期，将产生以下影响：

-   在内核中从计时器队列中，而无需将对象设置为终止状态或队列移除计时器对象*CustomTimerDpc*例程。

-   内核构思在计时器队列中，使用新的计时器对象*DueTime*值。

针对不同用途使用相同的计时器对象可能导致争用状况或严重的驱动程序错误。 例如，假定一个驱动程序指定单一计时器对象同时设置为调用*CustomTimerDpc*例程并设置在驱动程序专用的线程中等待。 每当在驱动程序专用的线程调用**KeSetTimer**， **KeSetTimerEx**，或**KeCancelTimer**对于常见的计时器对象，该线程将取消对的调用*CustomTimerDpc*例程，如果计时器对象已排队等待*CustomTimerDpc*调用。

如果驱动程序包含*CustomTimerDpc*例程，以及等待计时器对象在 nonarbitrary 线程上下文中，它应：

-   永远不会使用一个线程上下文相关计时器对象在 nonarbitrary 线程上下文中，反之亦然。

-   每个分配单独的计时器对象*CustomTimerDpc*例程。 驱动程序线程或 nonarbitrary 线程上下文中调用的驱动程序例程的每个集应具有其自己的"可等待"计时器对象集。

如果您使用*CustomTimerDpc*例程，请仔细选择的时间间隔，驱动程序将对的调用中传递**KeSetTimer**或**KeSetTimerEx**。 此外，考虑到调用的所有可能的影响**KeCancelTimer**与使此调用，特别是在 SMP 平台的任何驱动程序例程从相同的计时器对象。

请记住以下这一事实有关*CustomTimerDpc*例程：

只有一个实例化一个 DPC 对象，该对象表示一个特定的 DPC 例程可以排队等待执行在任何给定时间点。

如果第二个的驱动程序例程调用**KeSetTimer**或**KeSetTimerEx**若要运行相同*CustomTimerDpc*例程由第一个调用方指定的时间间隔过期之前,*CustomTimerDpc*例程仅由第二个调用方指定的时间间隔到期后运行。 在这些情况下， *CustomTimerDpc*不会无需任何工作为其调用第一个例程**KeSetTimer**或**KeSetTimerEx**。

驱动程序具有*CustomTimerDpc*例程和使用定期计时器：

驱动程序不能释放定期计时器从 DPC 例程。 驱动程序可以解除分配仅非周期性计时器从 DPC 例程。

请考虑以下的驱动程序，同时具有一个设计指导原则*CustomDpc*并*CustomTimerDpc*例程：

若要避免出现争用情况，永远不会传递同一*Dpc*指针，指向**KeSetTimer**或**KeSetTimerEx**并[ **KeInsertQueueDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinsertqueuedpc).

换而言之，假设驱动程序的*StartIo*例程调用**KeSetTimer**或**KeSetTimerEx**到队列*CustomTimerDpc*例程，驱动程序的 ISR 调用**KeInsertQueueDpc**同时从具有相同的另一个处理器*Dpc*指针。 处理器上的 IRQL 低于调度时，将运行 DPC 例程\_级别或计时器间隔过期，具体取决于第一个。 准确实首先，一些基本的工作*StartIo*或 DPC 例程将只需删除 ISR。

此外，与完全不同的功能使用由两个标准驱动程序例程 DPC 将具有较差的性能特征与单独*CustomTimerDpc*并*CustomDpc*例程。 必须确定哪些操作来执行，具体取决于导致的条件 DPC *StartIo*例程或 ISR 若要在队列中。 这些条件的 DPC 测试会使用额外的 CPU 周期。

 

 





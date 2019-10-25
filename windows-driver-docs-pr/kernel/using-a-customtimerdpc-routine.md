---
title: 使用 CustomTimerDpc 例程
description: 使用 CustomTimerDpc 例程
ms.assetid: e95d01a2-4d13-40d2-aeb0-44c45e4a49f5
keywords:
- timer 对象 WDK 内核，CustomTimerDpc 例程
- CustomTimerDpc
- 禁用计时器对象
- 计时器对象 WDK 内核，禁用
- 定期计时器内核
- 队列计时器对象
- 计时器对象 WDK 内核，过期
- 计时器过期 WDK 内核
- 过期计时器内核内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: cfaafb79eb94c50c34c2984847e0bad2855e7247
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838374"
---
# <a name="using-a-customtimerdpc-routine"></a>使用 CustomTimerDpc 例程





若要禁用先前设置的 timer 对象，驱动程序将调用[**KeCancelTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kecanceltimer)。 此例程将从系统的计时器队列中移除计时器对象。 通常情况下，timer 对象不会设置为 "已终止" 状态，并且*CustomTimerDpc*例程不会排队等待执行。 但是，如果在调用**KeCancelTimer**时计时器即将过期，则可能会在**KeCancelTimer**有机会访问时间队列之前发生过期，在这种情况下，将会发生信号和 DPC 队列。

在以前指定的时间间隔到期之前，通过之前指定的*计时器*和*Dpc*指针撤回[**KeSetTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesettimer)或[**KeSetTimerEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesettimerex)具有以下效果：

-   内核从计时器队列中删除计时器对象，而不会将对象设置为 "已终止" 状态或对*CustomTimerDpc*例程进行排队。

-   内核使用新的*DueTime*值重新插入计时器队列中的计时器对象。

为不同目的使用相同的计时器对象可能导致争用条件或严重驱动程序错误。 例如，假定驱动程序指定了一个计时器对象，以设置对*CustomTimerDpc*例程的调用，并在驱动程序专用线程中设置等待。 每当驱动程序专用线程为常见计时器对象调用**KeSetTimer**、 **KeSetTimerEx**或**KeCancelTimer**时，如果 timer 对象已排队等候，线程就会取消对*CustomTimerDpc*例程的调用。*CustomTimerDpc*调用。

如果驱动程序具有*CustomTimerDpc*例程，并且还会在 nonarbitrary 线程上下文中等待计时器对象，则应执行以下操作：

-   切勿在 nonarbitrary 线程上下文中使用与线程上下文相关的计时器对象，反之亦然。

-   为每个*CustomTimerDpc*例程分配单独的计时器对象。 在 nonarbitrary 线程上下文中调用的每组驱动程序线程或驱动程序例程应有自己的 "可等待" 计时器对象集。

如果使用*CustomTimerDpc*例程，请仔细选择驱动程序在调用**KeSetTimer**或**KeSetTimerEx**时传递的间隔。 此外，请考虑使用来自任何进行此调用的驱动程序例程（特别是在 SMP 平台上）调用**KeCancelTimer**的所有可能效果。

请记住以下有关*CustomTimerDpc*例程的事实：

在任意给定时刻，只能对表示特定 DPC 例程的 DPC 对象的一个实例化进行排队以便执行。

如果第二个驱动程序例程调用**KeSetTimer**或**KeSetTimerEx**以在第一个调用方指定的间隔过期之前运行相同的*CustomTimerDpc*例程，则仅在此间隔后运行*CustomTimerDpc*例程由第二个调用方指定的已过期。 在这些情况下， *CustomTimerDpc*不会执行第一个例程为**KeSetTimer**或**KeSetTimerEx**的任何工作。

对于具有*CustomTimerDpc*例程并使用定期计时器的驱动程序：

驱动程序无法通过 DPC 例程释放定期计时器。 驱动程序只能从 DPC 例程释放非周期性计时器。

对于同时具有*CustomDpc*和*CustomTimerDpc*例程的驱动程序，请考虑以下设计准则：

若要防止出现争用情况，请不要将同一*Dpc*指针传递到**KeSetTimer**或**KeSetTimerEx**和[**KeInsertQueueDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinsertqueuedpc)。

换句话说，假设驱动程序的*StartIo*例程调用**KeSetTimer**或**KeSetTimerEx**来对*CustomTimerDpc*例程进行排队，驱动程序的 ISR 同时从另一个处理器调用**KeInsertQueueDpc**同一*Dpc*指针。 当处理器上的 IRQL 低于调度\_级别或计时器间隔过期（以先达到的时间为准）时，将运行该 DPC 例程。 第一种方法是， *StartIo*或 ISR 的一些必要工作只是由 DPC 例程丢弃。

此外，具有不同功能的两个标准驱动程序例程使用的 DPC 比单独的*CustomTimerDpc*和*CustomDpc*例程具有更差的性能特征。 DPC 必须确定要执行的操作，具体取决于导致*StartIo*例程或 ISR 将操作排队的情况。 在 DPC 中测试这些条件会使用更多的 CPU 周期。

 

 





---
title: 正在删除系统分配计时器对象
description: 从 Windows 8.1 开始，ExDeleteTimer 例程中删除已通过 ExAllocateTimer 例程的计时器对象。
ms.assetid: 7D119448-3890-4E8F-BC79-7FEB3213B693
keywords:
- ExXxxTimer 例程
- ExAllocateTimer
- ExDeleteTimer
- ExSetTimer
- ExCancelTimer
- ExTimerCallback
- ExTimerDeleteCallback
- EX_TIMER
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 62e5af582c1926f1222f53050f749438548dea06
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546953"
---
# <a name="deleting-a-system-allocated-timer-object"></a>正在删除系统分配计时器对象


从 Windows 8.1 [ **ExDeleteTimer** ](https://msdn.microsoft.com/library/windows/hardware/dn265181)例程中删除已创建的计时器对象[ **ExAllocateTimer** ](https://msdn.microsoft.com/library/windows/hardware/dn265179)例程。 此计时器对象是系统分配[ **EX\_计时器**](https://msdn.microsoft.com/library/windows/hardware/dn265199)结构，其成员是不透明的驱动程序。 删除计时器对象之前，请**ExDeleteTimer**进一步禁用计时器对象上的操作和取消或完成任何挂起的操作可能正在进行中的对象。

驱动程序调用后**ExDeleteTimer**，此例程需要几个步骤以确保它可以安全地删除计时器对象。 首先， **ExDeleteTimer**计时器对象标记为禁用，以防止该驱动程序启动新的计时器操作，使用对象。 禁用计时器对象后，调用[ **ExSetTimer** ](https://msdn.microsoft.com/library/windows/hardware/dn265188)或[ **ExCancelTimer** ](https://msdn.microsoft.com/library/windows/hardware/dn265180)例程会立即返回**FALSE**和会执行任何操作。 此外，对的第二个调用**ExDeleteTimer**返回**FALSE**和会执行任何操作。

下一步， **ExDeleteTimer**检查计时器是否仍处于挂起状态从以前调用**ExDeleteTimer**。 禁用计时器对象不会取消该对象已被禁用之前已设置的计时器。 在上述任一以下两种情况下，禁用该计时器对象后，可能会过期之前已设置的计时器：

-   定期计时器。
-   计时器是单步 （或非周期性） 和尚未过期。

禁用计时器对象后，定期计时器将永远不会超过一次过期。

如果您的驱动程序实现[ *ExTimerCallback* ](https://msdn.microsoft.com/library/windows/hardware/dn265190)回调例程*计时器*保证此例程的参数始终是指向该计时器的有效指针对象 （**EX\_计时器**结构)，即使在计时器过期后禁用该计时器对象。

如果没有计时器处于挂起状态， **ExDeleteTimer**删除计时器对象，并返回而不等待。

如果计时器正在等待何时**ExDeleteTimer**调用时，*取消*并*等待*您的驱动程序提供给此例程的参数值控制例程的行为。 *取消*参数将告知**ExDeleteTimer**是否尝试取消挂起的计时器。 *等待*参数将告知**ExDeleteTimer**是否等待返回，直到删除该计时器对象。

如果*取消*是**FALSE** (在这种情况下，*等待*必须是**FALSE**) 和一个计时器处于挂起状态， **ExDeleteTimer**可让计时器过期之前删除该计时器对象。 在这种情况下， **ExDeleteTimer**标记的计时器对象，以指示它是要删除挂起的计时器过期后 (和任何最后一个回调*ExTimerCallback*例程完成)。 然后**ExDeleteTimer**返回而不等待完成即将到期的计时器或要删除的对象。

如果*取消*是**TRUE**， **ExDeleteTimer**尝试取消挂起的计时器过期之前。 **ExDeleteTimer**将返回**TRUE**如果它已成功取消计时器。 **ExDeleteTimer**将返回**FALSE**如果它不能取消计时器，是一个单步计时器已过期或即将到期的过程中是这种情况。 **ExDeleteTimer**也会返回**FALSE**如果之前已取消 （单步或定期） 计时器**ExDeleteTimer**调用或如果永远不会设置计时器。

如果*取消*是**TRUE**并*等待*是**FALSE**， **ExDeleteTimer**永远不会阻止调用线程。 如果不能立即删除计时器对象， **ExDeleteTimer**标记以指示它是即将过期，挂起的计时器完成后要删除的计时器对象并立即返回，而无需等到为到计时器过期或要删除的对象。

如果*取消*并*等待*都是**TRUE**， **ExDeleteTimer**阻止调用线程，如果不能立即删除计时器对象. **ExDeleteTimer**等待，如有必要，要完成即将到期的计时器以及对驱动程序实现的任何回调*ExTimerCallback*例程完成。 下一步， **ExDeleteTimer**删除该计时器对象并调用[ *ExTimerDeleteCallback* ](https://msdn.microsoft.com/library/windows/hardware/dn265192)例程中，如果该驱动程序实现此例程。 最后， **ExDeleteTimer**返回。

驱动程序可以调用**ExDeleteTimer**来自驱动程序的*ExTimerCallback*例程，运行在 IRQL = 调度\_级别，但该驱动程序必须设置*等待*对此调用中的参数**FALSE**。

作为一个选项，可以实现一个驱动程序*ExTimerDeleteCallback*运行计时器对象删除后的回调例程。 通常情况下， *ExTimerDeleteCallback*例程释放该驱动程序分配以使用计时器对象的任何系统资源。

**ExDeleteTimer**计划驱动程序实现*ExTimerDeleteCallback*日常运行计时器对象删除后，此时此对象的指针将不再有效。 如果*等待*参数是**TRUE**中**ExDeleteTimer**调用的回调*ExTimerDeleteCallback*例程完成之前**ExDeleteTimer**返回。 如果*等待*是**FALSE**，则*ExTimerDeleteCallback*例程之前或之后可能会运行**ExDeleteTimer**返回。

有关详细信息，请参阅[Ex*Xxx*计时器例程和 EX\_计时器对象](exxxxtimer-routines-and-ex-timer-objects.md)。

 

 





---
title: KeXxxTimer 例程、 KTIMER 对象和 dpc 进行标记
description: 从 Windows 2000 开始，一组 KeXxxTimer 例程是可用于管理计时器。
ms.assetid: b58487de-6e9e-45f4-acb8-9233c8718ee2
keywords:
- 计时器 WDK 内核
- 计时器对象 WDK 内核
- 计时器对象 WDK 内核，有关计时器对象
- 延迟的过程调用 WDK 内核
- Dpc WDK 内核
- 内核调度程序对象 WDK，计时器对象
- 调度程序对象 WDK 内核，计时器对象
- 通知计时器 WDK 内核
- 同步计时器 WDK 内核
- KTIMER
- KeXxxTimer 例程
- KeInitializeTimer
- KeInitializeTimerEx
- KeSetTimer
- KeSetTimerEx
- CustomTimerDpc
- 超时间隔 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d53ae173b646788694372d70da1190a4bf6076b6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525212"
---
# <a name="kexxxtimer-routines-ktimer-objects-and-dpcs"></a>KeXxxTimer 例程、 KTIMER 对象和 dpc 进行标记


从 Windows 2000 中，一套**Ke*Xxx*计时器**例程是可用于管理计时器。 这些例程使用计时器对象的基于[ **KTIMER** ](https://msdn.microsoft.com/library/windows/hardware/ff554250)结构。 若要创建计时器对象，驱动程序，首先分配用于存储**KTIMER**结构。 然后，驱动程序调用例程，如[ **KeInitializeTimer** ](https://msdn.microsoft.com/library/windows/hardware/ff552168)或[ **KeInitializeTimerEx** ](https://msdn.microsoft.com/library/windows/hardware/ff552173)初始化此结构。




可以设置一个计时器，只需一次，过期或重复在给定时间间隔后过期。 [**KeSetTimer** ](https://msdn.microsoft.com/library/windows/hardware/ff553286)始终设置将只需一次过期的计时器。 [**KeSetTimerEx** ](https://msdn.microsoft.com/library/windows/hardware/ff553292)接受一个可选*段*参数，指定重复的计时器时间间隔。

一个可选[ *CustomTimerDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542983)例程 （一种延缓的过程调用） 可以与通知计时器或同步计时器相关联。 当在指定的时间间隔到期时，将执行此例程。 有关详细信息，请参阅[使用计时器对象](using-timer-objects.md)。

可以是计时器*通知计时器*或*同步计时器*。

-   时发出信号通知计时器，所有等待线程都都可以满足其等待。 计时器的状态保持终止状态，直到显式重置。

-   同步计时器过期时，其状态设置为用信号通知释放单个等待线程之前。 然后计时器重置为未发出信号状态。

**KeInitializeTimer**始终会创建通知计时器。 **KeInitializeTimerEx**接受*类型*可以为参数**NotificationTimer**或**SynchronizationTimer**。

以下主题提供有关计时器对象和 dpc 进行标记的详细信息：

[使用计时器对象](using-timer-objects.md)
[计时器准确性](timer-accuracy.md)
[注册和队列 CustomTimerDpc 例程](registering-and-queuing-a-customtimerdpc-routine.md)
[提供CustomTimerDpc 上下文信息](providing-customtimerdpc-context-information.md)
[使用 CustomTimerDpc 例程](using-a-customtimerdpc-routine.md)
 

 





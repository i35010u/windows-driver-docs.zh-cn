---
title: ExXxxTimer 例程和 EX_TIMER 对象
description: 从 Windows 8.1 开始，一组全面的 ExXxxTimer 例程是可用于管理计时器。
ms.assetid: 5F2622F5-4D1A-48F4-9FF5-27DEC6109266
keywords:
- 计时器 WDK 内核
- 计时器对象 WDK 内核
- 计时器对象 WDK 内核，有关计时器对象
- 内核调度程序对象 WDK，计时器对象
- 调度程序对象 WDK 内核，计时器对象
- 高分辨率计时器 WDK 内核
- 没有唤醒计时器 WDK 内核
- EX_TIMER
- ExXxxTimer 例程
- ExAllocateTimer
- ExDeleteTimer
- ExSetTimer
- ExCancelTimer
- ExTimerCallback
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0d2d669547bb7559dad9d1cf69c5c8ecfcc63b4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386618"
---
# <a name="exxxxtimer-routines-and-extimer-objects"></a>ExXxxTimer 例程和 EX\_计时器对象


从 Windows 8.1 开始，一套综合的**Ex*Xxx*计时器**例程是可用于管理计时器。 这些例程使用计时器对象的基于[ **EX\_计时器**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)结构。 **Ex*Xxx*计时器**例程是替换**Ke*Xxx*计时器**例程，可从 Windows 2000 开始。 驱动程序用于只能在 Windows 8.1 上运行，并可以使用更高版本的 Windows **Ex*Xxx*计时器**而不是例程**Ke*Xxx*计时器**例程。 继续支持 Windows 8.1 和更高版本的 Windows **Ke*Xxx*计时器**例程。

**Ex*Xxx*计时器**例程拥有由提供的所有重要的功能**Ke*Xxx*计时器**例程。 此外， **Ex*Xxx*计时器**例程都支持两个计时器类型*高分辨率计时器*并*否唤醒计时器*，不是受**Ke*Xxx*计时器**例程。 高分辨率计时器是其过期时间可以指定与准确性更高的系统时钟的默认分辨率受限于其准确性的计时器的计时器。 没有唤醒计时器是避免不必要地唤醒从低功耗状态的处理器的计时器。 有关详细信息，请参阅下列主题：

[高分辨率计时器](high-resolution-timers.md)
[否唤醒计时器](no-wake-timers.md)从 Windows 8.1，以下**Ex*Xxx*计时器**例程都可用：

[**ExAllocateTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatetimer)
[**ExSetTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exsettimer)
[**ExCancelTimer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-excanceltimer) 
 [ **ExDeleteTimer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exdeletetimer) **ExSetTimer**例程可以使用而不是[ **KeSetTimer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesettimer)或[ **KeSetTimerEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesettimerex)例程。 **ExCancelTimer**例程可以使用而不是[ **KeCancelTimer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kecanceltimer)例程。

**ExAllocateTimer**并**ExDeleteTimer**例程具有不能直接**Ke*Xxx*计时器**对应项。 两个例程分配和释放计时器对象。 此计时器对象是系统分配[ **EX\_计时器**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)结构，其成员是不透明的驱动程序。 与此相反，该计时器对象由**Ke*Xxx*计时器**例程是驱动程序分配[ **KTIMER** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)结构。 驱动程序调用[ **KeInitializeTimer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinitializetimer)或[ **KeInitializeTimerEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinitializetimerex)例程来初始化此对象。 **ExAllocateTimer**初始化它再分配计时器对象。 有关详细信息**ExDeleteTimer**，请参阅[删除 System-Allocated 计时器对象](deleting-a-system-allocated-timer-object.md)。

**EX\_计时器**并**KTIMER**结构是可等待对象。 驱动程序调用后**ExSetTimer**， **KeSetTimer**，或**KeSetTimerEx**若要设置一个计时器，该驱动程序可以调用一个例程如[ **KeWaitForSingleObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitforsingleobject)或[ **KeWaitForMultipleObjects** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitformultipleobjects)等待计时器过期。 在计时器过期时，计时器对象发出信号。 驱动程序可以作为一个选项，提供指向驱动程序实现的指针[ *ExTimerCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-ext_callback)或[ *CustomTimerDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542983)回调例程操作系统将调用计时器过期后。

**Ke*Xxx*计时器**例程具有不由提供的两个功能**Ex*Xxx*计时器**例程，但这些功能不需要的大多数驱动程序。

首先， **KTIMER**用作由计时器对象的结构**Ke*Xxx*计时器**例程是驱动程序分配。 该驱动程序可以预分配此对象，以确保该对象可用于甚至在情况下在其中限制资源和内存分配可能会失败。 与之相反，调用**ExAllocateTimer**分配计时器对象可能会失败在资源受限环境中。 但是，一些驱动程序需要设计为在环境中的内存分配失败，操作和大多数驱动程序受益的便利性**ExAllocateTimer**同时分配并初始化计时器对象的例程。

其次，还有没有**Ex*Xxx*计时器**等效于[ **KeReadStateTimer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereadstatetimer)例程，该值指示是否在计时器对象已发出信号的状态。 但是，很少使用此例程。 如有必要，驱动程序，使用**Ex*Xxx*计时器**例程可以检查计时器对象是否处于终止状态通过读取一个布尔值，通过设置*ExTimerCallback*驱动程序提供给的回调例程**ExAllocateTimer**例程。

 

 





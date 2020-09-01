---
title: ExXxxTimer 例程和 EX_TIMER 对象
description: 从 Windows 8.1 开始，可以使用一组全面的 ExXxxTimer 例程来管理计时器。
ms.assetid: 5F2622F5-4D1A-48F4-9FF5-27DEC6109266
keywords:
- 计时器的 WDK 内核
- 计时器对象 WDK 内核
- 计时器对象 WDK 内核，关于计时器对象
- 内核调度程序对象 WDK，计时器对象
- 调度程序对象 WDK 内核，计时器对象
- 高分辨率计时器 WDK 内核
- 无唤醒计时器 WDK 内核
- EX_TIMER
- ExXxxTimer 例程
- ExAllocateTimer
- ExDeleteTimer
- ExSetTimer
- ExCancelTimer
- ExTimerCallback
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8acdbdf385c5d9744db43520148cdf63ba063f93
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190059"
---
# <a name="exxxxtimer-routines-and-ex_timer-objects"></a>ExXxxTimer 例程和 EX \_ 计时器对象


从 Windows 8.1 开始，可以使用一组全面的 **Ex*Xxx*计时器** 例程来管理计时器。 这些例程使用基于 [**EX \_ 计时器**](./eprocess.md) 结构的计时器对象。 **Ex*xxx*计时器**例程是适用于从 Windows 2000 开始的 " **Ke*xxx*计时器**" 例程的替换项。 仅在 Windows 8.1 和更高版本的 Windows 上运行的驱动程序可以使用 **Ex*xxx*计时器** 例程，而不是 **Ke*xxx*计时器** 例程。 Windows 8.1 和更高版本的 Windows 将继续支持 **Ke*Xxx*计时器** 例程。

**Ex*xxx*计时器**例程具有由**Ke*xxx*计时器**例程提供的所有重要功能。 此外， **Ex*xxx*计时器**例程支持不受**Ke*xxx*计时器**例程支持的两种计时器类型、*高分辨率计时器*和*无唤醒计时器*。 高分辨率计时器是计时器，其过期时间可指定为具有比系统时钟默认分辨率限制的计时器更高的精度。 无唤醒计时器是避免不必要地从低功耗状态唤醒处理器的计时器。 有关详细信息，请参阅下列主题：

[高分辨率计时器](high-resolution-timers.md) 
[无唤醒计时器](no-wake-timers.md)从 Windows 8.1 开始，可以使用以下**Ex*Xxx*计时器**例程：

[**ExAllocateTimer**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatetimer) 
[**ExSetTimer**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exsettimer) 
[**ExCancelTimer**](/windows-hardware/drivers/ddi/wdm/nf-wdm-excanceltimer) 
[**ExDeleteTimer**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeletetimer)可以使用**ExSetTimer**例程，而不是[**KeSetTimer**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesettimer)或[**KeSetTimerEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesettimerex)例程。 可以使用 **ExCancelTimer** 例程，而不是 [**KeCancelTimer**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kecanceltimer) 例程。

**ExAllocateTimer**和**ExDeleteTimer**例程没有直接的**Ke*Xxx*计时器**对应项。 这两个例程分配并释放计时器对象。 此计时器对象是系统分配的 [**EX \_ 计时器**](./eprocess.md) 结构，其成员对于驱动程序是不透明的。 与此相反，" **Ke*Xxx*计时器** " 例程使用的 timer 对象是驱动程序分配的 [**KTIMER**](./eprocess.md) 结构。 驱动程序调用 [**KeInitializeTimer**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializetimer) 或 [**KeInitializeTimerEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializetimerex) 例程来初始化此对象。 **ExAllocateTimer** 初始化它分配的计时器对象。 有关 **ExDeleteTimer**的详细信息，请参阅 [删除系统分配的计时器对象](deleting-a-system-allocated-timer-object.md)。

**EX \_TIMER** 和 **KTIMER** 结构是可等待对象。 驱动程序调用 **ExSetTimer**、 **KeSetTimer**或 **KeSetTimerEx** 来设置计时器之后，驱动程序可以调用一个例程，如 [**KeWaitForSingleObject**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject) 或 [**KeWaitForMultipleObjects**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitformultipleobjects) ，以等待计时器过期。 计时器过期时，将终止 timer 对象。 作为选项，驱动程序可以提供一个指针，指向在计时器过期后操作系统调用的驱动程序实现的 [*ExTimerCallback*](/windows-hardware/drivers/ddi/wdm/nc-wdm-ext_callback) 或 [*CustomTimerDpc*](https://msdn.microsoft.com/library/windows/hardware/ff542983) 回调例程。

**Ke*xxx*计时器**例程有两个功能，这些功能不由**Ex*xxx*计时器**例程提供，但大多数驱动程序都不需要这些功能。

首先，由**Ke*Xxx*计时器**例程用作计时器对象的**KTIMER**结构是由驱动程序分配的。 驱动程序可以预分配此对象，以确保即使在资源受到限制并且内存分配可能会失败的情况下，对象也可用。 相反，在资源受限的环境中，对 **ExAllocateTimer** 的调用来分配计时器对象可能会失败。 但是，很少有驱动程序需要设计为在内存分配失败的环境中运行，而大多数驱动程序都从 **ExAllocateTimer** 例程的便利性中获益，这两种情况都可以分配和初始化 timer 对象。

其次，没有与[**KeReadStateTimer**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereadstatetimer)例程等效的**Ex*Xxx*计时器**，这指示计时器对象是否处于终止状态。 但是，此例程很少使用。 如有必要，使用**Ex*Xxx*计时器**例程的驱动程序可以通过读取由驱动程序提供给**ExAllocateTimer**例程的*ExTimerCallback*回调例程设置的布尔值来检查计时器对象是否处于终止状态。

 


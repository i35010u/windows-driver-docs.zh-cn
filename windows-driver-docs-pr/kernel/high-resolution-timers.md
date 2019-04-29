---
title: 高解析度计时器
description: 从 Windows 8.1，驱动程序可以使用 ExXxxTimer 例程用于管理高分辨率计时器。
ms.assetid: B8F2B28C-A02B-4015-B392-3D30BC0229B8
keywords:
- 高分辨率计时器
- 计时器准确性
- 计时器分辨率
- 系统时钟粒度
- EX_TIMER_HIGH_RESOLUTION
- ExXxxTimer 例程
- ExQueryTimerResolution
- ExSetTimerResolution
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 068b52e5f39eb1701ad3a7e945ac91869a2c43a4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386255"
---
# <a name="high-resolution-timers"></a>高解析度计时器


从 Windows 8.1 开始，可以使用驱动程序[ **Ex*Xxx*计时器**](exxxxtimer-routines-and-ex-timer-objects.md)例程用于管理高分辨率计时器。 高分辨率计时器的准确性仅受支持的最大的系统时钟分辨率。 与此相反，仅限于默认系统时钟分辨率的计时器是明显不太准确。

但是，高分辨率计时器需要到系统时钟中断-至少，暂时 — 出现在较高的速率，往往会增加功率消耗。 因此，驱动程序应使用高分辨率计时器，仅当计时器准确性至关重要，并且在所有其他情况下使用默认解析计时器。

若要创建高分辨率计时器，WDM 驱动程序调用[ **ExAllocateTimer** ](https://msdn.microsoft.com/library/windows/hardware/dn265179)例程和集 EX\_计时器\_高\_中的解析标志*属性*参数。 当驱动程序调用[ **ExSetTimer** ](https://msdn.microsoft.com/library/windows/hardware/dn265188)例程设置高分辨率计时器，操作系统会增加必要时，系统时钟的分辨率，以便在该时间计时器过期的详细信息准确地对应中指定的名义上已过期时间*DueTime*并*段*参数。

内核模式驱动程序框架 (KMDF) 驱动程序可以调用[ **WdfTimerCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff550050)方法来创建高分辨率计时器。 在此调用中，驱动程序将传递一个指向[ **WDF\_计时器\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff552519)结构作为参数。 若要创建高分辨率计时器，驱动程序集**UseHighResolutionTimer**到此结构的成员**TRUE**。 此成员是从 Windows 8.1 和 KMDF 版本 1.13 开始结构的一部分。

## <a name="controlling-timer-accuracy"></a>控制计时器准确性


例如，对于在 x86 上运行的 Windows 处理器，系统时钟计时周期之间的默认间隔通常是大约 15 毫秒，系统时钟计时周期之间的最小间隔为大约 1 毫秒。 因此，默认高分辨率计时器的过期时间 (其中**ExAllocateTimer**创建如果 EX\_计时器\_高\_解析标志未设置) 可以在大约 15 只能与控制毫秒为单位，但高分辨率计时器的过期时间可以在一毫秒以下控制到。

如果驱动程序指定相对过期时间的默认分辨率计时器，计时器将过期到大约 15 毫秒，前面或更高版本比指定的过期时间。 如果驱动程序指定相对过期时间的高分辨率计时器，计时器会晚有关毫秒后指定的过期时间，但它永不过期提前过期。 有关系统时钟分辨率和计时器准确性之间的关系的详细信息，请参阅[计时器准确性](timer-accuracy.md)。

如果不设置了任何高分辨率计时器，通常运行操作系统的系统时钟在其默认速率。 但是，如果设置了一个或多个高分辨率计时器，操作系统可能需要最少部分的这些计时器过期之前的时间以其最大速率运行系统时钟。

若要避免不必要地增加功率消耗，操作系统在其最大速率仅在需要以满足高分辨率计时器的计时要求时运行系统时钟。 例如，如果高分辨率计时器是周期性的且其期跨越多个默认系统时钟计时周期，操作系统可能运行系统时钟在其最大速率仅在紧贴每个过期的计时器周期的一部分。 计时器周期的其余部分，将系统时钟在其默认速率运行。

若要防止过量的功率消耗，驱动程序应避免将长时间运行的高分辨率计时器的周期设置为小于系统时钟计时周期之间的默认间隔值。 否则，操作系统被迫持续运行的系统时钟在其最大速率。

从 Windows 8 开始，驱动程序可以调用[ **ExQueryTimerResolution** ](https://msdn.microsoft.com/library/windows/hardware/dn275969)例程，以获取支持的系统时钟的计时器分辨率的范围。

## <a name="comparison-to-exsettimerresolution"></a>与 ExSetTimerResolution 之间的比较


从 Windows 2000 开始，驱动程序可以调用[ **ExSetTimerResolution** ](calling-exsettimerresolution-while-processing-a-power-irp.md)例程，以更改连续系统时钟中断的时间间隔。 例如，驱动程序可以调用此例程，以将系统时钟从其默认速率更改为其最大速率，以提高计时器的精确度。 但是，使用**ExSetTimerResolution**相比于使用高分辨率计时器创建的几个缺点**ExAllocateTimer**。

首先，在调用**ExSetTimerResolution**若要暂时增加的系统时钟速率，驱动程序必须调用**ExSetTimerResolution**还原到其默认速率的系统时钟的第二个时机。 否则，系统时钟计时器持续生成可能会导致过量的功率消耗的最大速率的中断。

其次，驱动程序，使用**ExSetTimerResolution**例程不能与操作系统为高分辨率计时器，有效地优化其临时使用的更高的系统时钟速率。 因此，系统时钟在花费的时间超出必须严格限制，以最大速率运行。

第三，如果同时使用多个驱动程序**ExSetTimerResolution**若要提高计时器准确性，系统时钟可能会在运行其最大速率很长一段。 与此相反，操作系统全局协调的操作的多个高分辨率计时器，以便以最大速率仅在需要以满足这些计时器的计时要求时运行的系统时钟。

最后，使用**ExSetTimerResolution**是本质上是比使用高分辨率计时器不太准确。 驱动程序调用后**ExSetTimerResolution**若要增加到其最大速率，这通常是有关 / 毫秒为单位的时钟计时周期，系统时钟驱动程序可能调用一个例程如[ **KeSetTimerEx**](https://msdn.microsoft.com/library/windows/hardware/ff553292)设置计时器。 如果在此调用中，该驱动程序指定了相对过期时间，可以最多过期计时器有关早于或晚于指定的过期时间以毫秒为单位。 但是，如果为高分辨率计时器指定相对过期时间，则计时器过期最多一毫秒以下有关晚于指定的过期时间，但它永远不会提前过期。

 

 





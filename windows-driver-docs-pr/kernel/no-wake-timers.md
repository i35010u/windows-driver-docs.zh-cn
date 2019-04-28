---
title: 无唤醒功能的计时器
description: 从 Windows 8.1，驱动程序可以使用无唤醒计时器以避免不必要地唤醒从低功耗状态的处理器。
ms.assetid: 04CD107B-F196-4FF8-A423-C43CAA9A7EBD
keywords:
- 没有唤醒计时器
- ExXxxTimer 例程
- EX_TIMER_NO_WAKE
- EX_TIMER_UNLIMITED_TOLERANCE
- coalescable 计时器
- 计时器合并
- KeSetCoalescableTimer
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e69f335ee69c22d6385d7a8130b64c1b745a59b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341968"
---
# <a name="no-wake-timers"></a>无唤醒功能的计时器


从 Windows 8.1，驱动程序可以使用无唤醒计时器以避免不必要地唤醒从低功耗状态的处理器。 通过在低功耗状态中保留的处理器，否唤醒计时器降低了电源消耗，并将扩展的平板电脑或其他移动计算机可以在电池电量运行的时间。

计时器将过期仅当处理器处于活动、 正在运行状态。 如果计时器达到其过期时间时处理器处于低功耗状态，并且需要立即过期计时器，计时器必须唤醒处理器。 但是，当否唤醒计时器达到其过期时间，并在处理器处于低功耗状态，此计时器等待处理器唤醒计时器以外的某种原因才过期。 作为一个选项，驱动程序可以指定最大延迟容差为否唤醒计时器，以便如果处理器不会不会唤醒 （适用于某些其他原因） 最大延迟的公差范围内计时器的过期时间后，计时器唤醒处理器。

驱动程序可以使用无唤醒计时器启动需要仅当在处理器处于活动状态时执行的非关键操作。 例如，驱动程序可能会使用无唤醒计时器定期刷新到文件的累积的状态信息从内存缓冲区。 此状态信息描述了该驱动程序执行仅当处理器处于活动状态时的处理工作。 当处理器处于低功耗状态时，生成的任何状态信息，并且没有无需唤醒处理器。

若要创建无唤醒计时器，WDM 驱动程序调用[ **ExAllocateTimer** ](https://msdn.microsoft.com/library/windows/hardware/dn265179)例程。 在此调用中，驱动程序设置 EX\_计时器\_否\_唤醒标志位*特性*参数。

若要设置无唤醒计时器过期在某个截止时间，该驱动程序调用[ **ExSetTimer** ](https://msdn.microsoft.com/library/windows/hardware/dn265188)例程。 在此调用，该驱动程序可以指定到达其过期时间之前计时器唤醒处理器后无唤醒计时器应等待多长时间。 该驱动程序将写入到此容许延迟时间**NoWakeTolerance**中的成员[ **EXT\_设置\_参数**](https://msdn.microsoft.com/library/windows/hardware/dn265196)结构驱动程序将作为输入参数传递**ExSetTimer**例程。 如果驱动程序设置**NoWakeTolerance**为特殊值，例如成员\_计时器\_UNLIMITED\_容差，计时器永远不会唤醒处理器，并因此，不能过期之前处理器唤醒某些其他原因。

内核模式驱动程序框架 (KMDF) 驱动程序或用户模式驱动程序框架 (UMDF) 驱动程序可以调用[ **WdfTimerCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff550050)方法来创建无唤醒计时器。 在此调用中，驱动程序将传递一个指向[ **WDF\_计时器\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff552519)结构作为参数。 若要创建一个永远不会唤醒，处理器的否唤醒计时器，驱动程序设置**TolerableDelay**到此结构的成员**TolerableDelayUnlimited**常量。 开始使用 Windows 8.1 和 KMDF 版本 1.13 或 UMDF 2.0 支持此常量。

## <a name="comparison-to-coalescable-timers"></a>与 coalescable 计时器之间的比较


[ **KeSetCoalescableTimer** ](https://msdn.microsoft.com/library/windows/hardware/ff553249)例程在 Windows 7 中引入。 此例程可以指定多少容差，以允许在计时器的过期时间中的驱动程序。 通常，操作系统可以使用此信息来将两个或多个计时器中断合并成单个中断。 如果多个计时器的过期时间是笔悬停于每个另一种其容错时段重叠，重叠区域中的单个计时器中断可满足所有这些计时器的计时要求。

计时器合并的主要好处是，它将扩展处理器可保留在计时器过期时间之间的低电源状态的时间。 因此，驱动程序使用计时器合并和否唤醒计时器针对类似目的。

但是，coalesceable 计时器在行为上以不同方式否唤醒计时器。 具体而言，容许延迟为否唤醒计时器指定适用处理器时才处于低功耗状态，而无论是否在处理器处于低功耗状态适用 coalescable 计时器的过期日期为指定的公差。 Coalescable 计时器，驱动程序会增加的容错，允许的过期时间，以减少计时器唤醒处理器，但增加了容差具有副作用的减小计时器的准确性，当处理器的可能性处于活动状态。 与此相反，为否唤醒计时器指定可容忍延迟不会影响计时器的准确性，当处理器处于活动状态。 对于许多驱动程序，否唤醒计时器可能是更好的方法来降低功率消耗。

 

 





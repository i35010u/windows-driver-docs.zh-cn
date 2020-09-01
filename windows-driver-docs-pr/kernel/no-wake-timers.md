---
title: 无唤醒功能的计时器
description: 从 Windows 8.1 开始，驱动程序可以使用无唤醒计时器，以避免不必要地从低功耗状态唤醒处理器。
ms.assetid: 04CD107B-F196-4FF8-A423-C43CAA9A7EBD
keywords:
- 无唤醒计时器
- ExXxxTimer 例程
- EX_TIMER_NO_WAKE
- EX_TIMER_UNLIMITED_TOLERANCE
- coalescable 计时器
- 计时器合并
- KeSetCoalescableTimer
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5823fcc28c86e419ac698962822da7a536f6358
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188849"
---
# <a name="no-wake-timers"></a>无唤醒功能的计时器


从 Windows 8.1 开始，驱动程序可以使用无唤醒计时器，以避免不必要地从低功耗状态唤醒处理器。 通过使处理器处于低功耗状态，无唤醒计时器可减少能耗，并延长平板电脑或其他移动计算机在电池电量上可以运行的时间。

仅当处理器处于活动的运行状态时，计时器才会过期。 如果计时器在处理器处于低功耗状态时达到其过期时间，而计时器需要立即过期，则计时器必须唤醒处理器。 但是，当一个无唤醒计时器达到其过期时间并且处理器处于低功耗状态时，此计时器将等待过期，直到处理器唤醒，因为某些原因不是计时器。 作为一个选项，驱动程序可以指定无唤醒计时器的最大延迟容差，以便在计时器过期时间后，如果处理器不能唤醒 () 在最大延迟范围内，则计时器唤醒处理器。

驱动程序可以使用无唤醒计时器来启动非关键操作，这些操作只需在处理器处于活动状态时执行。 例如，驱动程序可能使用非唤醒计时器定期将累计状态信息从内存缓冲区刷新到文件中。 此状态信息介绍了驱动程序在处理器处于活动状态时所执行的处理工作。 当处理器处于低功耗状态时，不会生成任何状态信息，并且无需唤醒处理器。

若要创建无唤醒计时器，WDM 驱动程序将调用 [**ExAllocateTimer**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatetimer) 例程。 在此调用中，驱动程序在 \_ \_ Attributes 参数中设置 EX 计时器 NO \_ 唤醒*Attributes*标志位。

若要将非唤醒计时器设置为在某个截止时间过期，驱动程序将调用 [**ExSetTimer**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exsettimer) 例程。 在此调用中，驱动程序可以指定在计时器唤醒处理器之前，不唤醒计时器在到达其到期时间之前应等待的时间。 驱动程序将此容许延迟时间写入[**EXT \_ SET \_ 参数**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_ext_set_parameters_v0)结构中的**NoWakeTolerance**成员，驱动程序将该结构作为输入参数传递到**ExSetTimer**例程。 如果驱动程序将 **NoWakeTolerance** 成员设置为特殊值 EX \_ 计时器 \_ 无限制 \_ 容差，则计时器将永远不会唤醒处理器，因此，在由于其他原因而使处理器唤醒之前，无法过期。

内核模式驱动程序框架 (KMDF) 驱动程序或用户模式驱动程序框架 (UMDF) 驱动程序可以调用 [**WdfTimerCreate**](/windows-hardware/drivers/ddi/wdftimer/nf-wdftimer-wdftimercreate) 方法来创建无唤醒计时器。 在此调用中，驱动程序将一个指针作为参数传递给 [**WDF \_ 计时器 \_ 配置**](/windows-hardware/drivers/ddi/wdftimer/ns-wdftimer-_wdf_timer_config) 结构。 若要创建永不唤醒处理器的无唤醒计时器，驱动程序将此结构的 **TolerableDelay** 成员设置为 **TolerableDelayUnlimited** 常量。 从 Windows 8.1 和 KMDF 版本1.13 或 UMDF 2.0 开始，此常量受支持。

## <a name="comparison-to-coalescable-timers"></a>与 coalescable 计时器的比较


[**KeSetCoalescableTimer**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetcoalescabletimer)例程是在 Windows 7 中引入的。 使用此例程，驱动程序可以指定在计时器过期时间内允许的容差。 操作系统经常会使用此信息将两个或更多计时器中断合并为一个中断。 如果多个计时器的过期时间彼此接近于其容错窗口重叠，则重叠区域中的单个计时器中断可以满足所有这些计时器的计时要求。

计时器合并的主要优点是它扩展了处理器在计时器过期时间间隔内处于低功耗状态的时间。 因此，驱动程序使用计时器合并和无唤醒计时器来实现类似目的。

但是，coalesceable 计时器的行为不同于无唤醒计时器。 具体而言，为不唤醒计时器指定的容许延迟仅适用于处理器处于低功耗状态的情况，而无论处理器是否处于低功耗状态，coalescable 计时器的过期时间都适用。 对于 coalescable 计时器，驱动程序可以增加过期时间的容差量，以减少计时器唤醒处理器的可能性，但是增加公差的副作用是在处理器处于活动状态时降低计时器准确性。 与此相反，为无唤醒计时器指定的可容忍延迟不会影响处理器处于活动状态时的计时器准确性。 对于许多驱动程序，无唤醒计时器可能是降低功率消耗的更好方法。

 


---
title: 高解析度计时器
description: 从 Windows 8.1 开始，驱动程序可以使用 ExXxxTimer 例程来管理高分辨率计时器。
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
ms.openlocfilehash: ed7b352d1beeecadc35b66b534a2e935ab45814a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817711"
---
# <a name="high-resolution-timers"></a>高解析度计时器


从 Windows 8.1 开始，驱动程序可以使用 [**Ex *Xxx* 计时器**](exxxxtimer-routines-and-ex-timer-objects.md) 例程来管理高分辨率计时器。 高分辨率计时器的准确性仅受系统时钟支持的最大分辨率。 与此相反，限制为默认系统时钟解析的计时器会显著降低。

但是，高分辨率计时器需要系统时钟中断（至少是暂时的）以更高的速率发生，这往往会增加功率消耗。 因此，只有在计时器准确性非常重要时，驱动程序才应使用高分辨率计时器，并在所有其他情况下使用默认分辨率计时器。

若要创建高分辨率计时器，WDM 驱动程序将调用 [**ExAllocateTimer**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatetimer) 例程，并 \_ \_ \_ 在 *Attributes* 参数中设置 EX 计时器高分辨率标志。 当驱动程序调用 [**ExSetTimer**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exsettimer) 例程来设置高分辨率计时器时，操作系统会根据需要增加系统时钟的分辨率，使计时器的过期时间更精确地与 *DueTime* 和 *Period* 参数中指定的名义过期时间相对应。

Kernel-Mode Driver Framework (KMDF) 驱动程序可以调用 [**WdfTimerCreate**](/windows-hardware/drivers/ddi/wdftimer/nf-wdftimer-wdftimercreate) 方法来创建高分辨率计时器。 在此调用中，驱动程序将一个指针作为参数传递给 [**WDF \_ 计时器 \_ 配置**](/windows-hardware/drivers/ddi/wdftimer/ns-wdftimer-_wdf_timer_config) 结构。 若要创建高分辨率计时器，驱动程序将此结构的 **UseHighResolutionTimer** 成员设置为 **TRUE**。 此成员是从 Windows 8.1 和 KMDF 版本1.13 开始的结构的一部分。

## <a name="controlling-timer-accuracy"></a>控制计时器准确性


例如，对于 x86 处理器上运行的 Windows，系统时钟周期的默认时间间隔通常约为15毫秒，系统时钟计时周期之间的最小时间间隔约为1毫秒。 因此，默认解析计时器的过期时间 (如果 **ExAllocateTimer** \_ 未设置 EX 计时器 \_ 高分辨率标志，则会在 \_ 大约15毫秒内控制) ，但高分辨率计时器的过期时间可以在毫秒内进行控制。

如果驱动程序为默认解析计时器指定了相对过期时间，则计时器最多可以过期约15毫秒或更晚于指定的过期时间。 如果驱动程序为高分辨率计时器指定了相对过期时间，则计时器会在指定的过期时间之后的大约一毫秒后过期，但不会提前过期。 有关系统时钟解析与计时器准确性之间关系的详细信息，请参阅 [计时器准确性](timer-accuracy.md)。

如果未设置高分辨率计时器，操作系统通常会以默认速率运行系统时钟。 但是，如果设置了一个或多个高分辨率计时器，则操作系统可能需要在这些计时器过期之前至少以其最大速率运行系统时钟。

为了避免不必要地增加能耗，操作系统仅在需要满足高分辨率计时器的计时要求时才以其最大速率运行系统时钟。 例如，如果有一个高分辨率计时器定期运行，并且其期间跨越了几个默认的系统时钟周期，则操作系统可能只在计时器期间（即每个过期时间之前）的最大速率下运行系统时钟。 对于计时器时间的其余部分，系统时钟将按其默认速度运行。

为了避免消耗过多，驱动程序应避免将长时间运行的高分辨率计时器的持续时间设置为小于系统时钟计时周期的默认时间间隔的值。 否则，系统会强制以最大速率持续运行系统时钟。

从 Windows 8 开始，驱动程序可以调用 [**ExQueryTimerResolution**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exquerytimerresolution) 例程来获取系统时钟支持的计时器分辨率范围。

## <a name="comparison-to-exsettimerresolution"></a>与 ExSetTimerResolution 的比较


从 Windows 2000 开始，驱动程序可以调用 [**ExSetTimerResolution**](calling-exsettimerresolution-while-processing-a-power-irp.md) 例程来更改连续系统时钟中断之间的时间间隔。 例如，驱动程序可以调用此例程，将系统时钟从其默认速率更改为其最大速率以提高计时器准确性。 但是，与使用 **ExAllocateTimer** 创建的高分辨率计时器相比，使用 **ExSetTimerResolution** 有几个缺点。

首先，在调用 **ExSetTimerResolution** 以暂时增加系统时钟速率之后，驱动程序必须第二次调用 **ExSetTimerResolution** ，以将系统时钟还原为其默认速率。 否则，系统时钟计时器会持续以最大速率生成中断，这可能会导致过多的功率消耗。

其次，使用 **ExSetTimerResolution** 例程的驱动程序无法按照操作系统为高分辨率计时器有效地优化系统时钟速率的临时使用。 因此，系统时钟花费的时间超过了所需的最大速度。

第三，如果多个驱动程序同时使用 **ExSetTimerResolution** 来提高计时器准确性，则系统时钟可能会长时间运行一次。 与此相反，操作系统全局协调多个高分辨率计时器的操作，以便仅当需要满足这些计时器的计时要求时，系统时钟才以最大速率运行。

最后，使用 **ExSetTimerResolution** 在本质上不如使用高分辨率计时器。 驱动程序调用 **ExSetTimerResolution** 将系统时钟增加到其最大速率（通常约为每毫秒计时周期）时，驱动程序可能会调用例程（如 [**KeSetTimerEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesettimerex) ）来设置计时器。 如果在此调用中，驱动程序指定了相对过期时间，则计时器的过期时间大约为早于或晚于指定的过期时间。 但是，如果为高分辨率计时器指定了相对过期时间，则计时器会在超过指定的过期时间之后的大约一毫秒后过期，但永不会提前过期。

 


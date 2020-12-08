---
title: 使用计时器
description: 介绍如何使用框架的内置计时器支持。 适用于从版本2开始的 KMDF 驱动程序和 UMDF 驱动程序。
keywords:
- 计时器 WDK KMDF
- framework 对象 WDK KMDF，计时器对象
- timer 对象 WDK KMDF
- 定期计时器 KMDF
- 停止计时器 WDK KMDF
- 开始计时器 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8996222c36b1f41b6eaf7f2ed9fca9eb68a17c80
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785411"
---
# <a name="using-timers"></a>使用计时器


本主题介绍如何使用框架的内置计时器支持。 它适用于 Kernel-Mode Driver Framework (KMDF) 驱动程序以及从版本2开始的 User-Mode 驱动程序框架 (UMDF) 驱动程序。

该框架提供了一个 *计时器对象* ，使驱动程序可以创建计时器。 当驱动程序创建计时器对象并启动计时器时钟后，框架将在经过指定的时间后调用驱动程序提供的回调函数。 或者，您的驱动程序可以设置计时器，以便每当经过指定的一段时间，框架就会重复调用回调函数。

若要创建框架计时器对象，驱动程序必须调用 [**WdfTimerCreate**](/windows-hardware/drivers/ddi/wdftimer/nf-wdftimer-wdftimercreate) 方法。 此方法注册一个 [*EvtTimerFunc*](/windows-hardware/drivers/ddi/wdftimer/nc-wdftimer-evt_wdf_timer) 回调函数和一个周期性时间间隔。 如果希望框架只调用一次回调函数，则驱动程序将为周期性时间间隔指定零。

通常，您会知道您的驱动程序将需要每个设备的计时器数。 因此，驱动程序可以通过在其 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调函数中调用 [**WdfTimerCreate**](/windows-hardware/drivers/ddi/wdftimer/nf-wdftimer-wdftimercreate)来创建计时器对象，并且它可以在设备或队列对象的 [上下文空间](framework-object-context-space.md)中存储计时器对象句柄。

若要启动计时器，驱动程序将调用 [**WdfTimerStart**](/windows-hardware/drivers/ddi/wdftimer/nf-wdftimer-wdftimerstart)，同时传递 "截止时间"。 框架将启动计时器的时钟，并在指定的时间量已过后调用 [*EvtTimerFunc*](/windows-hardware/drivers/ddi/wdftimer/nc-wdftimer-evt_wdf_timer) 回调函数。

如果驱动程序在调用 [**WdfTimerCreate**](/windows-hardware/drivers/ddi/wdftimer/nf-wdftimer-wdftimercreate)时提供了一个周期性时间间隔，则该计时器称为 *定期计时器*。 在初始 "截止时间" 结束后，定期计时器的时钟将继续运行，并且每当周期性时间间隔结束后，框架将重复调用驱动程序的回调函数。 定期计时器不会自动启动。 与非定期计时器一样，驱动程序在创建计时器以首次启动时仍必须调用 [**WdfTimerStart**](/windows-hardware/drivers/ddi/wdftimer/nf-wdftimer-wdftimerstart) 。

驱动程序可以从其 [*EvtTimerFunc*](/windows-hardware/drivers/ddi/wdftimer/nc-wdftimer-evt_wdf_timer)回调函数调用 [**WdfTimerStart**](/windows-hardware/drivers/ddi/wdftimer/nf-wdftimer-wdftimerstart) ，以便在计时器过期后重新启动非定期计时器。

若要停止计时器，驱动程序可以调用 [**WdfTimerStop**](/windows-hardware/drivers/ddi/wdftimer/nf-wdftimer-wdftimerstop)。 驱动程序可以重复启动和停止计时器，从而重复使用计时器。

当驱动程序创建 timer 对象时，它必须指定一个父对象。 框架停止计时器，并在删除父项时删除计时器对象。 若要获取计时器对象的父对象，驱动程序可以调用 [**WdfTimerGetParentObject**](/windows-hardware/drivers/ddi/wdftimer/nf-wdftimer-wdftimergetparentobject)。

在版本1.9 之前的 KMDF 版本中，如果希望所有驱动程序的回调函数都以 IRQL = 被动级别运行，则无法轻松使用 timer 对象 \_ 。 该框架实现 timer 对象的 [*EvtTimerFunc*](/windows-hardware/drivers/ddi/wdftimer/nc-wdftimer-evt_wdf_timer) 回调函数作为延迟的过程调用 (DPC) ，该调用在 IRQL = 调度级别进行调用 \_ 。 因此，如果希望计时器过期代码在被动级别运行， \_ 则 *EvtTimerFunc* 回调函数必须将在被动级别运行的 [工作项](using-framework-work-items.md) 排队 \_ 。

在 KMDF 版本1.9 及更高版本中，可以创建 *被动级别计时器*，这是在被动级别运行的计时器 \_ 。 若要创建被动级别计时器，请在驱动程序调用 [**WdfTimerCreate**](/windows-hardware/drivers/ddi/wdftimer/nf-wdftimer-wdftimercreate)时指定 [**WdfExecutionLevelPassive**](/windows-hardware/drivers/ddi/wdfobject/ne-wdfobject-_wdf_execution_level)执行级别。 因此，框架将 [*EvtTimerFunc*](/windows-hardware/drivers/ddi/wdftimer/nc-wdftimer-evt_wdf_timer) 回调函数实现为在被动级别运行的工作项 \_ 。 请注意，被动级别的计时器不能是定期计时器。

从 UMDF 版本2.0 开始，框架将 timer 对象的 [*EvtTimerFunc*](/windows-hardware/drivers/ddi/wdftimer/nc-wdftimer-evt_wdf_timer) 回调函数实现为用户模式线程池中的工作线程。 因此，UMDF 驱动程序的计时器回调函数始终在被动 \_ 级别运行。

## <a name="no-wake-timers"></a>无唤醒计时器


系统能效降低了反复导致系统从低功耗状态恢复的计时器。 提高电池寿命的一种方法是延迟非关键定期操作，而不是唤醒系统。 从 Windows 8.1 开始，可以不使用 *唤醒计时器* 在 KMDF 或 UMDF 驱动程序中执行此类非关键操作。 如果系统处于低功耗状态，则不唤醒计时器不会唤醒系统。 相反，当系统下一次处于完全打开状态时，框架会调用驱动程序的 [*EvtTimerFunc*](/windows-hardware/drivers/ddi/wdftimer/nc-wdftimer-evt_wdf_timer) 回调函数。

从 KMDF 版本1.13 和 UMDF 版本2.0 开始，不提供任何唤醒计时器。

若要创建无唤醒计时器，请将 [**WDF \_ 计时器 \_ 配置**](/windows-hardware/drivers/ddi/wdftimer/ns-wdftimer-_wdf_timer_config)的 **TolerableDelay** 成员设置为 **TolerableDelayUnlimited**。

有关无唤醒计时器的详细信息，请参阅 [无唤醒计时器](../kernel/no-wake-timers.md)。

## <a name="high-resolution-timers"></a>高分辨率计时器


标准框架计时器具有与系统时钟滴答间隔（默认为15.6 毫秒）匹配的准确性。 从 Windows 8.1 开始，你可以创建 *高分辨率计时器*。 高分辨率计时器的精度为1毫秒。 对于需要精确、可预测过期时间的关键操作，可以使用高分辨率计时器。 由于它需要频繁处理，因此高分辨率计时器可能会导致电池电量下降。

高分辨率计时器仅适用于 KMDF 驱动程序，从 KMDF 版本1.13 开始。

若要创建高分辨率计时器，请将 [**WDF \_ 计时器 \_ 配置**](/windows-hardware/drivers/ddi/wdftimer/ns-wdftimer-_wdf_timer_config)的 **UseHighResolutionTimer** 成员设置为 **WdfTrue**，然后将 **Period** 值调整为所需的分辨率。

下表显示了基于驱动程序为 **句点** 提供的不同值的计时器行为的示例。 这些示例假定系统时钟滴答时间间隔为15毫秒。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">时间段（毫秒）</th>
<th align="left">标准计时器</th>
<th align="left">高分辨率计时器</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>10</p></td>
<td align="left"><p>计时器将在0毫秒到25毫秒之间过期。</p></td>
<td align="left"><p>计时器会在10毫秒后尽快过期。</p></td>
</tr>
<tr class="even">
<td align="left"><p>16</p></td>
<td align="left"><p>计时器在15毫秒到30毫秒之间到期。</p></td>
<td align="left"><p>计时器将在16毫秒后过期。</p></td>
</tr>
</tbody>
</table>

 

有关高分辨率计时器的详细信息，请参阅 [高分辨率计时器](../kernel/high-resolution-timers.md)。

有关计时器准确性与系统时钟粒度的关系的详细信息，请参阅 [计时器准确性](../kernel/timer-accuracy.md)。

 


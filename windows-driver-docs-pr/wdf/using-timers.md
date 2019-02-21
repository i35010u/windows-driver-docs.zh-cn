---
title: 使用计时器
description: 介绍如何使用框架的内置的计时器支持。 适用于 KMDF 驱动程序和 UMDF 驱动程序从版本 2。
ms.assetid: f3bca5bf-fa5f-4b8f-ad28-26d29fc33963
keywords:
- 计时器 WDK KMDF
- framework 对象 WDK KMDF，计时器对象
- 计时器对象 WDK KMDF
- 定期计时器 WDK KMDF
- 停止计时器 WDK KMDF
- 开始计时器 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 91a7fbdd2b40fadbc73594010311be790a2368fc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545504"
---
# <a name="using-timers"></a>使用计时器


本主题介绍如何使用框架的内置的计时器支持。 它适用于内核模式驱动程序框架 (KMDF) 驱动程序以及从版本 2 的用户模式驱动程序框架 (UMDF) 驱动程序。

该框架提供了*计时器对象*，使驱动程序，以创建计时器。 驱动程序创建计时器对象，并启动计时器的时钟后，框架将经过指定的时间段后调用的驱动程序提供的回调函数。 （可选） 您的驱动程序可以设置计时器，以便框架调用的回调函数重复，只要指定的时间内已过。

若要创建 framework 计时器对象，您的驱动程序必须调用[ **WdfTimerCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff550050)方法。 此方法注册[ *EvtTimerFunc* ](https://msdn.microsoft.com/library/windows/hardware/ff541823)回调函数和定期时间间隔。 如果你想要一次调用的回调函数的框架，您的驱动程序指定的定期时间间隔为零。

通常情况下，您将知道您的驱动程序将需要为每个设备的计时器的数目。 因此，该驱动程序可以通过调用创建计时器对象[ **WdfTimerCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff550050)中其[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)回调函数它可以在设备或队列对象的存储计时器对象句柄[上下文空间](framework-object-context-space.md)。

若要启动计时器，驱动程序调用[ **WdfTimerStart**](https://msdn.microsoft.com/library/windows/hardware/ff550054)，传递"截止时间"。 在框架开始计时器的时钟和调用[ *EvtTimerFunc* ](https://msdn.microsoft.com/library/windows/hardware/ff541823)回调函数时指定的时间量已过。

如果该驱动程序提供周期性的时间间隔时调用它[ **WdfTimerCreate**](https://msdn.microsoft.com/library/windows/hardware/ff550050)，计时器称为*定期计时器*。 定期计时器时钟将继续运行后初始过后"截止时间"，和框架调用驱动程序的回调函数重复，只要周期性的时间间隔已过。 不自动启动定期计时器。 非定期计时器，如驱动程序仍需调用[ **WdfTimerStart** ](https://msdn.microsoft.com/library/windows/hardware/ff550054)后创建要启动它第一次的计时器。

驱动程序可能会调用[ **WdfTimerStart** ](https://msdn.microsoft.com/library/windows/hardware/ff550054)从其[ *EvtTimerFunc* ](https://msdn.microsoft.com/library/windows/hardware/ff541823)以便重新启动后的非定期计时器回调函数过期。

若要停止计时器，该驱动程序可以调用[ **WdfTimerStop**](https://msdn.microsoft.com/library/windows/hardware/ff550056)。 您的驱动程序可以通过启动和停止它们反复重新使用计时器。

当您的驱动程序创建计时器对象时，它必须指定父对象。 框架停止计时器并删除的父级时删除该计时器对象。 若要获取计时器对象的父对象，您的驱动程序可以调用[ **WdfTimerGetParentObject**](https://msdn.microsoft.com/library/windows/hardware/ff550052)。

在之前的版本 1.9 KMDF 版本中，您不能方便地使用计时器对象如果所需的所有驱动程序的回调函数在 IRQL 运行 = 被动\_级别。 该框架实现计时器对象的[ *EvtTimerFunc* ](https://msdn.microsoft.com/library/windows/hardware/ff541823)回调函数作为延迟的过程调用 (DPC) 的调用在 IRQL = 调度\_级别。 因此，如果您希望计时器过期代码运行在被动\_级别*EvtTimerFunc*回调函数必须排队[工作项](using-framework-work-items.md)运行在被动\_级别。

在 KMDF 版本 1.9 及更高版本中，可以创建*被动级别计时器*，这是在被动运行的计时器\_级别。 若要创建被动级别计时器，请指定[ **WdfExecutionLevelPassive** ](https://msdn.microsoft.com/library/windows/hardware/ff551310)时驱动程序所调用的执行级别[ **WdfTimerCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff550050). 因此，该框架实现[ *EvtTimerFunc* ](https://msdn.microsoft.com/library/windows/hardware/ff541823)回调函数，如工作项运行的被动\_级别。 请注意，被动级别计时器不能为定期计时器。

从 UMDF 2.0 版开始，该框架实现计时器对象[ *EvtTimerFunc* ](https://msdn.microsoft.com/library/windows/hardware/ff541823)回调函数，从用户模式的工作线程为线程池。 因此，UMDF 驱动程序的计时器回调函数始终运行在被动\_级别。

## <a name="no-wake-timers"></a>没有唤醒计时器


系统电源效率降低重复导致系统从低功耗状态恢复的计时器。 提高电池使用寿命的一种方法是延迟非关键的定期操作，而不是唤醒系统。 从 Windows 8.1，您可以使用*没有唤醒计时器*KMDF 或 UMDF 驱动程序中执行此类非关键操作。 没有唤醒计时器不会唤醒系统，如果系统处于低功耗状态时过期。 相反，框架将调用的驱动程序[ *EvtTimerFunc* ](https://msdn.microsoft.com/library/windows/hardware/ff541823)系统处于其完全处于 S0 状态下一次的回调函数。

没有唤醒计时器是从版本 1.13 KMDF 和 UMDF 2.0 版开始提供。

若要创建一个没有唤醒计时器，设置**TolerableDelay**的成员[ **WDF\_计时器\_配置**](https://msdn.microsoft.com/library/windows/hardware/ff552519)到**TolerableDelayUnlimited**。

没有唤醒计时器的详细信息，请参阅[否唤醒计时器](https://msdn.microsoft.com/library/windows/hardware/dn265414)。

## <a name="high-resolution-timers"></a>高分辨率计时器


标准框架在计时器有精确匹配系统时钟计时周期时间间隔，这是默认 15.6 毫秒。 从 Windows 8.1，您可以创建*高分辨率计时器*。 高分辨率计时器的精度为一毫秒。 所需的精确、 可预测的过期时间的关键操作，可以使用高分辨率计时器。 由于频繁地提供服务，它要求，而高分辨率计时器可能会导致降低的电池寿命。

高分辨率计时器可仅供 KMDF 驱动程序 KMDF 版本 1.13 从开始。

若要创建高分辨率计时器，设置**UseHighResolutionTimer**的成员[ **WDF\_计时器\_配置**](https://msdn.microsoft.com/library/windows/hardware/ff552519)到**WdfTrue**，然后调整**期**到所需的分辨率的值。

下表显示了基于的驱动程序提供了不同值的计时器行为的示例**期**。 这些示例假定系统时钟计时周期时间间隔为 15 毫秒。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">段，以毫秒为单位</th>
<th align="left">标准计时器</th>
<th align="left">高分辨率计时器</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>10</p></td>
<td align="left"><p>在计时器过期 0 毫秒和 25 毫秒之间。</p></td>
<td align="left"><p>尽可能情况下，在计时器过期后，立即后 10 毫秒。</p></td>
</tr>
<tr class="even">
<td align="left"><p>16</p></td>
<td align="left"><p>在计时器过期 15 毫秒到 30 毫秒。</p></td>
<td align="left"><p>尽可能情况下，在计时器过期后，立即在 16 毫秒后。</p></td>
</tr>
</tbody>
</table>

 

关于高分辨率计时器的详细信息，请参阅[高分辨率计时器](https://msdn.microsoft.com/library/windows/hardware/dn265247)。

有关如何与系统时钟的粒度关联计时器准确性的详细信息，请参阅[计时器准确性](https://msdn.microsoft.com/library/windows/hardware/jj602805)。

 

 






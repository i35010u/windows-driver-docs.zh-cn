---
title: KeXxxTimer 例程、KTIMER 对象和 DPC
description: 从 Windows 2000 开始，可以使用一组 KeXxxTimer 例程来管理计时器。
keywords:
- 计时器的 WDK 内核
- 计时器对象 WDK 内核
- 计时器对象 WDK 内核，关于计时器对象
- 延迟的过程调用 WDK 内核
- Dpc WDK 内核
- 内核调度程序对象 WDK，计时器对象
- 调度程序对象 WDK 内核，计时器对象
- 通知计时器 WDK 内核
- 同步计时器，WDK 内核
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
ms.openlocfilehash: 15f1b8cfd3e490145008d3afd0766e3104f77909
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814271"
---
# <a name="kexxxtimer-routines-ktimer-objects-and-dpcs"></a>KeXxxTimer 例程、KTIMER 对象和 DPC


从 Windows 2000 开始，可以使用一组 **Ke *Xxx* 计时器** 例程来管理计时器。 这些例程使用基于 [**KTIMER**](./eprocess.md) 结构的计时器对象。 若要创建 timer 对象，驱动程序首先为 **KTIMER** 结构分配存储。 然后，该驱动程序将调用一个例程，如 [**KeInitializeTimer**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializetimer) 或 [**KeInitializeTimerEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializetimerex) 来初始化此结构。




计时器可以设置为仅在一次后过期，或在给定的时间间隔后重复过期。 [**KeSetTimer**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesettimer) 始终设置将只在一次后过期的计时器。 [**KeSetTimerEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesettimerex) 接受一个可选的 *Period* 参数，该参数指定一个周期性计时器时间间隔。

可选的 [*CustomTimerDpc*](https://msdn.microsoft.com/library/windows/hardware/ff542983) 例程 (一种延迟的过程调用) 可以与通知计时器或同步计时器相关联。 此例程在指定的时间间隔到期时执行。 有关详细信息，请参阅 [使用计时器对象](using-timer-objects.md)。

计时器可以是 *通知计时器* 或 *同步计时器*。

-   通知计时器收到信号时，所有正在等待的线程均已满足等待。 计时器的状态将保持为已终止状态，直到它被显式重置。

-   同步计时器过期时，会将其状态设置为 "已终止"，直到释放单个等待线程。 然后，计时器将重置为 Not-Signaled 状态。

**KeInitializeTimer** 始终创建通知计时器。 **KeInitializeTimerEx** 接受类型参数，该 *类型* 参数可以是 **NotificationTimer** 或 **SynchronizationTimer**。

以下主题提供了有关计时器对象和 Dpc 的详细信息：

[使用计时器对象](using-timer-objects.md) 
[计时器准确性](timer-accuracy.md) 
[注册和排队 CustomTimerDpc 例程](registering-and-queuing-a-customtimerdpc-routine.md) 
[提供 CustomTimerDpc 上下文信息](providing-customtimerdpc-context-information.md) 
[使用 CustomTimerDpc 例程](using-a-customtimerdpc-routine.md)
 


---
title: 使用计时器对象
description: 使用计时器对象
ms.assetid: b3ee9d92-87b9-47b7-ab13-11e42bec7997
keywords:
- 计时器对象 WDK 内核，等待
- 等待计时器对象
- 通知计时器 WDK 内核
- KeDelayExecutionThread
- KeWaitForSingleObject
- KeInitializeTimer
- KeSetTimer
- DueTime 值
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5297b5703b0424d3b7f348313f0fb57151ee9eeb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835844"
---
# <a name="using-timer-objects"></a>使用计时器对象





下图说明了如何使用通知计时器设置操作的超时时间间隔，并等待其他驱动程序例程处理 i/o 请求。

![说明如何等待计时器对象的关系图](images/3ketimer.png)

如上图所示，驱动程序必须为 timer 对象提供存储，该对象必须通过调用[**KeInitializeTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializetimer)并使用指向此存储的指针进行初始化。 驱动程序通常从其[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)例程进行此调用。

在特定线程的上下文中（如驱动程序创建的线程或请求同步 i/o 操作的线程），驱动程序可以等待其 timer 对象，如下图所示：

1.  该线程使用指向 timer 对象的指针和给定的*DueTime*值（以100毫微秒为单位表示）调用[**KeSetTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesettimer) 。 *DueTime*的正值指定应从内核的计时器队列中删除计时器对象并将其设置为终止状态的绝对时间。 *DueTime*的负值指定了相对于当前系统时间的间隔。

    请注意，在系统线程中运行的线程（或在系统线程中运行的驱动程序例程）为 DPC 对象传递**NULL**指针（如图中所示，演示如何在[CustomTimerDpc 例程中使用 timer 和 DPC 对象](registering-and-queuing-a-customtimerdpc-routine.md)）调用**KeSetTimer**如果它等待计时器对象，而不是对[*CustomTimerDpc*](https://msdn.microsoft.com/library/windows/hardware/ff542983)例程进行排队。

2.  该线程使用指向 timer 对象的指针调用[**KeWaitForSingleObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject) ，这会将线程置于等待状态，而计时器对象位于内核的计时器队列中。

3.  给定的*DueTime*过期。

4.  内核取消排队 timer 对象，将其设置为 "已终止" 状态，并将线程的状态从 "正在等待" 更改为 "就绪"。

5.  处理器可用时，内核会立即调度线程以执行：也就是说，具有较高优先级的其他线程目前处于 "就绪" 状态，并且没有要在更高的 IRQL 上运行的内核模式例程。

以 IRQL &gt;= 调度\_级别运行的驱动程序例程可以通过将 timer 对象与关联的 DPC 对象结合使用来排队驱动程序提供的[*CustomTimerDpc*](https://msdn.microsoft.com/library/windows/hardware/ff542983)例程，从而超时请求。 只有在 nonarbitrary 线程上下文中运行的驱动程序例程才能在 timer 对象上等待非零间隔，如上图所示。

与其他每个线程一样，驱动程序创建的线程由内核线程对象表示，这也是一个调度程序对象。 因此，驱动程序不需要其驱动程序创建的线程使用 timer 对象，以便在给定的时间间隔内自行进入等待状态。 相反，线程可以使用调用方提供的时间间隔来调用[**KeDelayExecutionThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kedelayexecutionthread) 。 有关此技术的详细信息，请参阅对[设备进行轮询](avoid-polling-devices.md)。

[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)、重新[*初始化*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nc-ntddk-driver_reinitialize)和[*卸载*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)例程也在系统线程上下文中运行，因此，驱动程序可以使用驱动程序初始化的 timer 对象或**KeDelayExecutionThread**调用**KeWaitForSingleObject** ，正在初始化或卸载。 如果设备驱动程序在其初始化过程中必须等待设备更新状态，则设备驱动程序可以调用[**KeStallExecutionProcessor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-kestallexecutionprocessor)一段很短的时间（最好是小于50微秒的时间）。

但是，更高级别的驱动程序通常会在其[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)中使用其他同步机制，并重新[*初始化*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nc-ntddk-driver_reinitialize)例程，而不是使用 timer 对象。 应始终将较高级别的驱动程序设计为在特定类型或设备类型的任何较低级别的驱动程序上进行分层。 因此，更高级别的驱动程序在等待 timer 对象或调用**KeDelayExecutionThread**时，加载速度会变慢，因为这样的驱动程序必须等待足够长的时间间隔来容纳支持它的可能的最慢设备。 另请注意，这种等待的最小时间间隔很难确定。

同样，PnP 驱动程序不应等待其他操作发生，而应使用 PnP 管理器的[通知](using-pnp-notification.md)机制。

 

 





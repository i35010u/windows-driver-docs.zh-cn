---
title: 访问共享状态信息
description: 访问共享状态信息
ms.assetid: f3e5ac07-cab1-4f66-90e4-88b2e28079a5
keywords:
- 关键节例程 WDK 内核
- 计时器计数器 WDK 内核
- 共享的状态信息 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8a3a21892aaba925d4987de51317c6d800cbe77
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363447"
---
# <a name="accessing-shared-state-information"></a>访问共享状态信息





遵循以下通用原则用于设计和编写[ *SynchCritSection* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-ksynchronize_routine)维护状态的例程：

-   若要访问 ISR 还可访问的数据，驱动程序例程必须调用*SynchCritSection*例程。 非关键部分代码可能会中断。 请记住，是不足够，只需获取数值调节钮锁来保护 Isr 还访问，数据，因为 Isr 执行 DIRQL 和获取数值调节钮锁 ([**KeAcquireSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keacquirespinlock)) 只会提升到 IRQL调度\_级别，允许中断调用 ISR 当前处理器上的。

-   为每个*SynchCritSection*例程维护一组离散的状态变量的状态信息负责。 也就是说，避免编写*SynchCritSection*维护重叠的例程的状态信息。

    这可以防止争用情况，并可能争用条件之间*SynchCritSection*例程 （和 ISR） 尝试访问相同的并发状态。

    这还可以确保每个*SynchCritSection*例程返回控件尽可能快地因为一个*SynchCritSection*例程绝不会等待另一个更新的某些相同的状态若要将控制返回的信息。

-   避免编写单一的大型、 常规用途*SynchCritSection*的例程，多个测试条件来确定要执行的操作比实际执行有用的工作。 另一方面，避免许多*SynchCritSection*永远不会执行的条件语句，因为每个更新仅单字节的状态信息的例程。

-   每个*SynchCritSection*例程必须尽可能快速地返回控制，因为运行任何*SynchCritSection*例程阻止驱动程序的 ISR 执行。

下面是用于维护设备扩展中的计时器计数器的技术。 假定该驱动程序使用计数器来确定某个 I/O 操作已超时。另外，假设驱动程序不重叠的 I/O 操作。

-   在驱动程序[ *StartIo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)例程初始化每个 I/O 请求的计时器计数器为一些初始的值。 该驱动程序然后将第二个添加到其设备超时值，以防其[ *IoTimer* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_timer_routine)例程刚返回控制。

-   驱动程序的 ISR 必须设置此计时器计数器减一。

-   在驱动程序[ *IoTimer* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_timer_routine)例程调用一次每秒读取的 time 计数器，并确定是否 ISR 具有已将其设置到减一。 如果没有，则*IoTimer*例程递减使用计数器[ **KeSynchronizeExecution** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesynchronizeexecution)调用 SynchCritSection\_1 例程。

    如果计数器回到零，表示请求已超时，SynchCritSection\_1 例程调用 SynchCritSection\_2 例程进行编程设备重置操作。 如果计数器值减 1， [ *IoTimer* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_timer_routine)例程仅返回。

-   如果驱动程序的[ *DpcForIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_dpc_routine)例程必须对设备开始部分传输操作中，它必须重新初始化为计时器计数器[ *StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)未例程。

    [ *DpcForIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_dpc_routine)例程也必须使用[ **KeSynchronizeExecution** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesynchronizeexecution)调用 SynchCritSection\_2 例程或可能是 SynchCritSection\_3 例程进行编程的另一个传输操作设备。

在此方案中，该驱动程序有多个*SynchCritSection*例程中，每个与离散的特定职责; 来维护其计时器的计数器，和一个或多个其他人进行编程的设备。 每个*SynchCritSection*例程可以快速地返回控制，因为它将执行单一的离散任务。

请注意，该驱动程序包含单个 SynchCritSection\_1 例程的驱动程序的 ISR 以及维护到计时器计数器的状态。 因此，不存在争用访问其中的几计时器计数器*SynchCritSection*例程和 ISR

 

 





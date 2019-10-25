---
title: 访问共享状态信息
description: 访问共享状态信息
ms.assetid: f3e5ac07-cab1-4f66-90e4-88b2e28079a5
keywords:
- 关键部分例程 WDK 内核
- 计时器计数器 WDK 内核
- 共享状态信息 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 04a7b9ba98ae50837e0cb5a98a0b7887737c49a1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828681"
---
# <a name="accessing-shared-state-information"></a>访问共享状态信息





使用以下一般准则来设计和编写维护状态的[*SynchCritSection*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-ksynchronize_routine)例程：

-   若要访问 ISR 还访问的数据，驱动程序例程必须调用*SynchCritSection*例程。 非关键部分代码可能会中断。 请记住，只需获取旋转锁来保护 Isr 也访问的数据，因为 Isr 在 DIRQL 执行，而获取旋转锁（[**KeAcquireSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock)）只会引发 IRQL 来调度\_级别，这允许中断在当前处理器上调用 ISR。

-   为每个*SynchCritSection*例程提供维护一组离散状态变量的状态信息的责任。 也就是说，应避免编写维护重叠状态信息的*SynchCritSection*例程。

    这可以防止在*SynchCritSection*例程（和 ISR）之间尝试同时访问同一状态的争用和可能出现争用情况。

    这还可以确保每个*SynchCritSection*例程尽快返回 control，因为一个*SynchCritSection*例程永远都不需要等待更新某些相同状态信息的另一个状态信息来返回控制。

-   避免编写单一、大型、通用的*SynchCritSection*例程，该例程可以更好地测试条件，以确定要执行的操作。 另一方面，请避免使用许多*SynchCritSection*例程，这些例程永远不会执行条件语句，因为每个例程只更新一字节的状态信息。

-   每个*SynchCritSection*例程必须尽快返回控制权，因为运行任何*SynchCritSection*例程会阻止驱动程序的 ISR 执行。

下面是在设备扩展中维护计时器计数器的一项技术。 假定驱动程序使用计数器来确定 i/o 操作是否已超时。还假定驱动程序未与 i/o 操作重叠。

-   驱动程序的[*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)例程将计时器计数器初始化为每个 i/o 请求的某个初始值。 然后，该驱动程序将第二个添加到其设备的超时值，以防其[*IoTimer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_timer_routine)例程刚刚返回控件。

-   驱动程序的 ISR 必须将此计时器计数器设置为减1。

-   每秒调用一次驱动程序的[*IoTimer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_timer_routine)例程来读取时间计数器，并确定 ISR 是否已将其设置为减1。 否则， *IoTimer*例程会通过使用[**KeSynchronizeExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution)调用 SynchCritSection\_1 例程来递减计数器。

    如果计数器的值为零，表示请求超时，则 SynchCritSection\_1 例程将调用 SynchCritSection\_2 例程来对设备重置操作进行编程。 如果计数器为减1，则[*IoTimer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_timer_routine)例程只返回。

-   如果驱动程序的[*DpcForIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)例程必须重新编程设备才能开始部分传输操作，则它必须重新初始化计时器计数器，因为[*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)例程已执行。

    [*DpcForIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)例程还必须使用[**KeSynchronizeExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution)调用 SynchCritSection\_2 例程，或使用 SynchCritSection\_3 例程来对设备进行其他传输操作。

在此方案中，驱动程序具有多个*SynchCritSection*例程，其中每个例程都具有离散的特定职责;一个用于维护其计时器计数器，另一个或多个用于对设备进行编程。 每个*SynchCritSection*例程会快速返回控制权，因为它执行单个离散任务。

请注意，驱动程序具有单个 SynchCritSection\_1 例程，该例程与驱动程序的 ISR 一起维护计时器计数器的状态。 因此，在多个*SynchCritSection*例程和 ISR 之间，无争用访问计时器计数器。

 

 





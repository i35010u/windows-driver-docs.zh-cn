---
title: 访问共享状态信息
description: 访问共享状态信息
keywords:
- 关键部分例程 WDK 内核
- 计时器计数器 WDK 内核
- 共享状态信息 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a4112bcee8c821a012fdd2c954babe887839bde
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790549"
---
# <a name="accessing-shared-state-information"></a>访问共享状态信息





使用以下一般准则来设计和编写维护状态的 [*SynchCritSection*](/windows-hardware/drivers/ddi/wdm/nc-wdm-ksynchronize_routine) 例程：

-   若要访问 ISR 还访问的数据，驱动程序例程必须调用 *SynchCritSection* 例程。 非关键部分代码可能会中断。 请记住，只需获取旋转锁来保护 Isr 也访问的数据，因为 Isr 在 DIRQL 上执行并获取旋转锁 ([**KeAcquireSpinLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock)) 只会将 IRQL 提升为调度 \_ 级别，这允许中断调用当前处理器上的 ISR。

-   为每个 *SynchCritSection* 例程提供维护一组离散状态变量的状态信息的责任。 也就是说，应避免编写维护重叠状态信息的 *SynchCritSection* 例程。

    这可以防止在 *SynchCritSection* 例程之间发生争用和可能出现争用情况， (和 ISR) 尝试同时访问同一状态。

    这还可以确保每个 *SynchCritSection* 例程尽快返回 control，因为一个 *SynchCritSection* 例程永远都不需要等待更新某些相同状态信息的另一个状态信息来返回控制。

-   避免编写单一、大型、通用的 *SynchCritSection* 例程，该例程可以更好地测试条件，以确定要执行的操作。 另一方面，请避免使用许多 *SynchCritSection* 例程，这些例程永远不会执行条件语句，因为每个例程只更新一字节的状态信息。

-   每个 *SynchCritSection* 例程必须尽快返回控制权，因为运行任何 *SynchCritSection* 例程会阻止驱动程序的 ISR 执行。

下面是在设备扩展中维护计时器计数器的一项技术。 假定驱动程序使用计数器来确定 i/o 操作是否已超时。还假定驱动程序未与 i/o 操作重叠。

-   驱动程序的 [*StartIo*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio) 例程将计时器计数器初始化为每个 i/o 请求的某个初始值。 然后，该驱动程序将第二个添加到其设备的超时值，以防其 [*IoTimer*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_timer_routine) 例程刚刚返回控件。

-   驱动程序的 ISR 必须将此计时器计数器设置为减1。

-   每秒调用一次驱动程序的 [*IoTimer*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_timer_routine) 例程来读取时间计数器，并确定 ISR 是否已将其设置为减1。 否则， *IoTimer* 例程会通过使用 [**KeSynchronizeExecution**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution) 调用 SynchCritSection 1 例程来减小计数器的值 \_ 。

    如果该计数器的值为零，表示请求超时，则 SynchCritSection \_ 1 例程将调用 SynchCritSection \_ 2 例程来对设备重置操作进行编程。 如果计数器为减1，则 [*IoTimer*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_timer_routine) 例程只返回。

-   如果驱动程序的 [*DpcForIsr*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine) 例程必须重新编程设备才能开始部分传输操作，则它必须重新初始化计时器计数器，因为 [*StartIo*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio) 例程已执行。

    [*DpcForIsr*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)例程还必须使用 [**KeSynchronizeExecution**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution)调用 SynchCritSection \_ 2 例程，或使用 SynchCritSection \_ 3 例程来对设备进行其他传输操作。

在此方案中，驱动程序具有多个 *SynchCritSection* 例程，其中每个例程都具有离散的特定职责;一个用于维护其计时器计数器，另一个或多个用于对设备进行编程。 每个 *SynchCritSection* 例程会快速返回控制权，因为它执行单个离散任务。

请注意，驱动程序具有单个 SynchCritSection \_ 1 例程，该例程与驱动程序的 ISR 一起维护计时器计数器的状态。 因此，在多个 *SynchCritSection* 例程和 ISR 之间，无争用访问计时器计数器。

 


---
title: 同步对设备数据的访问
description: 同步对设备数据的访问
ms.assetid: aaed8006-6773-4d20-b3a0-b48131f728c6
keywords:
- 中断服务例程 WDK 内核，同步
- Isr WDK 内核，同步
- 中断对象 WDK 内核，同步
- 同步 WDK 内核，中断
- 单个中断向量 WDK 内核
- 关键部分例程 WDK 内核
- 中断自旋锁定 WDK 内核
- 旋转锁定 WDK 内核
- 同步 WDK 内核，设备数据访问
- SynchCritSection
- SynchronizeIrql
- 旋转锁参数
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 297095bf2b105529c607e4a7c184accbc862dc7e
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185947"
---
# <a name="synchronizing-access-to-device-data"></a>同步对设备数据的访问





通常，驱动程序的 [*InterruptService*](/windows-hardware/drivers/ddi/wdm/nc-wdm-kservice_routine) 或 [*InterruptMessageService*](/windows-hardware/drivers/ddi/wdm/nc-wdm-kmessage_service_routine) 例程 (isr) 必须与其他驱动程序例程共享对驱动程序数据和硬件资源的访问权限。 由于 Isr 在中断上下文中以提升的 IRQL 执行，并且系统可能具有多个处理器，因此必须同步对共享数据和资源的访问，以便可以保证每个日常都可以在不中断的情况下临时获得对此共享信息的独占访问权限。

系统通过在 *中断关键部分*中执行 ISR 来支持此同步。 中断具有分配的自旋锁、 *中断自旋锁*和 irql （ *中断同步的 irql*）。 系统保证在关键部分中执行此代码，以独占方式访问共享信息，方法是：将处理器的 IRQL 提升为中断同步 IRQL，并在执行代码前获取中断自旋锁。 在执行其 ISR 之前，系统始终会输入中断的关键部分。 不同的中断可通过共享其中断自旋锁和同步 IRQL 来共享同一关键部分。

驱动程序可以通过提供 [*SynchCritSection*](/windows-hardware/drivers/ddi/wdm/nc-wdm-ksynchronize_routine) 例程来实现在中断的关键部分中运行的代码。 当驱动程序使用 [**KeSynchronizeExecution**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution) 调用 *SynchCritSection* 例程时，系统将自动为 *中断* 参数指定的中断输入临界区。

将处理器的 IRQL 提高到中断的同步 IRQL 会阻止当前处理器被中断，但具有更高同步 IRQL 的中断除外。 获取旋转锁可防止其他处理器执行与该旋转锁关联的任何关键部分代码。

当驱动程序调用 [**IoConnectInterruptEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterruptex)时，系统会为中断分配中断自旋锁和同步 IRQL。 在大多数情况下，驱动程序可以允许系统确定这两个值：

-   如果驱动程序使用基于连接 \_ 线路 \_ 的 **IoConnectInterruptEx**版本，并指定 **NULL** 旋转锁定，系统将为中断行分配一个自旋锁。 系统还会确定同步 IRQL 的值 (驱动程序可以选择指定较高的值) 。

-   如果驱动程序使用基于 CONNECT \_ MESSAGE \_ 的 **IoConnectInterruptEx**版本，并指定 **NULL** 自旋锁，系统将为每个中断消息分配一个自旋锁。 系统还会确定每个消息的同步 IRQL 值 (驱动程序可以选择指定较高的值（) 的所有消息都是相同的）。


仅当使用 IoConnectInterruptEx 的 CONNECT \_ 完全 \_ 指定版本时，以及具有必须共享同一关键**IoConnectInterruptEx**部分的多个中断向量时，驱动程序才必须分配其自己的自旋锁。 驱动程序可以通过使用**IO \_ CONNECT \_ 中断 \_ 参数**的**旋转锁**和**SynchronizeIrql**成员指定其自己的旋转锁定和同步 IRQL。 有关详细信息，请参阅 [**IO \_ CONNECT \_ 中断 \_ 参数**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_connect_interrupt_parameters)。

有关编写和输入关键部分的信息，请参阅 [使用关键部分](using-critical-sections.md)。

 


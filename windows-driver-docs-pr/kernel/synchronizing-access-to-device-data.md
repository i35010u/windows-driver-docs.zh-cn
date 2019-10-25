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
ms.openlocfilehash: af3c18a11220e7ad9fa47aec312c83e6232d7929
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838393"
---
# <a name="synchronizing-access-to-device-data"></a>同步对设备数据的访问





通常，驱动程序的[*InterruptService*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kservice_routine)或[*InterruptMessageService*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kmessage_service_routine)例程（isr）必须与其他驱动程序例程共享对驱动程序数据和硬件资源的访问权限。 由于 Isr 在中断上下文中以提升的 IRQL 执行，并且系统可能具有多个处理器，因此必须同步对共享数据和资源的访问，以便可以保证每个例程暂时具有对此的独占访问权限共享信息，无需中断。

系统通过在*中断关键部分*中执行 ISR 来支持此同步。 中断具有分配的自旋锁、*中断自旋锁*和 irql （*中断同步的 irql*）。 系统保证在关键部分中执行此代码，以独占方式访问共享信息，方法是：将处理器的 IRQL 提升为中断同步 IRQL，并在执行代码前获取中断自旋锁。 在执行其 ISR 之前，系统始终会输入中断的关键部分。 不同的中断可通过共享其中断自旋锁和同步 IRQL 来共享同一关键部分。

驱动程序可以通过提供[*SynchCritSection*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-ksynchronize_routine)例程来实现在中断的关键部分中运行的代码。 当驱动程序使用[**KeSynchronizeExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution)调用*SynchCritSection*例程时，系统将自动为*中断*参数指定的中断输入临界区。

将处理器的 IRQL 提高到中断的同步 IRQL 会阻止当前处理器被中断，但具有更高同步 IRQL 的中断除外。 获取旋转锁可防止其他处理器执行与该旋转锁关联的任何关键部分代码。

当驱动程序调用[**IoConnectInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterruptex)时，系统会为中断分配中断自旋锁和同步 IRQL。 在大多数情况下，驱动程序可以允许系统确定这两个值：

-   如果驱动程序使用 CONNECT\_LINE\_**IoConnectInterruptEx**版本，并指定**NULL**旋转锁定，系统将为中断行分配一个自旋锁。 系统还会确定同步 IRQL 的值（驱动程序可以选择指定较大的值）。

-   如果驱动程序使用连接\_基于**IoConnectInterruptEx**的消息\_版本，并指定**NULL**自旋锁，系统将为每个中断消息分配一个自旋锁。 系统还会确定每个消息的同步 IRQL 值（驱动程序可以选择指定较高的值，这对于所有消息都是通用的）。


仅当使用连接\_完全\_指定的**IoConnectInterruptEx**版本，并且具有必须共享同一关键部分的多个中断向量时，驱动程序才能分配其自己的自旋锁。 驱动程序可以通过使用**IO\_连接\_中断\_参数**的**旋转锁**和**SynchronizeIrql**成员指定自身的旋转锁定和同步 IRQL。 有关详细信息，请参阅[**IO\_连接\_中断\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_connect_interrupt_parameters)。

有关编写和输入关键部分的信息，请参阅[使用关键部分](using-critical-sections.md)。

 

 





---
title: 同步对设备数据的访问
description: 同步对设备数据的访问
ms.assetid: aaed8006-6773-4d20-b3a0-b48131f728c6
keywords:
- 中断服务例程 WDK 内核同步
- Isr WDK 内核同步
- 中断对象 WDK 内核同步
- 同步 WDK 内核中断
- 单个中断向量 WDK 内核
- 关键节例程 WDK 内核
- 中断自旋锁 WDK 内核
- 数值调节钮锁 WDK 内核
- 同步 WDK 内核设备数据访问
- SynchCritSection
- SynchronizeIrql
- 旋转锁参数
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac4f704b4295982d69aaff4aae7ef08879864615
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377904"
---
# <a name="synchronizing-access-to-device-data"></a>同步对设备数据的访问





通常情况下，驱动程序的[ *InterruptService* ](https://msdn.microsoft.com/library/windows/hardware/ff547958)或[ *InterruptMessageService* ](https://msdn.microsoft.com/library/windows/hardware/ff547940)例程 (Isr) 必须共享到驱动程序数据的访问权限和与其他驱动程序例程的硬件资源。 因为 Isr 在提升的 IRQL，中断上下文中执行，因为系统可能有多个处理器，很重要，以便可以保证每个例程来暂时具有独占访问此同步对共享的数据和资源的访问共享的信息，而不发生中断。

系统支持此同步通过执行在 ISR*中断关键节*。 中断已分配数值调节钮锁定*中断自旋锁*，和 irql，因此*中断同步 IRQL*。 系统可以保证此中的代码执行的关键部分独占访问权共享信息，通过引发处理器的 IRQL 与中断同步 IRQL 并执行代码之前获取中断自旋锁。 系统始终执行其 ISR.之前进入中断的关键部分 不同的中断可以通过共享其中断自旋锁和同步 IRQL 共享相同的关键部分。

驱动程序可以实现运行中断的关键部分中，通过提供的代码[ *SynchCritSection* ](https://msdn.microsoft.com/library/windows/hardware/ff563928)例程。 当使用该驱动程序[ **KeSynchronizeExecution** ](https://msdn.microsoft.com/library/windows/hardware/ff553302)调用*SynchCritSection*例程，系统会自动进入关键节中断通过指定*中断*参数。

引发到中断的同步 IRQL 防止被中断当前处理器的处理器的 IRQL，除非通过使用更高版本的同步 IRQL 中断。 获取数值调节钮锁会阻止其他处理器执行任何与该数值调节钮锁相关的关键部分代码。

当驱动程序调用时，系统将分配中断自旋锁和同步 IRQL 中断[ **IoConnectInterruptEx**](https://msdn.microsoft.com/library/windows/hardware/ff548378)。 在大多数情况下，该驱动程序可以允许系统以确定这两个值：

-   如果驱动程序使用 CONNECT\_行\_基于或 CONNECT\_消息\_基于版本的**IoConnectInterruptEx**，并指定**NULL**旋转锁，系统将分配旋转锁以在所有设备的中断之间都共享。 系统还确定同步 IRQL 值 （驱动程序可以选择指定较高的值）。 所有驱动程序的中断将共享相同的关键部分。

-   如果驱动程序使用 CONNECT\_完全\_的指定版本**IoConnectInterruptEx**并且具有仅单个中断矢量，可以指定驱动程序**NULL**旋转锁。 系统将为仅该特定的中断，将具有其自己的临界区的分配自旋锁。

仅当使用连接时，驱动程序必须分配数值调节钮锁定\_完全\_的指定版本**IoConnectInterruptEx**和时，它具有多个必须共享同一个严重的中断向量部分。 驱动程序可以通过使用指定其自己的自旋锁和同步 IRQL **SpinLock**并**SynchronizeIrql**的成员**IO\_CONNECT\_中断\_参数**。 有关详细信息，请参阅[ **IO\_CONNECT\_中断\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff550541)。

有关编写和进入临界区的信息，请参阅[使用临界区](using-critical-sections.md)。

 

 





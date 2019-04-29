---
title: 编写 ISR
description: 编写 ISR
ms.assetid: d696d683-e010-4a5c-ba2d-f536ab5f38b2
keywords:
- 中断服务例程 WDK 内核、 编写
- Isr WDK 内核、 编写
- 编写 Isr
- 中断对象 WDK 内核，编写 Isr
- I/O WDK 内核中断
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c3ec61d40e98171f5b0b173404b40d03dfec79e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355995"
---
# <a name="writing-an-isr"></a>编写 ISR





生成中断的物理设备的驱动程序必须具有至少一个中断服务例程 (ISR)。 ISR 必须执行任何适于到设备，以便消除可能包括停止设备从中断的中断。 然后，它应仅执行必要的操作要保存状态，并将队列 DPC 完成 I/O 操作在比 ISR 执行的较低优先级 (IRQL)。

在中断上下文中，在某些系统分配执行驱动程序的 ISR *DIRQL*按指定*SynchronizeIrql*参数[ **IoConnectInterruptEx**](https://msdn.microsoft.com/library/windows/hardware/ff548378).

Isr 可中断。 另一台设备具有更高版本的系统分配 DIRQL 可能会中断，或进行高 IRQL 系统中断，在任何时间。

系统调用 ISR 之前，它获取中断的旋转锁，因此 ISR 不能同时在另一个处理器上执行。 ISR 返回后，系统将释放自旋锁。

因为 ISR 运行在相对较高的 IRQL，关闭在当前处理器上的等效或更低的 IRQL 与中断会屏蔽，它应尽可能快地返回控制。 此外，在 DIRQL 运行 ISR 限制集的支持例程 ISR 可以调用。 有关详细信息，请参阅[管理硬件优先级](managing-hardware-priorities.md)。

通常情况下，ISR 执行下述常规步骤：

-   如果导致中断的设备不是所支持的 ISR，ISR 立即返回**FALSE**。

-   否则，ISR 清除中断如有必要，保存任何设备上下文是必需的和队列 DPC 来完成较低的 IRQL 在 I/O 操作。 请参阅[DPC 对象和 dpc 进行标记](dpc-objects-and-dpcs.md)有关详细信息。 然后必须返回 ISR **，则返回 TRUE**。

具体而言，在不重叠的 I/O 操作设备的驱动程序，ISR 应执行以下操作：

1.  确定是否虚假中断。 如果是这样，则返回**FALSE**立即因此 ISR 中断的设备将立即调用。 否则，继续执行中断处理。

2.  如有必要，请停止从中断，设备。

3.  收集任何上下文信息[ *DpcForIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff544079) (或[ *CustomDpc*](https://msdn.microsoft.com/library/windows/hardware/ff542972)) 将需要完成处理的 I/O 例程当前操作。

4.  将此上下文存储在可访问的区域*DpcForIsr*或*CustomDpc*例程，通常在处理当前的 I/O 请求引起的目标设备对象的设备扩展中中断。

    如果驱动程序与重叠的 I/O 操作，上下文信息必须包括的任何上下文以及完成 DPC 日常需求来完成每个请求所需的 DPC 例程的未完成请求的计数。 如果 ISR 调用之前已经运行了 DPC 处理另一个中断时，它必须不会覆盖尚未通过 DPC 完成的请求已保存的上下文。

5.  如果该驱动程序有*DpcForIsr*例程，调用[ **IoRequestDpc** ](https://msdn.microsoft.com/library/windows/hardware/ff549657)使用指向当前 IRP、 目标设备对象和已保存的上下文的指针。 **IoRequestDpc**队列*DpcForIsr*例程，以尽快 IRQL 低于调度运行\_级别处理器上。

    如果该驱动程序有*CustomDpc*例程，调用[ **KeInsertQueueDpc** ](https://msdn.microsoft.com/library/windows/hardware/ff552185)用一个指针指向 DPC 对象 (与关联*CustomDpc*例程) 和任何已保存的上下文指针*CustomDpc*例程将需要完成该操作。 通常情况下，ISR 还将指针传递给当前的 IRP 和目标设备对象。 *CustomDpc*只要 IRQL 低于调度运行时例程\_级别处理器上。

6.  返回 **，则返回 TRUE**以指示其设备生成中断。

一般情况下，ISR 执行任何实际的 I/O 处理，以满足 IRP。 相反，它会停止从中断其设备、 设置必要的状态信息，并进行排队，驱动程序的*DpcForIsr*或*CustomDpc*如何进行必要以满足当前的 I/O 处理导致要中断的设备的请求。

ISR 必须运行在 DIRQL 为可能的最短间隔。 遵循这些指导增加了在计算机中每个设备的 I/O 吞吐量，因为在 DIRQL 掩码关闭系统更小或相等的 IRQL 值分配到的所有中断运行。

*SynchronizeIrql*驱动程序的中断的对象，调用时，指定驱动程序**IoConnectInterrupt**，确定在其中执行驱动程序的 ISR DIRQL。 有关详细信息，请参阅[对设备数据的同步访问](synchronizing-access-to-device-data.md)。

 

 





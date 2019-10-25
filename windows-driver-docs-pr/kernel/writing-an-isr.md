---
title: 编写 ISR
description: 编写 ISR
ms.assetid: d696d683-e010-4a5c-ba2d-f536ab5f38b2
keywords:
- 中断服务例程 WDK 内核，写入
- Isr WDK 内核，写入
- 正在写入 Isr
- 中断对象 WDK 内核，写入 Isr
- I/o WDK 内核，中断
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6bb1969516ea13efeac7926399ed301cf724d76
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835593"
---
# <a name="writing-an-isr"></a>编写 ISR





用于生成中断的物理设备的驱动程序必须至少具有一个中断服务例程（ISR）。 ISR 必须执行适用于设备的任何操作，以消除中断，其中可能包括阻止设备中断。 然后，它只应执行保存状态并将 DPC 排队以使 i/o 操作的优先级（IRQL）超过 ISR 执行所需的内容。

驱动程序的 ISR 在中断上下文中执行，在某个系统分配的*DIRQL*中，由*SynchronizeIrql*参数指定给[**IoConnectInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterruptex)。

Isr 会被中断。 系统分配的 DIRQL 较高的其他设备可能会中断，或者可能会在任何时间中断高 IRQL 系统中断。

在系统调用 ISR 之前，它将获取中断的自旋锁，以便 ISR 无法在另一个处理器上同时执行。 ISR 返回后，系统释放旋转锁。

由于 ISR 以相对较高的 IRQL 运行，因此在当前处理器上屏蔽了等效或更低的 IRQL，因此应尽快返回 control。 此外，在 DIRQL 上运行 ISR 会限制 ISR 可以调用的支持例程集。 有关详细信息，请参阅[管理硬件优先级](managing-hardware-priorities.md)。

通常情况下，ISR 执行以下常规步骤：

-   如果导致中断的设备不是 ISR 支持的设备，则 ISR 会立即返回**FALSE**。

-   否则，ISR 会清除中断（如有必要），保存所需的任何设备上下文，并将 DPC 排队，以以较低的 IRQL 完成 i/o 操作。 有关详细信息，请参阅[Dpc 对象和 dpc](dpc-objects-and-dpcs.md) 。 ISR 必须返回**TRUE**。

具体而言，在不与设备 i/o 操作重叠的驱动程序中，ISR 应该执行以下操作：

1.  确定中断是否为伪中断。 如果是这样，则立即返回**FALSE** ，这样会立即调用被中断的设备的 ISR。 否则，请继续中断处理。

2.  如有必要，阻止设备中断。

3.  收集[*DpcForIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine) （或[*CustomDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kdeferred_routine)）例程为当前操作完成 i/o 处理所需的所有上下文信息。

4.  将此上下文存储在*DpcForIsr*或*CustomDpc*例程可访问的区域中，通常在处理当前 i/o 请求的目标设备对象的设备扩展中导致中断。

    如果驱动程序与 i/o 操作重叠，则上下文信息必须包括 DPC 例程需要完成的未处理请求数，以及 DPC 例程完成每个请求所需的任何上下文。 如果在 DPC 运行之前调用了 ISR 来处理另一中断，则不能覆盖 DPC 尚未完成的请求的已保存的上下文。

5.  如果驱动程序具有*DpcForIsr*例程，请调用[**IoRequestDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iorequestdpc) ，其中包含指向当前 IRP、目标设备对象和已保存上下文的指针。 **IoRequestDpc**会将*DpcForIsr*例程排队，使其在一个处理器上\_级别调度后立即运行。

    如果驱动程序具有*CustomDpc*例程，请使用指向 DPC 对象（与*CustomDpc*例程关联）的指针和指向任何已保存上下文的指针调用[**KeInsertQueueDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinsertqueuedpc) ， *CustomDpc*例程将需要完成运作. 通常，ISR 还会将指针传递到当前 IRP 和目标设备对象。 *CustomDpc*例程将在以下情况下运行： IRQL 降至低于在处理器上调度\_级别。

6.  返回**TRUE** ，指示其设备生成中断。

通常，ISR 不会进行实际的 i/o 处理来满足 IRP。 相反，它会阻止其设备中断、设置必要的状态信息，并将驱动程序的*DpcForIsr*或*CustomDpc*排队，以便执行任何所需的 i/o 处理，以满足导致设备中断的当前请求。

对于可能的最短间隔，ISR 必须在 DIRQL 上运行。 按照此指导原则增加了计算机中每台设备的 i/o 吞吐量，因为在 DIRQL 中运行时，会屏蔽系统为其分配了一个较低或相等 IRQL 值的所有中断。

驱动程序中断对象的*SynchronizeIrql* ，当驱动程序调用**IoConnectInterrupt**时指定，它确定驱动程序的 ISR 的执行 DIRQL。 有关详细信息，请参阅[同步对设备数据的访问](synchronizing-access-to-device-data.md)。

 

 





---
title: 使用 IoTimer 例程
description: 使用 IoTimer 例程
ms.assetid: 9de2d2ec-31c5-4a60-96bf-5da067d2d9db
keywords:
- IoTimer
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: cfdce82d30e5b083a47760e1e28aa51aa68da941
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361099"
---
# <a name="using-an-iotimer-routine"></a>使用 IoTimer 例程





启用关联的设备对象，尽管计时器[ *IoTimer* ](https://msdn.microsoft.com/library/windows/hardware/ff550381)例程称为大约每秒一次。 但是，因为在其中的每个间隔*IoTimer*例程称为取决于系统时钟的分辨率，不要假定*IoTimer*将上一秒中精确调用例程边界。

**请注意**   *IoTimer*例程，如所有 DPC 例程，称为在 IRQL = 调度\_级别。 DPC 例程时，会阻止所有线程在同一个处理器上运行。 驱动程序开发人员应仔细设计其*IoTimer*例程 brief 尽可能时间运行的。

 

可能是最常见用途*IoTimer*例程是 IRP 的超时时间设备 I/O 操作。 请考虑使用的以下情形*IoTimer*例程作为设备驱动程序中正在运行的计时器：

1.  启动设备时，驱动程序初始化为-1，指示没有当前设备 I/O 操作，并调用设备扩展中的计时器计数器[ **IoStartTimer** ](https://msdn.microsoft.com/library/windows/hardware/ff550373)之前它将返回状态\_成功。

    每次*IoTimer*调用例程，它检查是否计时器计数器为-1，并且，如果是这样，返回控件。

2.  在驱动程序[ *StartIo* ](https://msdn.microsoft.com/library/windows/hardware/ff563858)例程初始化到设定了一个上限，设备扩展中的计时器计数器加上其他用例中的第二个*IoTimer*例程仅具有已运行。 然后，它使用[ **KeSynchronizeExecution** ](https://msdn.microsoft.com/library/windows/hardware/ff553302)调用*SynchCritSection\_1*例程，程序请求的操作的物理设备当前的 IRP。

3.  驱动程序的 ISR 的驱动程序前，先将重置计时器计数器为-1 [ *DpcForIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff544079)例程或[ *CustomDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542972)例程。

4.  每次*IoTimer*调用例程，它将检查是否为-1，ISR 重置计时器计数器和，如果是这样，返回控件。 如果没有，则*IoTimer*例程使用**KeSynchronizeExecution**调用*SynchCritSection\_2*例程，它可通过一些调整计时器计数器驱动程序确定的秒数。

5.  *SynchCritSection\_2*例程返回**TRUE**到*IoTimer*例程，只要当前请求具有不已超时。如果计时器计数器回到零， *SynchCritSection\_2*例程将重置计时器计数器为驱动程序确定重置超时值、 重置预期标志设置为自身 (和*DpcForIsr*) 在其上下文区域中，尝试重置设备，并返回**TRUE**。

    *SynchCritSection\_2*如果将其重置操作还会超时在设备上，它返回时将再次调用例程**FALSE**。 如果其重置成功， *DpcForIsr*例程确定设备重置预期标志从已重置和重试请求，重复的操作*StartIo*例程所述在步骤 2 中。

6.  如果*SynchCritSection\_2*例程返回**FALSE**，则*IoTimer*例程假定物理设备是处于未知状态，因为尝试重置已失败。 在这些情况下， *IoTimer*例程队列*CustomDpc*例程，并返回。 这*CustomDpc*例程日志设备 I/O 错误，调用[ **IoStartNextPacket**](https://msdn.microsoft.com/library/windows/hardware/ff550358)、 失败当前 IRP，并返回。

如果此设备驱动程序 ISR 重置计数器为-1，共享的计时器，如中所述步骤 3 中，驱动程序的*DpcForIsr*例程完成当前的 IRP 中断驱动 I/O 处理。 重置计时器计数器指示，此设备 I/O 操作未超时，因此*IoTimer*例程不需要更改的计时器计数器。

在大多数情况下，前面*SynchCritSection\_2*例程只是计时器计数器。 *SynchCritSection\_2*例程会尝试将设备重置仅当前的 I/O 操作已超时，如果它是指示当计时器计数器回到零。 并尝试将设备重置已失败的情况下，才执行*SynchCritSection\_2*例程返回**FALSE**到*IoTimer*例程。

因此，这两个前面*IoTimer*例程和其帮助程序*SynchCritSection\_2*例程需要很少的时间才能在正常情况下执行。 通过使用*IoTimer*例程以这种方式，设备驱动程序可确保，可以重试每个有效的设备 I/O 请求，如有必要，并且*CustomDpc*例程将失败 IRP，仅当无法纠正硬件失败会阻止在满足从正在 IRP。 此外，驱动程序提供此功能在执行时间很少的费用。

上述方案的简单性取决于执行一次只有一个操作的设备和驱动程序，通常不重叠的 I/O 操作。 重叠的设备 I/O 操作，将执行的驱动程序或使用更高级别的驱动程序*IoTimer*例程超时的驱动程序分配 Irp 发送到多个系列的较低的驱动程序的一组将有更复杂的超时若要管理的方案。

 

 





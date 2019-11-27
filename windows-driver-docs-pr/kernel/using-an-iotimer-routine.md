---
title: 使用 IoTimer 例程
description: 使用 IoTimer 例程
ms.assetid: 9de2d2ec-31c5-4a60-96bf-5da067d2d9db
keywords:
- IoTimer
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e1d778be762313022af54994da9b24df5d5fef8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838364"
---
# <a name="using-an-iotimer-routine"></a>使用 IoTimer 例程





当关联设备对象的计时器处于启用状态时， [*IoTimer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_timer_routine)例程大约每秒调用一次。 但是，由于每个*IoTimer*例程的调用时间间隔取决于系统时钟的分辨率，因此不要假设*IoTimer*例程将在一秒边界内精确调用。

**请注意**  *IoTimer*例程（如所有 DPC 例程）在 IRQL = 调度\_级别调用。 当 DPC 例程运行时，将阻止所有线程在同一处理器上运行。 驱动程序开发人员应认真设计其*IoTimer*例程，使其尽可能简短地运行。

 

*IoTimer*例程的最常见用途可能是为 IRP 的设备 i/o 操作超时。 请考虑以下用于在设备驱动程序中使用*IoTimer*例程作为正在运行的计时器的方案：

1.  启动设备时，驱动程序会将设备扩展中的计时器计数器初始化为-1，指示没有当前设备 i/o 操作，并在 IoStartTimer 成功返回\_状态之前调用[](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostarttimer) 。

    每次调用*IoTimer*例程时，它都会检查计时器计数器是否为-1，如果是，则返回 control。

2.  驱动程序的[*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)例程将设备扩展中的计时器计数器初始化为上限，并在*IoTimer*例程刚刚运行的情况下将额外的秒初始化为第二次。 然后，它使用[**KeSynchronizeExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution)调用*SynchCritSection\_1*例程，该例程为物理设备提供当前 IRP 请求的操作的计划。

3.  驱动程序的 ISR 将计时器计数器重置为-1，然后对驱动程序的[*DpcForIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)例程或[*CustomDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kdeferred_routine)例程进行排队。

4.  每次调用*IoTimer*例程时，它都会检查 ISR 是否已由 ISR 重置为-1，如果是，则返回 control。 否则， *IoTimer*例程使用**KeSynchronizeExecution**调用*SynchCritSection\_2*例程，该例程会按驱动程序确定的秒数调整计时器计数器。

5.  只要当前请求尚未超时， *SynchCritSection\_2*例程就会向*IoTimer*例程返回**TRUE** 。如果计时器计数器的值为零，则*SynchCritSection\_2*例程会将计时器计数器重置为驱动程序确定的重置超时值，并在其上下文区域中为自身（对于*DpcForIsr*）设置一个重置预期标志，尝试重置设备，并返回**TRUE**。

    如果*SynchCritSection\_2*例程的重置操作也会在设备上超时，则会再次调用该**例程。** 如果其重置成功， *DpcForIsr*例程会确定设备已被重置预期标志重置并重试请求，如步骤2中所述，重复执行*StartIo*例程的操作。

6.  如果*SynchCritSection\_2*例程返回**FALSE**，则*IoTimer*例程假定物理设备处于未知状态，因为重置它的尝试已失败。 在这些情况下， *IoTimer*例程会将*CustomDpc*例程排队，并返回。 此*CustomDpc*例程记录设备 i/o 错误，调用[**IoStartNextPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartnextpacket)，失败当前 IRP，并返回。

如果此设备驱动程序的 ISR 将共享计时器计数器重置为-1 （如步骤3中所述），则驱动程序的*DpcForIsr*例程将完成当前 IRP 的中断驱动的 i/o 处理。 重置计时器计数器指示此设备 i/o 操作未超时，因此*IoTimer*例程不需要更改计时器计数器。

在大多数情况下，前面的*SynchCritSection\_2*例程只是减少计时器计数器。 *SynchCritSection\_2*例程尝试仅在当前 i/o 操作超时的情况下重置设备，当计时器计数器变为零时，将会指示这种情况。 仅当重置设备的尝试已失败时， *SynchCritSection\_2*例程会将**FALSE**返回到*IoTimer*例程。

因此，在正常情况下，前面的*IoTimer*例程及其 helper *SynchCritSection\_2*例程只需很少的时间。 通过以这种方式使用*IoTimer*例程，设备驱动程序可确保在必要时可以重试每个有效的设备 i/o 请求，并且仅当无法纠正的硬件故障导致 irp 无法满足时， *CustomDpc*例程才会失败。 而且，驱动程序在执行时间极少会提供此功能。

上述方案的简单性依赖于一种设备，该设备一次只执行一个操作，而在通常不会重叠 i/o 操作的驱动程序上执行该操作。 执行重叠的设备 i/o 操作的驱动程序，或者使用*IoTimer*例程将一组由驱动程序分配的 irp 发送到多个较低的驱动程序链的驱动程序，将具有更复杂的超时方案来进行管理。

 

 





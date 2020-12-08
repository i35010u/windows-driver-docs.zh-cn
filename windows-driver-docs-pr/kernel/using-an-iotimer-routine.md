---
title: 使用 IoTimer 例程
description: 使用 IoTimer 例程
keywords:
- IoTimer
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5fd62e1a88fb4427cbde1b84420c5f2b4e07d459
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825611"
---
# <a name="using-an-iotimer-routine"></a>使用 IoTimer 例程





当关联设备对象的计时器处于启用状态时， [*IoTimer*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_timer_routine) 例程大约每秒调用一次。 但是，由于每个 *IoTimer* 例程的调用时间间隔取决于系统时钟的分辨率，因此不要假设 *IoTimer* 例程将在一秒边界内精确调用。

**注意** *IoTimer* 例程（如所有 DPC 例程）在 IRQL = 调度级别进行调用 \_ 。 当 DPC 例程运行时，将阻止所有线程在同一处理器上运行。 驱动程序开发人员应认真设计其 *IoTimer* 例程，使其尽可能简短地运行。

 

*IoTimer* 例程的最常见用途可能是为 IRP 的设备 i/o 操作超时。 请考虑以下用于在设备驱动程序中使用 *IoTimer* 例程作为正在运行的计时器的方案：

1.  启动设备时，驱动程序会将设备扩展中的计时器计数器初始化为-1，指示没有当前设备 i/o 操作，并在返回状态 "成功" 之前调用 [**IoStartTimer**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostarttimer) \_ 。

    每次调用 *IoTimer* 例程时，它都会检查计时器计数器是否为-1，如果是，则返回 control。

2.  驱动程序的 [*StartIo*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio) 例程将设备扩展中的计时器计数器初始化为上限，并在 *IoTimer* 例程刚刚运行的情况下将额外的秒初始化为第二次。 然后，它使用 [**KeSynchronizeExecution**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution) 来调用 *SynchCritSection \_ 1* 例程，该例程为物理设备提供当前 IRP 请求的操作的计划。

3.  驱动程序的 ISR 将计时器计数器重置为-1，然后对驱动程序的 [*DpcForIsr*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine) 例程或 [*CustomDpc*](/windows-hardware/drivers/ddi/wdm/nc-wdm-kdeferred_routine) 例程进行排队。

4.  每次调用 *IoTimer* 例程时，它都会检查 ISR 是否已由 ISR 重置为-1，如果是，则返回 control。 否则， *IoTimer* 例程使用 **KeSynchronizeExecution** 调用 *SynchCritSection \_ 2* 例程，该例程根据驱动程序确定的秒数调整计时器计数器。

5.  只要当前请求尚未超时， *SynchCritSection \_ 2* 例程就会向 *IoTimer* 例程返回 **TRUE** 。如果计时器计数器的值为零，则 *SynchCritSection \_ 2* 例程会将计时器计数器重置为驱动程序确定的重置超时值，并为其本身 (和 *DpcForIsr*) 设置 "重置预期" 标志，尝试重置设备，并返回 **TRUE**。

    如果 *SynchCritSection \_ 2* 例程在设备上的重置操作也超时，则会再次调用 **它。** 如果其重置成功， *DpcForIsr* 例程会确定设备已被重置预期标志重置并重试请求，如步骤2中所述，重复执行 *StartIo* 例程的操作。

6.  如果 *SynchCritSection \_ 2* 例程返回 **FALSE**，则 *IoTimer* 例程会假定物理设备处于未知状态，因为重置它的尝试已失败。 在这些情况下， *IoTimer* 例程会将 *CustomDpc* 例程排队，并返回。 此 *CustomDpc* 例程记录设备 i/o 错误，调用 [**IoStartNextPacket**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartnextpacket)，失败当前 IRP，并返回。

如果此设备驱动程序的 ISR 将共享计时器计数器重置为-1 （如步骤3中所述），则驱动程序的 *DpcForIsr* 例程将完成当前 IRP 的中断驱动的 i/o 处理。 重置计时器计数器指示此设备 i/o 操作未超时，因此 *IoTimer* 例程不需要更改计时器计数器。

在大多数情况下，前面的 *SynchCritSection \_ 2* 例程只是递减计时器计数器。 仅当当前 i/o 操作已超时（当计时器计数器变为零时，才会显示）， *SynchCritSection \_ 2* 例程才会尝试重置设备。 仅当重置设备的尝试已失败时， *SynchCritSection \_ 2* 例程才会将 **FALSE** 返回到 *IoTimer* 例程。

因此，在正常情况下，上述 *IoTimer* 例程及其 helper *SynchCritSection \_ 2* 例程只需很少的时间。 通过以这种方式使用 *IoTimer* 例程，设备驱动程序可确保在必要时可以重试每个有效的设备 i/o 请求，并且仅当无法纠正的硬件故障导致 irp 无法满足时， *CustomDpc* 例程才会失败。 而且，驱动程序在执行时间极少会提供此功能。

上述方案的简单性依赖于一种设备，该设备一次只执行一个操作，而在通常不会重叠 i/o 操作的驱动程序上执行该操作。 执行重叠的设备 i/o 操作的驱动程序，或者使用 *IoTimer* 例程将一组由驱动程序分配的 irp 发送到多个较低的驱动程序链的驱动程序，将具有更复杂的超时方案来进行管理。

 


---
title: 为 I/O 操作分配控制器对象
description: 为 I/O 操作分配控制器对象
keywords:
- 控制器对象 WDK 内核，分配
- ControllerControl 例程，控制器对象分配
- IoAllocateController
- 分配控制器对象
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3135d881fa588d7ebc75f36c317d2a6fa77ec286
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836945"
---
# <a name="allocating-controller-objects-for-io-operations"></a>为 I/O 操作分配控制器对象





使用控制器对象的驱动程序启动其设备后，就可以处理发送到其目标设备对象的 Irp 了。 当 IRP 需要驱动程序对由控制器对象表示的物理设备进行 i/o 操作时，驱动程序将调用 [**IoAllocateController**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioallocatecontroller)。 下图说明了此类调用。

![说明如何为 i/o 分配控制器对象的关系图](images/3ctlaloc.png)

如上图所示，驱动程序必须提供超过 [**IoCreateController**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatecontroller)在调用 [**IoAllocateController**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioallocatecontroller)时返回的 *ControllerObject* 指针。 与此指针一起，它必须将指向表示当前 i/o 请求目标的设备对象的指针传递到驱动程序提供的 [*ControllerControl*](https://msdn.microsoft.com/library/windows/hardware/ff542049)例程，并将其传递到其 *ControllerControl* 例程为所请求的 i/o 操作设置设备的任何 *上下文*。

如果控制器对象表示的设备忙， **IoAllocateController** 将对驱动程序提供的 *ControllerControl* 例程进行排队。 否则，会立即用上图中显示的输入参数调用 *ControllerControl* 例程。 当运行时，将 **IoAllocateController** 的输入 *上下文* 指针传递给驱动程序的 *ControllerControl* 例程。

使用以下准则来确定存储上下文信息的位置：

-   驱动程序提供的上下文区域不应在控制器扩展中，除非驱动程序先处理每个 IRP 才能完成，然后再在物理控制器上启动另一操作。 否则，控制器扩展中的上下文区域可能会被其他驱动程序例程覆盖，或在收到新的 IRP 时被覆盖。

-   即使驱动程序与其他设备对象的设备 i/o 操作重叠，也无法覆盖目标设备对象的设备扩展中的上下文区域。

-   如果对某个特定设备对象进行了另一个 i/o 请求，但该驱动程序具有 [*StartIo*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio) 例程，则其设备扩展中的上下文区域也无法被覆盖，因为当驱动程序调用 [**IoStartPacket**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartpacket) 时传入的 irp 将排队，并且同一 IRP 将保留在设备队列中，直到该驱动程序在完成该设备对象的当前 IRP 之前调用 [**IoStartNextPacket**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartnextpacket) 。

*DeviceObject* - &gt; **CurrentIrp** 如果驱动程序有 *StartIo* 例程，则 i/o 管理器会将 DeviceObject CurrentIrp 的指针传递到 *ControllerControl* 例程。 如果驱动程序管理自己的 Irp 队列，而不是使用 *StartIo* 例程，则 i/o 管理器无法为 *ControllerControl* 例程指定指向当前 IRP 的指针。 当驱动程序调用 **IoAllocateController** 时，它应将当前 IRP 作为 *上下文* 可访问的数据的一部分传递。

调用 IoAllocateController 时，必须在 IRQL = 调度级别执行调用 **IoAllocateController** 的驱动程序例程 \_ 。 从其 *StartIo* 例程进行此调用的驱动程序已在调度级别运行 \_ 。

*ControllerControl* 例程为 IRP 请求的操作设置物理控制器。

如上图所示， *ControllerControl* 例程返回类型为 " [**IO \_ 分配 \_ 操作**](/windows-hardware/drivers/ddi/wdm/ne-wdm-_io_allocation_action)" 的值，它可以是以下系统定义的值之一：

-   如果 *ControllerControl* 例程可以在物理控制器上启动另一操作，它应返回 **DeallocateObject** ，以便驱动程序可以与下一个请求的 i/o 操作重叠。

    例如，如果 *ControllerControl* 例程可以对某个磁盘上的查找操作进行编程，完成该 IRP 并返回 **DeallocateObject**，则可以再次调用 *ControllerControl* 例程，以便在其他磁盘上当前排队的任何传输请求时对磁盘控制器进行编程，以便对该磁盘进行传输操作。

-   如果当前 IRP 需要由其他驱动程序例程进一步处理，则 *ControllerControl* 例程必须返回 **KeepObject**。

    例如，如果驱动程序将磁盘控制器用于传输操作，但在传输完成之前无法完成 IRP，则 *ControllerControl* 例程必须返回 **KeepObject**。

当 *ControllerControl* 例程返回 **KeepObject** 时，通常情况下，驱动程序的 ISR 在设备中断时运行，并且其 [*DpcForIsr*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine) 或 [*CustomDpc*](/windows-hardware/drivers/ddi/wdm/nc-wdm-kdeferred_routine) 例程完成 i/o 操作，并且当前 IRP 用于目标设备对象。

每当 *ControllerControl* 例程返回 **KeepObject** 时，完成 IRP 的例程都必须调用 [**IoFreeController**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iofreecontroller)。 此类驱动程序例程应该尽快调用 **IoFreeController** ，以便可以立即设置其下一设备 i/o 操作。

 


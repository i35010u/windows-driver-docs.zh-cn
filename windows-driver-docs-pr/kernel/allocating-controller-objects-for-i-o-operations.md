---
title: 为 I/O 操作分配控制器对象
description: 为 I/O 操作分配控制器对象
ms.assetid: 8a5e3741-f8ea-4e27-bb7f-6c20da1d618d
keywords:
- 控制器对象 WDK 内核，分配
- ControllerControl 例程，控制器对象分配
- IoAllocateController
- 分配控制器对象
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3cde992b60248b28a62a25e924c5c187753cc4d1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828643"
---
# <a name="allocating-controller-objects-for-io-operations"></a>为 I/O 操作分配控制器对象





使用控制器对象的驱动程序启动其设备后，就可以处理发送到其目标设备对象的 Irp 了。 当 IRP 需要驱动程序对由控制器对象表示的物理设备进行 i/o 操作时，驱动程序将调用[**IoAllocateController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioallocatecontroller)。 下图说明了此类调用。

![说明如何为 i/o 分配控制器对象的关系图](images/3ctlaloc.png)

如上图所示，驱动程序必须提供超过[**IoCreateController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatecontroller)在调用[**IoAllocateController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioallocatecontroller)时返回的*ControllerObject*指针。 除了此指针，它还必须将指向表示当前 i/o 请求目标的设备对象的指针传递给驱动程序提供的[*ControllerControl*](https://msdn.microsoft.com/library/windows/hardware/ff542049)例程，并将其传递到其*ControllerControl*例程需要的任何*上下文*为请求的 i/o 操作设置设备。

如果控制器对象表示的设备忙， **IoAllocateController**将对驱动程序提供的*ControllerControl*例程进行排队。 否则，会立即用上图中显示的输入参数调用*ControllerControl*例程。 当运行时，将**IoAllocateController**的输入*上下文*指针传递给驱动程序的*ControllerControl*例程。

使用以下准则来确定存储上下文信息的位置：

-   驱动程序提供的上下文区域不应在控制器扩展中，除非驱动程序先处理每个 IRP 才能完成，然后再在物理控制器上启动另一操作。 否则，控制器扩展中的上下文区域可能会被其他驱动程序例程覆盖，或在收到新的 IRP 时被覆盖。

-   即使驱动程序与其他设备对象的设备 i/o 操作重叠，也无法覆盖目标设备对象的设备扩展中的上下文区域。

-   如果对某个特定设备对象发出了另一个 i/o 请求，但该驱动程序具有[*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)例程，则不能覆盖其设备扩展中的上下文区域，因为当驱动程序调用[**IOSTARTPACKET**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartpacket)时传入 IRP 将排队，与在完成该设备对象的当前 IRP 之前，该驱动程序调用[**IoStartNextPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartnextpacket)之前，同一 IRP 将保留在设备队列中。

如果驱动程序有*StartIo*例程，则 i/o 管理器会将指向*DeviceObject*-&gt;**CurrentIrp**的指针传递到*ControllerControl*例程。 如果驱动程序管理自己的 Irp 队列，而不是使用*StartIo*例程，则 i/o 管理器无法为*ControllerControl*例程指定指向当前 IRP 的指针。 当驱动程序调用**IoAllocateController**时，它应将当前 IRP 作为*上下文*可访问的数据的一部分传递。

调用**IoAllocateController**时，必须在 IRQL = 调度\_级别执行调用的驱动程序例程。 从其*StartIo*例程进行此调用的驱动程序已在调度\_级别运行。

*ControllerControl*例程为 IRP 请求的操作设置物理控制器。

如上图所示， *ControllerControl*例程返回类型为[**IO\_分配\_操作**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_io_allocation_action)的值，它可以是以下系统定义的值之一：

-   如果*ControllerControl*例程可以在物理控制器上启动另一操作，它应返回**DeallocateObject** ，以便驱动程序可以与下一个请求的 i/o 操作重叠。

    例如，如果*ControllerControl*例程可以对某个磁盘上的查找操作进行编程，完成该 IRP 并返回**DeallocateObject**，则可以再次调用*ControllerControl*例程来对磁盘进行编程。如果传输请求当前在其他磁盘上排队，则该控制器用于在另一个磁盘上进行传输操作。

-   如果当前 IRP 需要由其他驱动程序例程进一步处理，则*ControllerControl*例程必须返回**KeepObject**。

    例如，如果驱动程序将磁盘控制器用于传输操作，但在传输完成之前无法完成 IRP，则*ControllerControl*例程必须返回**KeepObject**。

当*ControllerControl*例程返回**KeepObject**时，通常驱动程序的 ISR 在设备中断时运行，其[*DpcForIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)或[*CustomDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kdeferred_routine)例程完成 i/o 操作，并为目标设备完成当前 IRP对象.

每当*ControllerControl*例程返回**KeepObject**时，完成 IRP 的例程都必须调用[**IoFreeController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iofreecontroller)。 此类驱动程序例程应该尽快调用**IoFreeController** ，以便可以立即设置其下一设备 i/o 操作。

 

 





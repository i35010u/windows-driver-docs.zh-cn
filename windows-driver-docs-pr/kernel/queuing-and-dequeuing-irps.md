---
title: 排队和取消排队 IRP
description: 排队和取消排队 IRP
keywords:
- Irp WDK 内核，队列
- 队列 Irp
- 出列的 Irp
- 多个 i/o 请求处理 WDK 内核
- 内部 IRP 队列 WDK 内核
- 同步 WDK Irp
- 启动 i/o 操作
- I/o WDK 内核，操作开始
- StartIo 例程
- 取消安全 IRP 队列 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1a99d85c8ec2a80dd4a8282c7a2886abd7afac8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805371"
---
# <a name="queuing-and-dequeuing-irps"></a>排队和取消排队 IRP





因为 i/o 管理器支持多任务和多线程系统内的异步 i/o，所以，对设备的 i/o 请求的速度可能比驱动程序可处理完成的速度快，尤其是在多处理器计算机上。 因此，当绑定到任何特定设备的 Irp 正在忙于处理另一 IRP 时，该驱动程序必须在该驱动程序中排入队列。

因此，最低级别的驱动程序需要以下项之一：

-   [*StartIo*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)例程（i/o 管理器调用此例程来启动对 irp 的 i/o 操作，驱动程序已排入系统提供的 irp 队列 (参阅 [**IoStartPacket**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartpacket)) 。

-   内部 IRP 排队和出列机制，驱动程序使用该机制来管理比能够满足其速度更快的 Irp。 驱动程序可以使用设备队列、联锁队列或取消安全队列。 有关详细信息，请参阅 [驱动程序管理的 IRP 队列](driver-managed-irp-queues.md)。

只有可满足并在其调度例程中完成每个可能的 IRP 的最低级别设备驱动程序无需 *StartIo* 例程，并且不需要用于 irp 的驱动程序托管队列。

较高级别的驱动程序几乎没有 *StartIo* 例程。 大多数中间驱动程序既没有 *StartIo* 例程，也没有内部队列;中间驱动程序通常可以通过其调度例程传递包含有效参数的 Irp，并执行其 [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程中的任何 IRP 所需的任何后处理操作。

下面通常介绍一些设计注意事项，这些注意事项用于确定是否实现带有或不带内部驱动程序管理的 Irp 的 *StartIo* 例程。

### <a name="startio-routines-in-drivers"></a>驱动程序中的 StartIo 例程

对于能够一次只处理一个设备 i/o 操作的计算机外设设备，设备驱动程序可以实现 *StartIo* 例程。 对于这些驱动程序，i/o 管理器提供了 [**IoStartPacket**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartpacket) 和 [**IoStartNextPacket**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartnextpacket) 例程，用于在系统提供的 Irp 队列中对 irp 进行排队和取消排队。

有关 *StartIo* 例程的详细信息，请参阅 [编写 StartIo 例程](writing-a-startio-routine.md)。

### <a name="internal-queues-for-irps-in-drivers"></a>驱动程序中的 Irp 的内部队列

如果设备可以支持多个并发 i/o 操作，则其最低级别的设备驱动程序必须设置内部请求队列并管理其自己的 Irp 队列。 例如，系统序列驱动程序会在其设备上维护单独的队列，以便进行读、写、清除和等待操作，因为该驱动程序支持全双工串行设备。

将请求发送到一定数量的基础设备驱动程序的较高级别的驱动程序也可能维护 Irp 的内部队列。 例如，文件系统驱动程序几乎始终具有用于 Irp 的内部队列。

有关详细信息，请参阅 [驱动程序管理的 IRP 队列](driver-managed-irp-queues.md)。

### <a name="internal-queue-synchronization"></a>内部队列同步

具有设备专用线程的驱动程序和使用执行工作线程的最高级别的驱动程序 (包括大多数文件系统驱动程序) 通常为 Irp 设置自己的队列。 队列由驱动程序线程或驱动程序提供的工作线程回调以及处理 Irp 的其他驱动程序例程共享。

实现其自己的队列结构的驱动程序必须确保对队列的访问是同步的，并且取消的 Irp 将从队列中删除。 若要使此任务更简单地用于驱动程序编写器，请取消安全 IRP 队列提供可在实现 IRP 队列时使用的标准框架。 有关详细信息，请参阅 [取消安全 IRP 队列](cancel-safe-irp-queues.md) 。 这是实现 IRP 队列的首选方法。

驱动程序还可以完全实现 IRP 队列同步和取消逻辑。 例如，驱动程序可以使用联锁队列。 驱动程序的调度例程将 Irp 插入到联锁队列，驱动程序创建的线程或驱动程序的工作线程回调会通过调用 **ExInterlocked *Xxx* 列表** 支持例程来删除它们。

例如，系统软盘控制器驱动程序使用联锁队列。 其专用设备线程处理的 Irp 处理方式与其他设备驱动程序的 *StartIo* 例程处理相同，并处理其他设备驱动程序的 [*DpcForIsr*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine) 例程所执行的一些相同的 irp 处理。

### <a name="internal-queues-with-startio-routines-in-drivers"></a>包含驱动程序中的 StartIo 例程的内部队列

管理自己的内部队列的驱动程序还可以有 *StartIo* 例程，但不需要。 最底层的设备驱动程序具有 *StartIo* 例程或管理其各自的 irp 队列，但不能同时使用两者。

这种情况的一个例外是 SCSI 端口驱动程序，它具有 *StartIo* 例程并管理 irp 的内部队列。 I/o 管理器将 Irp 排队到端口驱动程序的 *StartIo* 例程上，该设备队列与代表 SCSI HBA 的驱动程序创建设备对象相关联。 SCSI 端口驱动程序还会为每个目标设备设置和管理用于 Irp 的设备队列 (对应于计算机中任何 HBA 驱动的 SCSI 总线上的 SCSI 逻辑单元) 。

当 SCSI 总线上的任何设备特别忙碌时，SCSI 端口驱动程序使用其补充设备队列来保存从 LU 特定队列的 SCSI 类驱动程序中发送的 Irp。 实际上，此驱动程序的补充，LU 特定的设备队列允许 SCSI 端口驱动程序通过 HBA 序列化异类 SCSI 设备的操作，同时使该 HBA 的 SCSI 总线上的每个设备尽可能忙碌。

 


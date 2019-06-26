---
title: 排队和取消排队 IRP
description: 排队和取消排队 IRP
ms.assetid: 736107bf-4790-4562-8785-c37fbbed03d3
keywords:
- Irp WDK 内核队列
- 队列的 Irp
- 取消排队的 Irp
- 处理 WDK 内核的多个 I/O 请求
- 内部 IRP 队列 WDK 内核
- 同步 WDK Irp
- 启动 I/O 操作
- I/O WDK 内核，启动的操作
- StartIo 例程
- 取消安全 IRP 队列 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 04ff9062fc46d403ecd8bbcc4db244431b459e52
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378755"
---
# <a name="queuing-and-dequeuing-irps"></a>排队和取消排队 IRP





由于 I/O 管理器支持多任务处理和多线程的系统中的异步 I/O，I/O 请求到设备可以有高于其驱动程序处理完后，尤其是在多处理器计算机速度更快。 因此，绑定到任何特定设备的 Irp 必须排队驱动程序中已忙于处理另一个 IRP 其设备时。

因此，最低级别驱动程序需要以下项之一：

-   一个[ *StartIo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)例程，该驱动程序的启动 I/O 操作的 Irp 调用 I/O 管理器已排队到系统提供 IRP 队列 (请参阅[ **IoStartPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iostartpacket)).

-   一个内部 IRP 队列和驱动程序用于管理比它更快地进入的 Irp 的取消排队机制可以满足它们。 驱动程序可以使用设备队列、 互锁的队列或取消安全队列。 有关详细信息，请参阅[Driver-Managed IRP 队列](driver-managed-irp-queues.md)。

仅可满足并完成其调度例程中的每个可能 IRP 的最低级别的设备驱动程序需要否*StartIo*例程和 Irp 的任何驱动程序管理队列。

更高级别的驱动程序几乎不用*StartIo*例程。 大多数中间驱动程序有都*StartIo*例程，也不内部队列; 中间驱动程序通常可以将 Irp 使用有效的参数传递，从其调度例程并执行任何后续处理所需在任何 IRP其[ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)例程。

下面介绍，一般情况下，一些用于确定是否实现的设计注意事项*StartIo*例程使用或不为 Irp 的内部、 驱动程序管理队列。

### <a name="startio-routines-in-drivers"></a>驱动程序中的 StartIo 例程

对于计算机能够处理一次只有一个设备 I/O 操作的外围设备，设备驱动程序可以实现*StartIo*例程。 对于这些驱动程序，I/O 管理器提供了[ **IoStartPacket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iostartpacket)并[ **IoStartNextPacket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iostartnextpacket)例程来排队和取消排队到 Irp 和从系统提供 IRP 队列。

有关详细信息*StartIo*例程，请参阅[编写 StartIo 例程](writing-a-startio-routine.md)。

### <a name="internal-queues-for-irps-in-drivers"></a>有关驱动程序中的 Irp 的内部队列

如果设备可以支持多个并发 I/O 操作，其最低级别的设备驱动程序必须设置内部请求队列，并管理其自己的 Irp 的队列。 例如，系统串行驱动程序维护单独的队列，用于读取、 写入、 清除，和等待其设备上的操作，因为它支持全双工串行设备。

将请求发送到基础设备驱动程序的一些更高级别的驱动程序还可能维护 Irp 的内部的队列。 例如，文件系统驱动程序几乎总是具有 Irp 内部队列。

有关详细信息，请参阅[Driver-Managed IRP 队列](driver-managed-irp-queues.md)。

### <a name="internal-queue-synchronization"></a>内部队列同步

使用设备专用线程和使用 executive 工作线程数 （包括大多数文件系统驱动程序） 通常他们自己队列为设置 Irp 的最高级别的驱动程序的驱动程序。 队列被共享由驱动程序线程或驱动程序所提供的工作线程回调和处理 Irp 其他驱动程序例程。

对队列的访问同步以及如何从队列删除的已取消的 Irp，必须确保实现其自己的队列结构的驱动程序。 若要使此任务更简单的驱动程序编写人员，取消安全 IRP 队列提供实现 IRP 队列时可以使用一个标准框架。 请参阅[取消安全 IRP 队列](cancel-safe-irp-queues.md)有关详细信息。 这是用于实现 IRP 队列的首选的方法。

驱动程序还可以实现所有 IRP 队列同步并显式取消逻辑。 例如，驱动程序可以使用互锁的队列。 驱动程序的调度例程中插入 Irp 互锁的队列和驱动程序创建线程或驱动程序的工作线程回调将其删除通过调用**ExInterlocked*Xxx*列表**支持例程。

例如，系统软盘控制器驱动程序使用互锁的队列。 其设备专用的线程处理通过在其他设备驱动程序的相同处理的 Irp *StartIo*例程以及一些可通过其他设备驱动程序的相同处理的 Irp [ *DpcForIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_dpc_routine)例程。

### <a name="internal-queues-with-startio-routines-in-drivers"></a>内部队列中的驱动程序的 StartIo 例程

管理其自己的内部队列的驱动程序还可以*StartIo*例程，但不是需要。 大多数最低级别的设备驱动程序有两种： *StartIo*例程或管理其自己的 Irp，但不是能同时队列。

一种例外是 SCSI 端口驱动程序，它具有*StartIo*例程，并管理的 Irp 的内部队列。 I/O 管理器到端口驱动程序的队列 Irp *StartIo*例程与表示 SCSI HBA 驱动程序创建的设备对象关联的设备队列中。 SCSI 端口驱动程序还将设置为和管理设备队列 Irp 到每个目标设备 （对应于 SCSI 逻辑单元） 计算机中任何 HBA 驱动 SCSI 总线上。

SCSI 端口驱动程序使用其补充设备队列来保存 Irp 发送从特定于 LU 的队列中的 SCSI 类驱动程序时特别繁忙的 SCSI 总线上的任何设备。 实际上，此驱动程序的补充、 特定于 LU 的设备队列允许 SCSI 端口驱动程序，同时保持该 HBA SCSI 总线上的每个设备尽可能序列化用于异类 SCSI 设备都通过 HBA 的操作。

 

 





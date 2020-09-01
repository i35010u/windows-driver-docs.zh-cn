---
title: 管理设备队列
description: 管理设备队列
ms.assetid: 8b7d39f8-0449-4e9b-a54c-fe60ee60842c
keywords:
- 设备队列 WDK Irp，管理
- 补充 IRP 队列 WDK 内核
- StartIo 例程，补充设备队列
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 463a5ef9070415f3c4cdd820f3f009ad8c934103
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187939"
---
# <a name="managing-device-queues"></a>管理设备队列





当驱动程序调用 [**IoCreateDevice**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)时，i/o 管理器通常 (除了 FSDs) 创建关联的设备队列对象。 它还提供了 [**IoStartPacket**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartpacket) 和 [**IoStartNextPacket**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartnextpacket)，驱动程序可调用这些驱动程序将 irp 插入关联的设备队列，或调用其 [*StartIo*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio) 例程。

因此，很少需要 (或特别有用的) 为驱动程序设置自己的用于 Irp 的设备队列对象。 可能的候选项是驱动程序，如 SCSI 端口驱动程序，必须将传入的 Irp 与通过单个控制器或总线适配器提供服务的异类设备的某些紧密耦合类驱动程序坐标。

换句话说，磁盘阵列控制器的驱动程序更有可能使用驱动程序创建的控制器对象，而不是 (s) 设置补充设备队列对象，而用于外接程序总线适配器的驱动程序和一组类驱动程序的驱动程序更有可能使用补充设备队列。

### <a name="using-supplemental-device-queues-with-a-startio-routine"></a>结合使用补充设备队列和 StartIo 例程

通过调用 **IoStartPacket** 和 **IoStartNextPacket**，驱动程序的调度和 [*DpcForIsr*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine) (或 [*CustomDpc*](/windows-hardware/drivers/ddi/wdm/nc-wdm-kdeferred_routine)) 例程使用当驱动程序创建设备对象时，i/o 管理器创建的设备队列来同步对其 *StartIo* 例程的调用。 对于带有 *StartIo* 例程的端口驱动程序， **IoStartPacket** 和 **IoStartNextPacket** 在端口驱动程序的共享设备控制器/适配器的设备队列中插入和删除 irp。 如果端口驱动程序还设置补充设备队列来容纳来自紧密耦合的更高级别类驱动程序的请求，则它必须将传入的 Irp "排序" 到其补充设备队列，通常在其 *StartIo* 例程中。

端口驱动程序必须确定每个 IRP 所属的补充设备队列，然后再尝试将该 IRP 插入到相应的队列中。 指向目标设备对象的指针将与 IRP 一起传递到驱动程序的调度例程。 驱动程序应保存指针以在传入的 Irp 的 "排序" 中使用。 请注意，传递到 *StartIo* 例程的设备对象指针是驱动程序自己的设备对象，表示设备控制器/适配器，因此不能用于此目的。

对任何 Irp 进行排队后，驱动程序会将其共享控制器/适配器用于执行请求。 因此，在对 [**KeInsertDeviceQueue**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keinsertdevicequeue) 的调用将 IRP 放入特定类驱动程序的设备队列之前，端口驱动程序可以首先处理所有设备的传入请求。

通过使用其自己的设备队列通过其 *StartIo* 例程处理所有 irp，基础端口驱动程序通过共享设备将操作序列化， (或总线) 控制器/适配器连接到所有连接的设备。 通过在单独的设备队列中保存每个受支持设备的 Irp，此端口驱动程序会禁止为已繁忙的设备处理 Irp，同时增加通过其共享硬件执行 i/o 的每个设备的 i/o 吞吐量。

为了响应从端口驱动程序的调度例程对 **IoStartPacket** 的调用，i/o 管理器会立即调用该驱动程序的 *StartIo* 例程，或将 IRP 放入与端口驱动程序的共享控制器/适配器的设备对象关联的设备队列中。

端口驱动程序必须维护其自己的有关它通过共享设备控制器/适配器服务的每个异类设备的状态信息。

**在用补充设备队列设计类/端口驱动程序时，请注意以下事项：**

-   驱动程序无法轻松获取指向其自身所在的任何驱动程序所创建的设备对象（其设备堆栈顶部的设备对象除外）的指针。

    按照设计，i/o 管理器不提供获得此类指针的支持例程。 而且，驱动程序的加载顺序使得驱动程序越低，驱动程序也无法获取更高级别的驱动程序的指针，这些对象在任何较低级别的驱动程序添加其设备时尚未创建。

    尽管 **IoGetAttachedDeviceReference** 返回指向驱动程序堆栈中最高级别的设备对象的指针，但驱动程序只应使用此指针为其堆栈指定 i/o 请求的目标。 驱动程序不应尝试读取或写入设备对象。

-   除了将请求发送到其自己的设备堆栈顶部以外，驱动程序不能使用指向其自身所创建的任何驱动程序所创建的设备对象的指针。

    没有办法同步访问单个设备对象 (及其设备扩展) 两个驱动程序之间以多处理器安全的方式进行。 两个驱动程序都不能对另一个驱动程序当前正在进行的 i/o 处理作出任何假设。

即使对于紧密耦合的类/端口驱动程序，每个类驱动程序都应使用指向端口驱动程序的设备对象的指针， (s) 只是通过 **IoCallDriver**传递 irp。 基础端口驱动程序必须维护其自己的状态（可能位于端口驱动程序的设备扩展中），关于它为任何紧密耦合的类驱动 (程序处理的请求（) "设备 () ）。

### <a name="managing-supplemental-device-queues-across-driver-routines"></a>跨驱动程序例程管理补充设备队列

对于紧耦合的类驱动程序，将补充设备队列中的 Irp 排队的任何端口驱动程序也必须有效地处理以下情况：

1.  其调度例程为该设备插入了驱动程序创建的设备队列中特定设备的 Irp。

2.  其他设备的 Irp 继续进入，并使用**IoStartPacket**将其排入驱动程序的*StartIo*例程，并通过共享设备控制器进行处理。

3.  设备控制器不会进入空闲状态，但包含在驱动程序创建的设备队列中的每个 IRP 还必须尽快排入驱动程序的 *StartIo* 例程。

因此，每当端口驱动程序完成 IRP 时，端口驱动程序的 *DpcForIsr* 例程必须尝试将 irp 从特定设备的驱动程序的内部设备队列传输到共享适配器/控制器的设备队列中，如下所示：

1.  *DpcForIsr*例程调用**IoStartNextPacket** ，使*StartIo*例程开始处理排队到共享设备控制器的下一个 IRP。

2.  *DpcForIsr*例程会调用[**KeRemoveDeviceQueue**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keremovedevicequeue)来取消下一个 IRP (，前提是它在该设备的内部设备队列中持有的任何) 都将完成 IRP。

3.  如果 **KeRemoveDeviceQueue** 返回非 NULL 指针，则 *DpcForIsr* 例程将使用刚刚取消排队的 IRP 调用 **IoStartPacket** ，使其排队等候共享设备控制器/适配器。 否则，对 **KeRemoveDeviceQueue** 的调用只是将设备队列对象的状态重置为不忙， *DpcForIsr* 例程将忽略对 **IoStartPacket**的调用。

4.  然后， *DpcForIsr* 例程使用输入 IRP 调用 [**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) ，其中，端口驱动程序已完成 i/o 处理，方法是将 i/o 状态块设置为错误或满足 i/o 请求。

请注意，前面的序列表示 *DpcForIsr* 例程还必须确定完成当前 (输入) IRP 的设备，以便有效地管理 irp 的内部队列。

如果端口驱动程序在其补充设备队列中挂起的 Irp 之前，尝试等待其共享控制器/适配器处于空闲状态，则驱动程序可能会枯竭需要较高 i/o 要求的设备，同时，该设备会向每个当前 i/o 需求实际太浅的其他设备提供响应。

 


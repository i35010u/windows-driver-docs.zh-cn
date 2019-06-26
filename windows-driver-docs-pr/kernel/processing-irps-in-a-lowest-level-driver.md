---
title: 在最低级驱动程序中处理 IRP
description: 在最低级驱动程序中处理 IRP
ms.assetid: 9b8c2586-d47b-49ab-bf65-a298af36304c
keywords:
- Irp WDK 内核，处理示例
- Irp WDK 内核，I/O 状态数据块
- I/O 状态块 WDK 内核
- 状态块 WDK 内核
- IoStartNextPacket
- IoCompleteRequest
- IoRequestDpc
- AllocateAdapterChannel
- MapTransfer
- IoStartPacket
- IoMarkIrpPending
- IoGetCurrentIrpStackLocation
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2af990ffb007eaa2070157c3864de358198ac32c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378830"
---
# <a name="processing-irps-in-a-lowest-level-driver"></a>在最低级驱动程序中处理 IRP





最低级别物理驱动程序具有更高级别的驱动程序不需要某些标准例程。 最低级别的驱动程序的标准例程集根据以下条件各不相同：

-   每个驱动程序控制的设备的性质

-   该驱动程序是否设置了其设备对象的直接或缓冲 I/O

-   单独的驱动程序的设计

为了说明标准驱动程序例程的角色下, 图显示的路径 IRP 可能需要的最低级别的大容量存储设备驱动程序处理时的示例。 在图中的驱动程序具有以下特征：

-   设备会生成中断末尾的每个 I/O 操作，因此，此驱动程序必须 ISR 和[ *DpcForIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_dpc_routine)例程。

-   该驱动程序有[ *StartIo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)例程，而不是为 Irp 设置内部队列和管理其自己的队列。

-   驱动程序使用系统 DMA，因此，设置其设备对象的**标志**针对直接 I/O，并具有[ *AdapterControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_control)例程。

![说明通过最低级别驱动程序例程的 irp 途径的关系图](images/4loddirp.png)

如此图所示，I/O 管理器创建 IRP，并将其发送到给定的主要函数代码的驱动程序的调度例程。 假设函数代码是任一[ **IRP\_MJ\_读取**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)或者[ **IRP\_MJ\_编写**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)，调度例程**DDDispatchReadWrite**。

### <a name="calling-iogetcurrentirpstacklocation"></a>Calling IoGetCurrentIrpStackLocation

必须调用需要 IRP 参数的任何驱动程序例程[ **IoGetCurrentIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetcurrentirpstacklocation)若要获取的驱动程序[I/O 堆栈位置](i-o-stack-locations.md)。 此类例程包含处理多个主要的 I/O 函数代码的调度例程 (<strong>IRP\_MJ\_* XXX</strong><em>)，处理支持次要函数的函数 (</em> <em>IRP\_MN\_</em>XXX<strong><em>)，或处理设备 I/O 控制请求 ([</em>* IRP\_MJ\_设备\_控制</strong>](<https://msdn.microsoft.com/library/windows/hardware/ff550744>)和/或[ **IRP\_MJ\_内部\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control))，以及每个处理 IRP 其他驱动程序例程。

此驱动程序的 I/O 堆栈位置是最小，具有更高级别的驱动程序 I/O 堆栈位置显示阴影数量不确定。 为简单起见，调用**IoGetCurrentIrpStackLocation**从[ *DispatchReadWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)， *StartIo*， *AdapterControl*，并[ *DpcForIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_dpc_routine)例程未显示在上图中。

### <a name="calling-iomarkirppending-and-iostartpacket"></a>调用 IoMarkIrpPending 和 IoStartPacket

示例驱动程序不会完成 IRP 在其调度例程中，但改为处理 IRP 中的其*StartIo*例程。 它可以执行此操作之前，调用的调度例程[ **IoMarkIrpPending** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iomarkirppending)以指示尚未完成 IRP。 然后，调用[ **IoStartPacket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iostartpacket)排队进行进一步处理驱动程序的 IRP *StartIo*例程。 调度例程也会返回 NTSTATUS 值状态\_PENDING。

下图说明了在调用**IoStartPacket**。

![说明对 iostartpacket 的调用关系图](images/4strtpak.png)

如果该驱动程序正忙于处理另一个在设备上的 IRP **IoStartPacket**将 IRP 插入到的设备对象与关联的设备队列。 该驱动程序可以根据需要提供*键*作为参数的值**IoStartPacket** ，设置上 Irp 设备队列中的驱动程序确定顺序。

如果该驱动程序不是正忙并且设备队列为空，I/O 管理器会立即调用其*StartIo*例程，传递 IRP 的输入。

对于大容量存储设备，最低级别驱动程序不需要提供[*取消*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_cancel)例程时，它调用**IoStartPacket**以下两个原因：

1.  文件系统通常上层这样的驱动程序处理文件 I/O 请求取消的操作。

2.  大容量存储设备驱动程序快速地处理 Irp。

通常情况下，链中的分层驱动程序的最高级别的驱动程序处理 Irp 的取消操作。

### <a name="calling-allocateadapterchannel-and-maptransfer"></a>调用 AllocateAdapterChannel 和 MapTransfer

假设*StartIo*例程，图中所示说明如何通过最低级别驱动程序例程的 IRP 途径，传输请求可以通过单个 DMA 操作，来确定*StartIo*例程调用[ **AllocateAdapterChannel** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pallocate_adapter_channel)驱动程序的入口点*AdapterControl*例程和 IRP。

当系统 DMA 控制器不可用时，I/O 管理器调用的驱动程序*AdapterControl*例程，以设置在传输操作。 *AdapterControl*例程调用[ **MapTransfer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pmap_transfer)若要设置系统 DMA 控制器。 然后，驱动程序程序 DMA 操作其设备，并返回。 (有关使用 DMA 和适配器对象的详细信息，请参阅[输入/输出技术](i-o-programming-techniques.md)。)

### <a name="calling-iorequestdpc-from-the-drivers-isr"></a>从驱动程序的调用 IoRequestDpc ISR

驱动程序的 ISR 时来指示其传输操作已完成，设备中断，使设备生成中断和调用停止[ **IoRequestDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iorequestdpc)，图说明中所示完成最低级别驱动程序例程的 IRP 路径。

此调用进行排队的驱动程序*DpcForIsr*例程，以尽可能多地在较低的硬件优先级 (IRQL) 在传输操作完成。

### <a name="calling-iostartnextpacket-and-iocompleterequest"></a>调用 IoStartNextPacket 和 IoCompleteRequest

当*DpcForIsr*例程处理传输完时，它调用[ **IoStartNextPacket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iostartnextpacket)及时，使驱动程序的*StartIo*例程将调用与设备队列中下一步的 IRP，如果任何排队。 *DpcForIsr*例程还将刚完成 IRP I/O 状态块，然后调用[ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest) IRP 的。

下图说明了此驱动程序调用**IoStartNextPacket**并**IoCompleteRequest**。

![调用 iostartnextpacket 和 iocompleterequest](images/4snxtpak.png)

驱动程序应调用**IoStartNextPacket**或[ **IoStartNextPacketByKey** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iostartnextpacketbykey)开始下一个请求的 I/O 操作越早越好，最好是它们调用之前**IoCompleteRequest**。

如果该设备，排队任何 Irp **IoStartNextPacket**调用[ **KeRemoveDeviceQueue** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keremovedevicequeue)若要从队列中删除下一步 IRP。 然后，I/O 管理器调用的驱动程序*StartIo*例程，将取消排队的 IRP 传递。 如果没有 Irp 设备队列中当前都是**IoStartNextPacket**只是返回给调用方。

### <a href="" id="ddk-setting-the-i-o-status-block-in-an-irp-kg"></a>在 IRP 中设置 I/O 状态块

每个最低级别驱动程序必须设置 IRP [I/O 状态块](i-o-status-blocks.md)之前，调用[ **IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)。 （在上图中，第二个阴影的区域表示状态块。）I/O 状态块提供了更高级别的驱动程序，则从根本上讲，对原始请求方的 I/O 操作的信息。 上图中的驱动程序的上面任何更高级别的驱动程序可能已设置了[ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)例程，用于读取 I/O 状态块由该驱动程序设置。 更高级别的驱动程序通常不修改 IRP 的设备驱动程序已完成，除非较高级别的驱动程序正在重试 IRP，在这种情况下它会重新初始化的 I/O 状态块中的 I/O 状态块。

在之前调用该 IRP 中块的每个更高级别的驱动程序，它还将其发送到下一个较低的驱动程序必须设置 I/O 状态的情况下完成 IRP **IoCompleteRequest**。 较高的整体 I/O 吞吐量，对于更高级别的驱动程序应检查其自己的每个 IRP 的 I/O 堆栈位置中的参数，和如果参数无效，应设置 I/O 状态块完成请求本身。 只要有可能，驱动程序应避免在链中传递到较低的驱动程序无效的请求。

假设在上图中在传输操作成功， *DpcForIsr*例程，图中所示说明如何完成最低级别驱动程序例程的 IRP 路径，设置状态\_成功**状态**和所传输的字节数**信息**IRP 的 I/O 状态块。

许多标准驱动程序例程还返回 NTSTATUS 类型值。 有关 NTSTATUS 常量，如状态详细信息\_成功，请参阅[日志记录错误](logging-errors.md)。

 

 





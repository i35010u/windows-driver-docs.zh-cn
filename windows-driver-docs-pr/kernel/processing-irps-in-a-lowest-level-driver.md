---
title: 在最低级驱动程序中处理 IRP
description: 在最低级驱动程序中处理 IRP
ms.assetid: 9b8c2586-d47b-49ab-bf65-a298af36304c
keywords:
- Irp WDK 内核，处理示例
- Irp WDK 内核，i/o 状态块
- I/o 状态阻止 WDK 内核
- 状态阻止 WDK 内核
- IoStartNextPacket
- IoCompleteRequest
- IoRequestDpc
- AllocateAdapterChannel
- MapTransfer
- IoStartPacket
- 也
- IoGetCurrentIrpStackLocation
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 26448d746e4e6e729f5cd254a0c3a612fbcdf4f0
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79242948"
---
# <a name="processing-irps-in-a-lowest-level-driver"></a>在最低级驱动程序中处理 IRP





最低级别的物理驱动程序具有特定的标准例程，这是较高级别的驱动程序不需要。 最低级别驱动程序的标准例程集也会根据以下条件而有所不同：

-   设备每个驱动程序控件的性质

-   驱动程序是否为直接或缓冲 i/o 设置其设备对象

-   单个驱动程序的设计

为了说明标准驱动程序例程的角色，下图显示了一个示例 IRP 在由最低级别的大容量存储设备驱动程序处理时可能采用的路径。 该图中的驱动程序具有以下特征：

-   设备在每次 i/o 操作结束时生成中断，因此此驱动程序具有 ISR 和[*DpcForIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)例程。

-   该驱动程序具有[*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)例程，而不是为 irp 设置内部队列并管理其自己的队列。

-   驱动程序使用系统 DMA，因此它将其设备对象的**标志**设置为直接 i/o，并具有[*AdapterControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_control)例程。

![通过最低级别的驱动程序例程说明 irp 路径的示意图](images/4loddirp.png)

如图所示，i/o 管理器会创建一个 IRP，并将其发送到给定主要函数代码的驱动程序调度例程。 假设函数代码为[**IRP\_mj\_READ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)或[**IRP\_mj\_WRITE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)，则调度例程为**DDDispatchReadWrite**。

### <a name="calling-iogetcurrentirpstacklocation"></a>调用 IoGetCurrentIrpStackLocation

需要 IRP 参数的任何驱动程序例程都必须调用[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)以获取驱动程序的[i/o 堆栈位置](i-o-stack-locations.md)。 此类例程包含处理多个主要 i/o 函数代码（<strong>IRP\_MJ\_* XXX</strong>）的调度例程<em>，处理一个函数，该函数支持次要函数（</em><em>IRP\_MN\_</em>XXX<strong><em>），或处理设备 I/O 控制请求（[</em>* IRP\_mj\_设备\_控制</strong>](<https://msdn.microsoft.com/library/windows/hardware/ff550744>)和/或 IRP\_[**内部\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)），以及处理 IRP 的每个其他驱动程序例程。\_

此驱动程序的 i/o 堆栈位置是最低的，其中数量不确定的高级驱动程序的 i/o 堆栈位置显示为灰色。 为简单起见，上图中未显示对[*DispatchReadWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)、 *StartIo*、 *AdapterControl*和[*DpcForIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)例程的**IoGetCurrentIrpStackLocation**的调用。

### <a name="calling-iomarkirppending-and-iostartpacket"></a>调用也和 IoStartPacket

示例驱动程序不会在其调度例程中完成 IRP，而是在其*StartIo*例程中处理 irp。 在执行此操作之前，调度例程会调用[**也**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)来指示 IRP 尚未完成。 然后，它会调用[**IoStartPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartpacket)以将 IRP 排队以供驱动程序的*StartIo*例程进一步处理。 调度例程还会返回\_挂起的 NTSTATUS 值状态。

下图说明了对**IoStartPacket**的调用。

![演示对 iostartpacket 的调用的关系图](images/4strtpak.png)

如果驱动程序正忙于处理设备上的其他 IRP， **IoStartPacket**会将 IRP 插入与设备对象相关联的设备队列中。 驱动程序可以选择将*键值*作为参数提供给**IoStartPacket** ，以便在设备队列中对 irp 施加驱动程序确定的顺序。

如果驱动程序不忙并且设备队列为空，则 i/o 管理器会立即调用其*StartIo*例程，同时传递输入 IRP。

对于大容量存储设备，最低级别的驱动程序在调用**IoStartPacket**时无需提供[*取消*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel)例程，原因有两个：

1.  在此类驱动程序上分层的文件系统通常会处理文件 i/o 请求的取消。

2.  大容量存储设备驱动程序快速处理 Irp。

通常，分层驱动程序链中的最上层驱动程序处理 Irp 的取消。

### <a name="calling-allocateadapterchannel-and-maptransfer"></a>调用 AllocateAdapterChannel 和 MapTransfer

假设*StartIo*例程（如图所示，通过最低级别的驱动程序例程说明 IRP 路径）可以通过单个 DMA 操作来确定传输请求，则*StartIo*例程将使用驱动程序的*AdapterControl*例程和 IRP 的入口点调用[**AllocateAdapterChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_adapter_channel) 。

当系统 DMA 控制器可用时，i/o 管理器会调用驱动程序的*AdapterControl*例程来设置传输操作。 *AdapterControl*例程调用[**MapTransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pmap_transfer)来设置系统 DMA 控制器。 然后，驱动程序将其设备用于 DMA 操作并返回。 （有关使用 DMA 和适配器对象的详细信息，请参阅[输入/输出技术](i-o-programming-techniques.md)。）

### <a name="calling-iorequestdpc-from-the-drivers-isr"></a>从驱动程序的 ISR 调用 IoRequestDpc

当设备中断指示其传输操作完成时，驱动程序的 ISR 会阻止设备生成中断并调用[**IoRequestDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iorequestdpc)，如通过最低级别的驱动程序例程说明 IRP 路径中所示。

此调用会将驱动程序的*DpcForIsr*例程排队，以更低的硬件优先级（IRQL）完成尽可能多的传输操作。

### <a name="calling-iostartnextpacket-and-iocompleterequest"></a>调用 IoStartNextPacket 和 IoCompleteRequest

*DpcForIsr*例程处理完传输后，会立即调用[**IoStartNextPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartnextpacket) ，以便在设备队列中的下一个 IRP （如果有）被排队时调用驱动程序的*StartIo*例程。 *DpcForIsr*例程还设置刚完成的 irp 的 i/o 状态块，并为 IRP 调用[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) 。

下图说明了此驱动程序对**IoStartNextPacket**和**IoCompleteRequest**的调用。

![调用 iostartnextpacket 和 iocompleterequest](images/4snxtpak.png)

驱动程序应尽可能早地调用**IoStartNextPacket**或[**IoStartNextPacketByKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartnextpacketbykey)来开始下一个请求的 i/o 操作，最好是在调用**IoCompleteRequest**之前进行。

如果为设备排队的任何 Irp， **IoStartNextPacket**会调用[**KeRemoveDeviceQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keremovedevicequeue) ，以从队列中删除下一个 IRP。 然后，i/o 管理器调用驱动程序的*StartIo*例程，同时传递取消排队的 IRP。 如果设备队列中当前没有任何 Irp， **IoStartNextPacket**只会返回到调用方。

### <a href="" id="ddk-setting-the-i-o-status-block-in-an-irp-kg"></a>设置 IRP 中的 i/o 状态块

在调用[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)之前，每个最低级别的驱动程序必须设置 IRP 的[i/o 状态块](i-o-status-blocks.md)。 （在上图中，第二个灰色区域表示状态块。）I/o 状态块向更高级的驱动程序提供信息，最终将其提供给 i/o 操作的原始请求者。 上图中的驱动程序上面的任何较高级别的驱动程序都可能设置了一个[*IoCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程，该例程读取此驱动程序设置的 i/o 状态块。 较高级别的驱动程序通常不会修改由设备驱动程序完成的 IRP 中的 i/o 状态块，除非较高级别的驱动程序正在重试 IRP，在这种情况下，它将重新初始化 i/o 状态块。

完成 IRP 但不将其发送到下一个较低版本的驱动程序的每个更高级别的驱动程序还必须在调用**IoCompleteRequest**之前设置该 irp 中的 i/o 状态块。 为了获得良好的总 i/o 吞吐量，更高级别的驱动程序应检查每个 IRP 各自的 i/o 堆栈位置中的参数，如果这些参数无效，则应设置 i/o 状态块并完成请求本身。 如果可能，驱动程序应避免将无效请求传递到链中较低的驱动程序。

假设上图中的传输操作成功， *DpcForIsr*例程（如图中所示）通过最低级别的驱动程序例程来说明 IRP 路径，将\_状态设置为 "**状态**" "成功" 和 "已在 IRP 的 I/o 状态块的**信息**中传输的字节数"。

许多标准驱动程序例程还会返回 NTSTATUS 类型值。 有关 NTSTATUS 常量（如状态\_成功）的详细信息，请参阅[日志记录错误](logging-errors.md)。

 

 





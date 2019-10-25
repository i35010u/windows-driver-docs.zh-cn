---
title: 为基于数据包的 DMA 分配适配器通道
description: 为基于数据包的 DMA 分配适配器通道
ms.assetid: c95e4b2d-ce19-453a-bcc5-4bb37fc5d9ed
keywords:
- 系统 DMA WDK 内核，基于数据包
- 基于数据包的 DMA WDK 内核
- DMA 传输 WDK 内核，基于数据包
- 分配适配器通道
- 适配器通道分配 WDK 内核
- AllocateAdapterChannel
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c18215fa31c5d7add7f583bff6dfb8056c09b75
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837232"
---
# <a name="allocating-an-adapter-channel-for-packet-based-dma"></a>为基于数据包的 DMA 分配适配器通道





若要准备基于数据包的系统 DMA，驱动程序将在收到[**IRP\_mj\_READ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)或[**IRP\_mj\_写入**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)请求后调用[**KeFlushIoBuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keflushiobuffers)和[**AllocateAdapterChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_adapter_channel) 。

在驱动程序调用这些例程之前，它的[*DispatchRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)或[*DispatchWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程（或处理 DMA 传输的任何其他调度例程）应该已经检查了 IRP 的参数的有效性。 调度例程还可能已将 IRP 排入队列，以便进行进一步处理。

调用**AllocateAdapterChannel**的驱动程序例程必须以 IRQL = 调度\_级别执行。 除了[**IoGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdmaadapter)返回的适配器对象的指针，驱动程序在调用**AllocateAdapterChannel**时必须提供以下内容：

-   指向目标设备对象的指针

-   其[*AdapterControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_control)例程的入口点

-   指向*AdapterControl*例程将使用的任何驱动程序确定的上下文信息的指针

**AllocateAdapterChannel**对驱动程序的*AdapterControl*例程进行排队，当系统 DMA 控制器分配到此驱动程序并为驱动程序的 DMA 操作分配了一组[映射寄存器](map-registers.md)时，将运行该例程。

进入时， *AdapterControl*例程会接收到对**AllocateAdapterChannel**的调用中传递的*DeviceObject*和*上下文*指针，以及分配的映射寄存器的句柄（*MapRegisterBase*）。

如果驱动程序有[*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)例程， *AdapterControl*例程还会收到指向**DeviceObject&gt;CurrentIrp**的指针。 如果驱动程序管理自己的 Irp 队列（而不是使用*StartIo*例程），驱动程序应在调用**AllocateAdapterChannel**时，将指向当前 IRP 的指针包括在它通过的上下文中。

*AdapterControl*例程通常执行以下操作：

1.  保存或初始化驱动程序维护的任何有关 DMA 操作的上下文。 上下文可能包括*MapRegisterBase*的输入，驱动程序必须将该句柄传递给[**MapTransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pmap_transfer)和[**FlushAdapterBuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pflush_adapter_buffers) ，还可能包括从 IRP 中的 I/o 堆栈位置请求的传输**长度**。

2.  调用[**MmGetMdlVirtualAddress**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)后跟**MapTransfer**。 请参阅[为基于数据包的 Dma 设置系统 Dma 控制器](setting-up-the-system-dma-controller-for-packet-based-dma.md)。

3.  设置从属设备以启动传输操作。

4.  返回值**KeepObject**。

每个*AdapterControl*例程必须返回类型为 IO\_的系统定义值[ **\_操作**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_io_allocation_action)。 对于使用系统 DMA 的驱动程序， *AdapterControl*例程必须返回值**KeepObject**。 这允许驱动程序保留系统 DMA 控制器的 "所有权" 和分配的映射寄存器，直到它传输了所有请求的数据。

由于*AdapterControl*例程无法等待从属设备执行 DMA 操作，因此每个*AdapterControl*例程至少必须执行以下操作：

1.  保存上下文信息，尤其是驱动程序的设备扩展中的*MapRegisterBase*句柄、控制器扩展或驱动程序可访问的其他常驻存储区域（驱动程序分配的非分页池）。

2.  返回**KeepObject**。

有关其他信息，请参阅[编写 AdapterControl 例程](writing-adaptercontrol-routines.md)。

每个 DMA 传输操作完成后，另一个驱动程序例程（可能是[*DpcForIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)例程）必须调用[**FlushAdapterBuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pflush_adapter_buffers) 。 如果有必要多次设置 DMA 控制器以满足当前 IRP 的传输请求，则此例程还必须再次调用**MapTransfer**和**FlushAdapterBuffers** 。

当驱动程序已满足当前 IRP 的请求时，它必须调用[**FreeAdapterChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_adapter_channel)。 对于当前 IRP，应立即调用**FlushAdapterBuffers**的此支持例程，使系统 DMA 控制器可供使用（由任何驱动程序使用），以满足其他传输请求迅速。

具有散点/集合功能的从属设备的驱动程序还应从其*AdapterControl*例程返回**KeepObject** 。 当驱动程序必须拆分给定 DMA 请求时，设备必须能够等待，同时系统 DMA 控制器 reprogrammed DMA 操作。 在某些 Windows 平台上，此类设备每个 DMA 操作最多可以传输一页数据，因为 HAL 只能向该设备的驱动程序分配一个映射寄存器。

 

 





---
title: 分配总线主控适配器对象
description: 分配总线主控适配器对象
ms.assetid: fc80d3f8-a12e-40bd-8b0e-c6bca2f9e7de
keywords:
- 分配总线主适配器对象
- 总线主控 DMA WDK 内核
- DMA 传输 WDK 内核，总线主机 DMA
- 适配器对象 WDK 内核，主线-主 DMA
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c92f50692838d1e31328d171bda5b21e3b667927
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192035"
---
# <a name="allocating-the-bus-master-adapter-object"></a>分配总线主控适配器对象





为准备基于数据包的总线主机 DMA，驱动程序将在收到[**IRP \_ mj \_ READ**](./irp-mj-read.md)或[**Irp \_ Mj \_ 写入**](./irp-mj-write.md)后调用[**KeFlushIoBuffers**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keflushiobuffers)和[**AllocateAdapterChannel**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_adapter_channel) 。 驱动程序调用这些例程之前，其调度例程应检查 IRP 参数的有效性。 它还可能会将 IRP 排队给另一驱动程序例程，以便进一步处理。 传输请求是当前 IRP，需要设备 i/o 操作。

调用 **AllocateAdapterChannel** 的驱动程序例程必须以 IRQL = 调度级别执行 \_ 。 除了 [**IoGetDmaAdapter**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdmaadapter)返回的适配器对象的指针，驱动程序在调用 **AllocateAdapterChannel**时必须提供以下内容：

-   指向当前 IRP 的目标设备对象的指针

-   其 [*AdapterControl*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_control) 例程的入口点

-   指向 *AdapterControl* 例程将使用的任何驱动程序确定的上下文信息的指针

**AllocateAdapterChannel** 对驱动程序的 *AdapterControl* 例程进行排队，在适配器对象处于免费的情况下运行，并为驱动程序的 DMA 操作分配了一组 [映射寄存器](map-registers.md) ，以供目标设备或目标设备使用。

进入时，将*为 AdapterControl*例程提供在调用**AllocateAdapterChannel**时传递的*DeviceObject*和*上下文*指针，以及分配的映射寄存器 (*MapRegisterBase*) 的句柄。

如果驱动程序有[*StartIo*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)例程，则还会向*AdapterControl*例程提供一个指向**DeviceObject- &gt; CurrentIrp**的指针。 如果驱动程序管理自己的 Irp 队列，而不是使用 *StartIo* 例程，则驱动程序应在调用 **AllocateAdapterChannel**时，在它传递的上下文中包含指向当前 IRP 的指针。

对于不带散播/收集功能的总线主控 DMA 设备的驱动程序， *AdapterControl* 例程通常执行以下操作：

1.  保存或初始化驱动程序维护的任何有关 DMA 操作的上下文。 上下文可能包括 MapRegisterBase 的输入*MapRegisterBase*句柄，驱动程序必须将该句柄传递到[**MapTransfer**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pmap_transfer)和[**FlushAdapterBuffers**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pflush_adapter_buffers)、从 IRP 中的 i/o 堆栈位置请求的**传输的字节**数（以字节为单位）等。

2.  调用[**MmGetMdlVirtualAddress**](./mm-bad-pointer.md) ，后跟[设置传输操作](setting-up-a-transfer-operation.md)中所述的**MapTransfer** (，接下来) 获取其设备可用于启动传输操作的逻辑地址。

3.  设置总线主适配器以启动传输操作。

4.  返回值 **DeallocateObjectKeepRegisters**。

对于具有散点/集合功能的总线主机设备的驱动程序， *AdapterControl* 例程通常会执行以下操作：

1.  保存或初始化驱动程序维护的有关 DMA 操作的任何状态，如保存驱动程序必须传递到**MapTransfer**和**FlushAdapterBuffers**的*MAPREGISTERBASE*句柄，从 IRP 中的 i/o 堆栈位置到所请求的**传输的字节**数（以字节为单位）等。

2.  调用 **MmGetMdlVirtualAddress** 后跟下一) 小节中描述的 **MapTransfer** (，以获取其设备可用于启动传输操作的逻辑地址。

    *AdapterControl*例程将重复调用 MapTransfer，直到它使用了所有可用的映射寄存器来生成用于总线主适配器的分散/收集列表。

3.  设置总线主适配器以启动传输操作。

4.  返回值 **DeallocateObjectKeepRegisters**。

有关其他信息，请参阅 [编写 AdapterControl 例程](writing-adaptercontrol-routines.md)。

请注意，执行总线主机 DMA 的驱动程序可以使用 [**GetScatterGatherList**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pget_scatter_gather_list) 和 [**PutScatterGatherList**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pput_scatter_gather_list) 例程，而不考虑其设备是否支持散播/聚集 dma。 使用这些例程将更改驱动程序的 *AdapterControl* 例程的要求;有关详细信息，请参阅 [使用散点/集合 DMA](using-scatter-gather-dma.md) 。

*AdapterControl*例程必须返回类型为 IO 分配操作的系统定义值 \_ \_ 。 对于使用 bus 主机 DMA 的驱动程序， *AdapterControl* 例程通常应返回值 **DeallocateObjectKeepRegisters**，这允许驱动程序保留目标设备对象的分配的映射寄存器，直到它为当前 IRP 传输所有请求的数据。 传输完成后，DPC 例程应调用 [**FreeMapRegisters**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_map_registers) 来释放已分配的映射寄存器。 但在设备不支持命令队列的情况下， *AdapterControl* 例程可以在当前 IRP 的传输完成时返回 **KEEPOBJECT** ，而 DPC 例程可以调用 [**FreeAdapterChannel**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_adapter_channel) 。

*AdapterControl*例程无法等待主线主机适配器完成 DMA 操作。

无论总线主适配器是否支持散点/集合， *AdapterControl* 例程至少必须执行以下操作：

1.  在驱动程序的设备扩展、控制器扩展或驱动程序可访问的其他可访问的常驻存储区域中保存必要的上下文信息（特别是 *MapRegisterBase* 句柄） (非分页池) 。 当驱动程序调用 **MapTransfer** 和 **FlushAdapterBuffers**时，必须传递此句柄。

2.  返回 **DeallocateObjectKeepRegisters**。

另一个驱动程序例程 (可能是 [*DpcForIsr*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine) 例程) 必须在每个 DMA 传输操作完成时调用 **FlushAdapterBuffers** 。 此例程还必须设置满足当前 IRP 所需的任何其他 DMA 操作。

当驱动程序已满足当前 IRP 的传输请求或由于设备或总线 i/o 错误而导致 IRP 失败时，它必须调用 **FreeMapRegisters**。 对于当前 IRP，应立即对 **FlushAdapterBuffers** 执行此调用，以便驱动程序可以为其他 DMA 请求提供服务，这可能是针对总线上的其他设备。

 


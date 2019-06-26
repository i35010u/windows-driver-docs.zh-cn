---
title: 分配总线主控适配器对象
description: 分配总线主控适配器对象
ms.assetid: fc80d3f8-a12e-40bd-8b0e-c6bca2f9e7de
keywords:
- 分配了主机总线适配器对象
- 主总线 DMA WDK 内核
- DMA 传输 WDK 内核，总线 master DMA
- 适配器对象 WDK 内核，总线 master DMA
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 667f1567ac1f8f271c0af2204f780d75a6c94f82
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369969"
---
# <a name="allocating-the-bus-master-adapter-object"></a>分配总线主控适配器对象





若要准备基于数据包的、 总线 master DMA 驱动程序调用[ **KeFlushIoBuffers** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keflushiobuffers)并[ **AllocateAdapterChannel** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pallocate_adapter_channel)后接收[ **IRP\_MJ\_读取**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)或者[ **IRP\_MJ\_编写**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write). 该驱动程序调用这些例程之前，其调度例程应检查的 IRP 的参数的有效性。 它还可能会排队到另一个驱动程序例程进行进一步处理 IRP。 转移请求是当前 IRP 要求设备 I/O 操作。

调用的驱动程序例程**AllocateAdapterChannel**必须执行在 IRQL = 调度\_级别。 以及指向返回的适配器对象的指针[ **IoGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdmaadapter)，它将调用时，驱动程序必须提供以下**AllocateAdapterChannel**:

-   指向当前 IRP 的目标设备对象的指针

-   入口点及其[ *AdapterControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_control)例程

-   指向任何驱动程序确定上下文信息的指针*AdapterControl*例程将使用

**AllocateAdapterChannel**队列的驱动程序*AdapterControl*例程，运行时是免费的适配器对象和一系列[映射寄存器](map-registers.md)已分配的驱动程序的 DMA操作从目标设备。

在进入时， *AdapterControl*给定例程*DeviceObject*并*上下文*指针传递到调用中**AllocateAdapterChannel**，以及一个句柄 (*MapRegisterBase*) 的分配的映射注册。

*AdapterControl*例程还提供一个指向**DeviceObject-&gt;CurrentIrp**如果该驱动程序有[ *StartIo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)例程。 如果该驱动程序管理的 Irp 自己队列，而不让*StartIo*例程，该驱动程序应包括指向当前 IRP 的指针调用时传递的上下文的一部分**AllocateAdapterChannel**.

主总线 DMA 设备没有散播-聚集功能的驱动程序*AdapterControl*例程通常执行以下操作：

1.  将保存或初始化该驱动程序会维护有关 DMA 操作任何上下文。 上下文可能包括输入*MapRegisterBase*句柄驱动程序必须将传递给[ **MapTransfer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pmap_transfer)并[ **FlushAdapterBuffers** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pflush_adapter_buffers)，则**长度**以字节为单位的来自其 I/O 请求的传输堆栈 IRP 中的位置等。

2.  调用[ **MmGetMdlVirtualAddress** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)跟**MapTransfer** (中所述[传输启动操作设置](setting-up-a-transfer-operation.md)、 下一步) 以获取其设备可用于启动在传输操作的逻辑地址。

3.  将主机总线适配器设置开始在传输操作。

4.  返回的值**DeallocateObjectKeepRegisters**。

散播-聚集功能的主总线设备驱动程序*AdapterControl*例程通常执行以下操作：

1.  保存或初始化任何状态驱动程序保持 DMA 操作，如保存有关*MapRegisterBase*句柄驱动程序必须将传递给**MapTransfer**和**FlushAdapterBuffers**，则**长度**以字节为单位的来自其 I/O 请求的传输堆栈 IRP 中的位置等。

2.  调用**MmGetMdlVirtualAddress**跟**MapTransfer** （下一小节中所述） 若要获取其设备的逻辑地址可用于启动在传输操作。

    *AdapterControl*例程调用 MapTransfer 重复直到它已使用所有可用的映射注册来生成主机总线适配器的分散/集中列表。

3.  将主机总线适配器设置开始在传输操作。

4.  返回的值**DeallocateObjectKeepRegisters**。

有关其他信息，请参阅[写入 AdapterControl 例程](writing-adaptercontrol-routines.md)。

请注意，可以使用驱动程序的执行主总线 DMA [ **GetScatterGatherList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pget_scatter_gather_list)并[ **PutScatterGatherList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pput_scatter_gather_list)例程而不考虑他们的设备是否支持散播-聚集 DMA。 使用这些例程可更改的驱动程序的要求*AdapterControl*例程，请参见[使用散播-聚集 DMA](using-scatter-gather-dma.md)有关详细信息。

*AdapterControl*例程必须返回类型 IO 的系统定义的值\_分配\_操作。 驱动程序使用总线 master DMA *AdapterControl*例程通常的返回值应**DeallocateObjectKeepRegisters**，这将允许驱动程序保留分配的映射注册目标设备对象直到其已经为当前的 IRP 传输所有请求的数据。 传输完成后，应调用 DPC 例程[ **FreeMapRegisters** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pfree_map_registers)来释放分配的映射注册。 在其中的设备不支持命令排队，但是的情况下*AdapterControl*例程可以返回**KeepObject**时当前 IRP 的传输已完成，并且可以调用 DPC 例程[ **FreeAdapterChannel** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pfree_adapter_channel)相反。

*AdapterControl*例程不能等待主机总线适配器来完成 DMA 操作。

无论主机总线适配器是否支持散播-聚集*AdapterControl*例程至少必须执行以下操作：

1.  保存必要的上下文信息 — 尤其是*MapRegisterBase*处理-驱动程序的设备扩展、 控制器扩展或其他驱动程序可访问驻留的存储区域 （非分页池，分配由驱动程序） 中。 调用时，该驱动程序必须通过此句柄**MapTransfer**并**FlushAdapterBuffers**。

2.  返回**DeallocateObjectKeepRegisters**。

另一个驱动程序例程 (可能[ *DpcForIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_dpc_routine)例程) 必须调用**FlushAdapterBuffers** DMA 传输的每个操作完成时。 此例程还必须设置的任何其他 DMA 操作需满足当前 IRP。

当驱动程序已满足当前 IRP 的传输请求，或者必须失败由于设备或总线 I/O 错误 IRP 时，它必须调用**FreeMapRegisters**。 此调用应发生到的最后一个调用后立即**FlushAdapterBuffers**为当前的 IRP，以便该驱动程序可以提供服务的其他 DMA 请求，可能是在总线上的其他设备。

 

 





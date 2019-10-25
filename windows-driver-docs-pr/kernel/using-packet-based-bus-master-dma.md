---
title: 使用基于数据包的总线主控 DMA
description: 使用基于数据包的总线主控 DMA
ms.assetid: 57b37103-8ae0-4c54-b613-55b1a629d9ae
keywords:
- 总线主控 DMA WDK 内核
- DMA 传输 WDK 内核，总线主机 DMA
- 适配器对象 WDK 内核，主线-主 DMA
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 58b34c66c4dd1d7e744d56750899f95b67b24422
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835942"
---
# <a name="using-packet-based-bus-master-dma"></a>使用基于数据包的总线主控 DMA





若要使用基于数据包的 DMA，总线主机 DMA 设备的驱动程序会在处理请求 DMA 传输的 IRP 时调用以下一般的支持例程顺序：

-   [**KeFlushIoBuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keflushiobuffers)即将尝试为传输请求分配映射寄存器（有关详细信息，请参阅[维护缓存一致性](maintaining-cache-coherency.md)）

-   当驱动程序准备好对用于 DMA 的主线主机适配器进行编程时， [**AllocateAdapterChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_adapter_channel)

-   [**MmGetMdlVirtualAddress**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)获取 MDL 的索引，作为[**MapTransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pmap_transfer)的初始参数需要，使用**MapTransfer**来使系统物理内存支持 IRP 的缓冲区设备-可访问

    请注意，任何驱动程序都可能需要执行多个传输操作才能满足当前 IRP，如[拆分传输请求](splitting-dma-transfer-requests.md)中所述。 不具有散点/集合功能的设备的驱动程序可以每次传输操作调用**MapTransfer**一次。 具有散点/集合功能的设备驱动程序可以多次调用**MapTransfer** ，以设置每个传输操作。 此外，这些驱动程序还可以使用系统内置的散播/聚集支持，如[使用散点/集合 DMA](using-scatter-gather-dma.md)中所述。

-   在每个 DMA 传输操作结束时[**FlushAdapterBuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pflush_adapter_buffers)目标设备，以确定是否已完全传输所有请求的数据

-   当当前 IRP 的所有 DMA 操作都已完成时[**FreeMapRegisters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_map_registers) ，因为所有请求的数据都已完全传输，或者因为设备或总线 i/o 错误，驱动程序必须失败 IRP

[**IoGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdmaadapter)返回的适配器对象指针是**AllocateAdapterChannel**、 **MapTransfer**、 **FlushAdapterBuffers**和**FreeMapRegisters**的必需参数。 请注意，在 Windows 2000 之前的 Windows NT 版本中，总线主机设备可将**NULL**适配器对象指针传递到**MapTransfer**和**FlushAdapterBuffers**。 在 Windows 2000 和更高版本中，驱动程序将无法再执行此操作。

**KeFlushIoBuffers**和**MmGetMdlVirtualAddress**需要指向**IRP&gt;MdlAddress**上的 MDL 的指针。

各个驱动程序会在不同的点调用此支持例程序列，这取决于每个驱动程序的实现方式，以便为其设备提供服务。 例如，一个驱动程序的[*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)例程可能会调用**AllocateAdapterChannel**，而另一个驱动程序可能会从从驱动程序创建的联锁队列或设备队列中删除 irp 的例程进行此调用。

不管使用此部分中所述的例程，使用基于数据包的 DMA 的任何驱动程序都可以使用支持例程来简化散播/聚集 DMA，而不管其设备是否有内置的散播/聚集支持。 有关详细信息，请参阅[使用散点/集合 DMA](using-scatter-gather-dma.md) 。

 

 





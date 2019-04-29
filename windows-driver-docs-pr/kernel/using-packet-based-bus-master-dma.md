---
title: 使用基于数据包的总线主控 DMA
description: 使用基于数据包的总线主控 DMA
ms.assetid: 57b37103-8ae0-4c54-b613-55b1a629d9ae
keywords:
- 主总线 DMA WDK 内核
- DMA 传输 WDK 内核，总线 master DMA
- 适配器对象 WDK 内核，总线 master DMA
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d20d035bc5982c60f3abdc9b9bc5f900efdedb0a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391073"
---
# <a name="using-packet-based-bus-master-dma"></a>使用基于数据包的总线主控 DMA





若要使用基于数据包的 DMA，总线 master DMA 设备的驱动程序调用处理 IRP 请求 DMA 传输支持例程的以下一般规则：

-   [**KeFlushIoBuffers** ](https://msdn.microsoft.com/library/windows/hardware/ff552041)之前尝试传输请求的分配映射寄存器 (有关详细信息，请参阅[维护缓存一致性](maintaining-cache-coherency.md))

-   [**AllocateAdapterChannel** ](https://msdn.microsoft.com/library/windows/hardware/ff540573)何时可以进行编程的 DMA 主机总线适配器驱动程序

-   [**MmGetMdlVirtualAddress** ](https://msdn.microsoft.com/library/windows/hardware/ff554539)进入 MDL，所需的初始参数作为索引[ **MapTransfer**](https://msdn.microsoft.com/library/windows/hardware/ff554402)，以及**MapTransfer**到将备份设备可访问的 IRP 的缓冲区的系统物理内存

    请注意，任何驱动程序可能需要执行多个传输的操作以满足当前的 IRP，如中所述[拆分传输请求](splitting-dma-transfer-requests.md)。 功能可以调用不了的设备驱动程序散播-聚集**MapTransfer**一次每个传输操作。 功能可以调用具有的设备驱动程序散播-聚集**MapTransfer**不止一次设置每个传输操作。 此外，这些驱动程序可以使用系统的内置散播-聚集支持中, 所述[使用散播-聚集 DMA](using-scatter-gather-dma.md)。

-   [**FlushAdapterBuffers** ](https://msdn.microsoft.com/library/windows/hardware/ff545917)向/从目标设备，以便确定所有请求的数据是否已完全传输每个 DMA 传输操作结束时

-   [**FreeMapRegisters** ](https://msdn.microsoft.com/library/windows/hardware/ff546513)只要完成所有当前 IRP DMA 操作，因为所有请求的数据已经全部传输，或者因为驱动程序必须失败，因为设备 IRP 或总线 I/O 错误

所返回的适配器对象指针[ **IoGetDmaAdapter** ](https://msdn.microsoft.com/library/windows/hardware/ff549220)为必需参数**AllocateAdapterChannel**， **MapTransfer****FlushAdapterBuffers**，并**FreeMapRegisters**。 请注意在 Windows 2000 之前的 Windows NT 版本，可以传递总线母版设备**NULL**适配器对象指针，指向**MapTransfer**并**FlushAdapterBuffers**。 在 Windows 2000 和更高版本，驱动程序可以不再会执行此操作。

**KeFlushIoBuffers**并**MmGetMdlVirtualAddress**需要指向在 MDL **Irp-&gt;MdlAddress**。

单独的驱动程序在不同时间点，具体取决于每个驱动程序的实现来服务其设备的方式调用这一序列的支持例程。 例如，一个驱动程序的[ *StartIo* ](https://msdn.microsoft.com/library/windows/hardware/ff563858)例程可能会使对调用**AllocateAdapterChannel**，而另一个驱动程序可能会进行此调用，从删除的例程从驱动程序创建互锁的队列或设备的队列的 Irp。

而不是使用例程所述在本部分中，使用基于数据包的 DMA 可以使用旨在简化支持例程散播-聚集 DMA，无论其设备是否有内置的分散/集中支持的任何驱动程序。 请参阅[使用散播-聚集 DMA](using-scatter-gather-dma.md)有关详细信息。

 

 





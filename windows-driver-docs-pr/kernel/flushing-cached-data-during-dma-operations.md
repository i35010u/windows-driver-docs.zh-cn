---
title: 执行 DMA 操作期间刷新缓存数据
description: 执行 DMA 操作期间刷新缓存数据
ms.assetid: 1b984b47-82cc-46b9-acad-73c5ed63e246
keywords:
- DMA 传输 WDK 内核，数据完整性
- KeFlushIoBuffers
- FlushAdapterBuffers
- 刷新缓存的数据
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca5160347d97edd817c43e2df691acf9491420d1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359981"
---
# <a name="flushing-cached-data-during-dma-operations"></a>执行 DMA 操作期间刷新缓存数据





在某些平台的处理器和系统 DMA 控制器 （或总线 master DMA 适配器） 表现出缓存协调性异常。 以下指导原则启用使用版本 1 或 2 的 DMA 操作接口的驱动程序 (请参阅[ **DMA\_OPERATIONS**](https://msdn.microsoft.com/library/windows/hardware/ff544071)) 以跨所有受支持的处理器维护一致的缓存状态体系结构，包括体系结构不包含硬件自动强制实施缓存一致性。

**请注意**  本主题中的指导原则仅适用于使用版本 1 和 2 DMA 操作接口的驱动程序。 使用此接口的版本 3 的驱动程序必须遵循一组不同的指导原则。 有关详细信息，请参阅[DMA 操作接口的版本 3](version-3-of-the-dma-operations-interface.md)。

 

**若要在 DMA 操作期间保持数据完整性，最低级别的驱动程序必须遵循这些指导原则**

1.  调用[ **KeFlushIoBuffers** ](https://msdn.microsoft.com/library/windows/hardware/ff552041)之前开始传输操作中可能缓存在处理器中的数据和内存中的数据之间保持一致。

    如果驱动程序调用[ **AllocateCommonBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff540575)与*CacheEnabled*参数设置为**TRUE**，驱动程序必须调用**KeFlushIoBuffers**开始传输操作中的向/从其缓冲区之前。

2.  调用[ **FlushAdapterBuffers** ](https://msdn.microsoft.com/library/windows/hardware/ff545917)末尾的每个设备传输操作以确保系统 DMA 控制器的缓冲区中的任何其余部分字节都已写入到内存或从属的设备。

    或者，致电**FlushAdapterBuffers**给定 IRP 每个传输操作的末尾以确保所有数据已读取到系统内存或写出到总线 master DMA 设备。

为何重要刷新处理器如下图所示缓存之前读取或写入操作使用 DMA，如果主机处理器和 DMA 控制器不会自动维护缓存一致性。

![关系图说明如何读取和写入操作使用 dma](images/16cchdma.png)

异步 DMA 读取或写入操作访问数据，在内存中，而不在处理器缓存。 除非此缓存已刷新通过调用**KeFlushIoBuffers**之前读取，只需通过 DMA 操作传输到系统内存的数据无法被覆盖过时的数据如果处理器缓存刷新更高版本。 除非已通过调用刷新处理器缓存**KeFlushIoBuffers**之前执行写入操作，此缓存中的数据可能会比在内存中复制更新。

**KeFlushIoBuffers** nothing 如果到，可用来确定处理器和 DMA 控制器中保存了缓存一致性，因此对此支持例程的调用具有这种平台中几乎没有开销。

由于在上图中还显示，DMA 控制器，由适配器对象表示可以让内部缓冲区。 DMA 控制器可以传输中固定大小的区块，一次的通常八个或多个字节的缓存的数据。 此外，这些 DMA 控制器可以等待，直到其内部缓冲区已满之前每个传输操作。

请考虑使用从属 DMA 读取可变大小的区块中或不是系统 DMA 控制器的缓存大小的整数倍的固定大小的区块中数据的最低级别驱动程序的情况。 除非此驱动程序调用**FlushAdapterBuffers**在每个设备传输结束时，它不能确保当实际将传输请求的驱动程序的每个字节。

主总线 DMA 设备的驱动程序还应调用**FlushAdapterBuffers** IRP 以确保所有数据是否已经都传输到系统内存中每个传输操作结束时或扩展到设备。

**FlushAdapterBuffers**返回布尔值，该值指示请求的刷新操作是否成功。 驱动程序可以使用此值以确定如何设置 I/O 状态块时完成的 DMA IRP 读取或写入操作。

 

 





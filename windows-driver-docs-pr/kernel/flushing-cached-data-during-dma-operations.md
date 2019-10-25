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
ms.openlocfilehash: 13c78deaa9d36a428127c0077d5322daf5ba8ff0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836710"
---
# <a name="flushing-cached-data-during-dma-operations"></a>执行 DMA 操作期间刷新缓存数据





在某些平台中，处理器和系统 DMA 控制器（或总线主机 DMA 适配器）显示缓存一致性异常。 以下准则启用使用第1版或第2版 DMA 操作界面的驱动程序（请参阅[**dma\_操作**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_dma_operations)），在所有支持的处理器体系结构中维护一致的缓存状态，包括不包含自动强制缓存一致性的硬件。

**请注意**  本主题中的准则仅适用于使用 DMA 操作接口版本1和版本2的驱动程序。 使用此接口版本3的驱动程序必须遵循一组不同的准则。 有关详细信息，请参阅[DMA 操作界面的版本 3](version-3-of-the-dma-operations-interface.md)。

 

**若要在 DMA 操作期间保持数据完整性，最低级别驱动程序必须遵循这些准则**

1.  在开始传输操作之前调用[**KeFlushIoBuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keflushiobuffers) ，以在处理器中缓存的数据与内存中的数据之间保持一致性。

    如果驱动程序调用[**AllocateCommonBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_common_buffer) ，并将*CacheEnabled*参数设置为**TRUE**，则驱动程序必须先调用**KeFlushIoBuffers** ，然后再开始对其缓冲区的传输操作。

2.  请在每个设备传输操作结束时调用[**FlushAdapterBuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pflush_adapter_buffers) ，以确保系统 DMA 控制器的所有缓冲区中的剩余字节已写入内存或从属设备。

    或者，在给定 IRP 的每个传输操作结束时调用**FlushAdapterBuffers** ，以确保所有数据都已读取到系统内存或写出到主线主机 DMA 设备。

下图显示了在主机处理器和 DMA 控制器不自动维护缓存一致性的情况下，在使用 DMA 读取或写入操作之前刷新处理器缓存非常重要的原因。

![说明如何使用 dma 进行读写操作的关系图](images/16cchdma.png)

异步 DMA 读取或写入操作访问内存中的数据，而不是在处理器缓存中访问数据。 除非已通过在读取之前调用**KeFlushIoBuffers**刷新了此缓存，否则 DMA 操作传输到系统内存中的数据可能会使用陈旧数据覆盖（如果稍后刷新处理器缓存）。 除非已通过在写入之前调用**KeFlushIoBuffers**来刷新处理器缓存，否则此缓存中的数据可能比内存中的副本新。

如果处理器和 DMA 控制器可以依靠来维护缓存一致性， **KeFlushIoBuffers**不会执行任何操作，因此，对此支持例程的调用在此类平台上几乎没有任何开销。

如上图所示，由适配器对象表示的 DMA 控制器可以具有内部缓冲区。 此类 DMA 控制器可以将缓存的数据传输为固定大小的区块，一次通常有八个或更多字节。 此外，在每次传输操作之前，这些 DMA 控制器都可以等待它们的内部缓冲区已满。

请考虑使用从属 DMA 读取大小可变的块区中的数据或固定大小的区块（不是系统 DMA 控制器的缓存大小的整数倍）的最低级别驱动程序的情况。 除非此驱动程序在每次设备传输结束时调用**FlushAdapterBuffers** ，否则当传输所请求的驱动程序的每个字节时，它都无法确定。

总线主控 DMA 设备的驱动程序还应在 IRP 的每个传输操作结束时调用**FlushAdapterBuffers** ，以确保所有数据都已传输到系统内存或传出到设备。

**FlushAdapterBuffers**返回一个布尔值，该值指示请求的刷新操作是否成功。 当完成 IRP 的读取或写入操作时，驱动程序可以使用此值来确定如何设置 i/o 状态块。

 

 





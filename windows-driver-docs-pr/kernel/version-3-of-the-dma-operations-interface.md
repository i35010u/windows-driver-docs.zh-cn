---
title: DMA 操作接口版本 3
description: 从 Windows 8 开始，将提供 DMA 操作接口的第3版。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f5540b25aa2b114768b7db00fd0f1e78e80d7fff
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840673"
---
# <a name="version-3-of-the-dma-operations-interface"></a>DMA 操作接口版本 3


从 Windows 8 开始，将提供 DMA 操作接口的第3版。 此接口的 **DMA \_ 操作** 结构包含多个未在此接口的先前版本中定义的新例程。 有关版本3中的例程列表，请参阅 [**DMA \_ 操作**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_dma_operations)。

尽管所有 Windows 硬件平台上都提供了 DMA 操作接口的第3版，但此接口具有许多功能，可让内核模式驱动程序使用芯片 (SoC) 集成线路上系统中的系统 DMA 控制器的高级功能。 这些功能通常包括执行散点/集合 DMA 传输的能力。 与此相反，先前版本的 DMA 操作接口会将分散/收集 DMA 传输限制到主线-主设备。 版本3界面简化了对分散/收集列表的管理，减少了复杂 DMA 传输过程中对驱动程序干预的需求。

若要使用 DMA 操作接口版本3来执行 DMA 传输，驱动程序通常会调用以下例程：

<a href="" id="iogetdmaadapter"></a>[**IoGetDmaAdapter**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdmaadapter)  
分配 DMA 适配器对象，并返回一个指向 [**dma \_ 适配器**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_dma_adapter) 结构的指针，该结构包含 dma 操作接口。

<a href="" id="getdmatransferinfo"></a>[**GetDmaTransferInfo**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pget_dma_transfer_info)  
提供执行调用方所述的 DMA 传输所需的资源的说明。

<a href="" id="allocateadapterchannelex"></a>[**AllocateAdapterChannelEx**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_adapter_channel_ex)  
分配 DMA 传输所需的资源，并将这些资源分配给 DMA 适配器对象。

<a href="" id="maptransferex"></a>[**MapTransferEx**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pmap_transfer_ex)  
为 DMA 传输初始化映射寄存器和散点/收集缓冲区，并开始传输。

<a href="" id="flushadapterbuffersex"></a>[**FlushAdapterBuffersEx**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pflush_adapter_buffers_ex)  
执行 DMA 传输结束时可能需要的任何缓存操作。

<a href="" id="freeadapterchannel"></a>[**FreeAdapterChannel**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_adapter_channel)  
释放 DMA 通道和映射寄存器。

<a href="" id="putdmaadapter"></a>[**PutDmaAdapter**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pput_dma_adapter)  
释放适配器对象。

这些例程同时用于使用专用 DMA 控制器的总线主控设备以及共享系统 DMA 控制器的从属设备。 有关驱动程序在典型 DMA 传输过程中所做调用的分步说明，请参阅 [版本 3 Dma 例程的基本调用模式](basic-calling-pattern-for-version-3-dma-routines.md)。

**注意**  
在 DMA 操作接口的第3版中，在 DMA 传输之前或之后不需要对 [**KeFlushIoBuffers**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keflushiobuffers) 例程的调用。 原因在于，以下例程涵盖了在不在硬件中强制进行缓存一致性的平台上刷新数据缓存的需求：

-   **MapTransferEx** 确保在写入 (内存到设备) 传输之前刷新处理器数据缓存。
-   **FlushAdapterBuffersEx** 可确保在读取 (设备到内存) 传输后，缓存失效。

在 x86 或 x64 处理器上， **KeFlushIoBuffers** 调用不执行任何操作，并且此调用（尽管不必要）不会干扰硬件平台的操作。 在 ARM 处理器上，在 DMA 传输过程中对 **KeFlushIoBuffers** 的调用执行不必要的缓存操作，并可能降低性能。

 

 


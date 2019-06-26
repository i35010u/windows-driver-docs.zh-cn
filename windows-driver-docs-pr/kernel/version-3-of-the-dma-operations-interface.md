---
title: DMA 操作接口版本 3
description: 可从 Windows 8 开始 DMA 操作接口的版本 3。
ms.assetid: EFB59930-7D58-4E6E-8242-66A326E239E5
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 55ab97cc145ad3ee80725dbde82b903b1ee2972e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358131"
---
# <a name="version-3-of-the-dma-operations-interface"></a>DMA 操作接口版本 3


可从 Windows 8 开始 DMA 操作接口的版本 3。 **DMA\_OPERATIONS**结构为此接口包含多个未定义此接口的早期版本中的新例程。 版本 3 中的例程的列表，请参阅[ **DMA\_OPERATIONS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_dma_operations)。

此接口尽管版本 3 的 DMA 操作接口，则可跨所有 Windows 硬件平台具有许多功能，可启用内核模式驱动程序中集成的系统芯片 (SoC) 上使用系统 DMA 控制器的高级的功能线路。 这些功能通常包括执行散播-聚集 DMA 传输的功能。 与此相反，以前版本的 DMA 操作接口限制散播-聚集 DMA 传输对总线母版设备。 版本 3 接口简化了的分散/聚拢列表管理，并在复杂 DMA 传输过程中减少了驱动程序干预的需要。

若要使用版本 3 的 DMA 操作接口执行 DMA 传输，驱动程序通常会调用以下例程：

<a href="" id="iogetdmaadapter"></a>[**IoGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdmaadapter)  
分配 DMA 适配器对象并返回一个指向[ **DMA\_适配器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_dma_adapter)结构，其中包含 DMA 操作接口。

<a href="" id="getdmatransferinfo"></a>[**GetDmaTransferInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pget_dma_transfer_info)  
提供执行由调用方所述的 DMA 传输所需的资源的说明。

<a href="" id="allocateadapterchannelex"></a>[**AllocateAdapterChannelEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pallocate_adapter_channel_ex)  
分配 DMA 传输所需的资源，并将这些资源分配给 DMA 适配器对象。

<a href="" id="maptransferex"></a>[**MapTransferEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pmap_transfer_ex)  
DMA 传输初始化地图寄存器和散播-聚集缓冲区并开始传输。

<a href="" id="flushadapterbuffersex"></a>[**FlushAdapterBuffersEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pflush_adapter_buffers_ex)  
执行可能需要 DMA 传输结束时的任何缓存操作。

<a href="" id="freeadapterchannel"></a>[**FreeAdapterChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pfree_adapter_channel)  
释放 DMA 通道和映射寄存器。

<a href="" id="putdmaadapter"></a>[**PutDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pput_dma_adapter)  
释放适配器对象。

这些例程用于使用专用的 DMA 控制器的总线 master 设备以及从属共享系统 DMA 控制器的设备。 有关驱动程序将典型的 DMA 传输过程的调用的分步说明，请参阅[版本 3 DMA 例程的基本调用模式](basic-calling-pattern-for-version-3-dma-routines.md)。

**请注意**   DMA 操作接口的版本 3 中，在调用[ **KeFlushIoBuffers** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keflushiobuffers)例程之前或之后 DMA 传输不需要。 原因是下面的例程，介绍了刷新不强制使用缓存协调性硬件中的平台上的数据缓存：

-   **MapTransferEx**可确保，将处理器数据缓存刷新之前写入 （内存设备） 传输。
-   **FlushAdapterBuffersEx**可确保缓存将失效后读取 （设备内存） 传输。

在 x86 或 x64 处理器上， **KeFlushIoBuffers**调用执行任何操作，并且此调用，而不必要的不会影响硬件平台的操作。 在 ARM 处理器上，调用**KeFlushIoBuffers**期间 DMA 传输执行缓存操作的不是必需的会降低性能。

 

 

 





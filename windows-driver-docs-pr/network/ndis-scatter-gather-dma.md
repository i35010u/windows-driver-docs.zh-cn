---
title: NDIS 分散/聚合 DMA
description: NDIS 分散/聚合 DMA
ms.assetid: 70b8321b-7b21-4d11-a9c2-46b0caa26ce6
keywords:
- 微型端口驱动程序 WDK 网络、 散播-聚集 DMA
- NDIS 微型端口驱动程序 WDK，散播-聚集 DMA
- 散播-聚集 DMA WDK 网络
- SGDMA WDK 网络
- Nic WDK 网络，系统内存传输
- 网络接口卡 WDK 网络、 s
ms.date: 06/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5623532e4f023b76079da33e76929d40b79396fc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329664"
---
# <a name="ndis-scattergather-dma"></a>NDIS 分散/聚合 DMA

[!include[NDIS DMA ARM note](ndis-dma-arm-note.md)]

NDIS 微型端口驱动程序可以使用散播-聚集 DMA (SGDMA) 方法将数据传输之间的 NIC 和系统内存。 成功的 DMA 传输要求要在 NIC 支持的地址范围中的数据的物理地址。 HAL 提供的驱动程序，以获取 MDL 链的物理地址列表，并如有必要，将双缓冲到物理地址范围的数据的机制。

在 NDIS NDIS 6.0 之前的版本，微型端口驱动程序和 NDIS 中的 SGDMA 支持限制在某些方面，以及特别是不会不适合 multipacket 发送方案。 NDIS 6.0 SGDMA 支持克服了这些限制，同时为微型端口驱动程序提供一个简单的接口。

## <a name="history-of-ndis-sgdma"></a>NDIS SGDMA 的历史记录

在 NDIS NDIS 6.0 之前的版本，NDIS 将数据包发送到微型端口驱动程序之前获取每个数据包散点图收集 (SG) 列表。 NDIS 还处理原始尝试获取 SG 列表由于过多碎片，导致失败的情况。 在此情况下，NDIS 双-缓冲区中到连续缓冲区并再次尝试该数据包。 HAL 还可以双缓冲到 NIC 支持，例如，物理地址是否数据的更高版本的 32 位最大 NIC 物理地址的数据不支持 64 位 DMA。

若要避免死锁情况下，NDIS 获取 SG 列表对于数据包，并将一个数据包发送一次。 如果 NDIS 尝试映射所有数据包发送到微型端口驱动程序之前，系统无法运行资源。 在这种情况下，NDIS 会等待映射寄存器变得可用，而某些映射寄存器的未发送的数据包已锁定的时间。 锁定数据包不能重复使用。

SGDMA 支持这种方法具有以下限制：

-   由于数据包被映射之前就微型端口驱动程序时，该驱动程序不能优化小型数据包或太零碎的数据包。 微型端口驱动程序不能双缓冲到已知的物理地址的数据包。

-   则 NDIS 传递给微型端口驱动程序的物理地址数组映射到原始数据的虚拟地址不能保证。 因此，如果该驱动程序将其发送之前更改 MDL 链中的虚拟地址处的数据，对数据所做的修改不会反映在的物理地址中的数据。 在这种情况下，NIC 将发送未修改的数据。

-   NDIS 仅限于以避免由于资源问题死锁一次发送一个数据包。 这不是发送多个数据包一样有效。

-   NDIS 无法确定微型端口驱动程序的传输功能，因为它不能预分配 SG 列表缓冲区的存储。 因此，NDIS 必须在运行时分配必要的存储。 这不是预先分配存储一样有效。

-   分配 SG 列表的 HAL 函数应调用在 IRQL = 调度\_级别。 NDIS 没有当前 IRQL 信息，因此它必须设置为调度的 IRQL\_级别，即使它已处于调度\_级别。 这不是有效的 IRQL 是否已在调度\_级别。

## <a name="benefits-of-ndis-sgdma-support"></a>NDIS SGDMA 支持的益处

在 NDIS 6.0 和更高版本 SGDMA 接口，NDIS 没有映射的数据缓冲区发送到微型端口驱动程序之前。 相反，NDIS 提供了一个接口，使驱动程序映射的网络数据。

这种方法具有以下优势：

-   NDIS 网络数据映射到 HAL 提供的接口，因为 NDIS 为屏蔽的复杂性和映射过程的详细信息的微型端口驱动程序。

-   微型端口驱动程序有权访问数据之前对其进行映射。 因此，对原始数据所做任何更改都会反映在数据由 SG 列表即使 NDIS 或 HAL 双缓冲区的数据。

-   微型端口驱动程序可以通过将其复制到具有已知的物理地址的预先分配缓冲区来优化小型或高分段的数据包的传输。 此方法避免了不是必需的因此可以提高系统性能的映射。

-   NDIS 可以安全地将多个缓冲区发送到微型端口驱动程序中。 这会导致较少调用微型端口驱动程序，因此可以提高系统性能。

-   微型端口驱动程序可以预 SG 列表的内存分配作为传输描述符块的一部分。 因此，NDIS 或微型端口驱动程序不需要在运行时为 SG 列表分配内存。

-   因为微型端口驱动程序可以运行在 IRQL = 调度\_级别，微型端口驱动程序可以避免不必要的调用引发调度到 IRQL\_级别。 例如，因为完成发送中断 DPC 的上下文中发生，所以微型端口驱动程序可以不会生成 IRQL 释放 SG 列表。


## <a name="registering-and-deregistering-dma-channels"></a>注册和取消 DMA 通道

NDIS 微型端口驱动程序调用[ **NdisMRegisterScatterGatherDma** ](https://msdn.microsoft.com/library/windows/hardware/ff563659)函数从其[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)函数DMA 通道注册到 NDIS。

微型端口驱动程序将传递到 DMA 说明[ **NdisMRegisterScatterGatherDma** ](https://msdn.microsoft.com/library/windows/hardware/ff563659)中*DmaDescription*参数。 **NdisMRegisterScatterGatherDma**返回应足够大以保存散播-聚集列表的缓冲区的大小。 微型端口驱动程序应使用此大小来预分配分散/集中列出的存储。

微型端口驱动程序还会传递[ **NdisMRegisterScatterGatherDma** ](https://msdn.microsoft.com/library/windows/hardware/ff563659)入口点*MiniportXxx*函数的 NDIS 调用以处理散播-聚集列表。 NDIS 调用微型端口驱动程序[ *MiniportProcessSGList* ](https://msdn.microsoft.com/library/windows/hardware/ff559420)函数后 HAL 已经构建了一个缓冲区的分散/集中列表。 **NdisMRegisterScatterGatherDma**提供的句柄*pNdisMiniportDmaHandle*微型端口驱动程序必须在对 NDIS 散播-聚集 DMA 函数的后续调用中使用的参数。

NDIS 微型端口驱动程序调用[ **NdisMDeregisterScatterGatherDma** ](https://msdn.microsoft.com/library/windows/hardware/ff563581)函数从其[ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)函数释放散播-聚集 DMA 资源。

## <a name="allocating-and-freeing-scattergather-lists"></a>分配和释放散播-聚集列表

NDIS 微型端口驱动程序调用[ **NdisMAllocateNetBufferSGList** ](https://msdn.microsoft.com/library/windows/hardware/ff562776)函数，在其[ *MiniportSendNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff559440)函数。 微型端口驱动程序调用**NdisMAllocateNetBufferSGList**一次为每个[ **NET\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff568376)必须映射的结构。 NDIS 资源变为可用，HAL 已准备好 SG 列表后，调用的驱动程序[ *MiniportProcessSGList* ](https://msdn.microsoft.com/library/windows/hardware/ff559420)函数。 可以调用 NDIS *MiniportProcessSGList*到微型端口驱动程序的调用之前还是之后**NdisMAllocateNetBufferSGList**返回。

若要提高系统性能，散播-聚集列表数据生成的网络时指定 MDL 开头**CurrentMdl**关联的成员[ **NET\_缓冲区\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff568381)结构。 SG 列表中的网络数据的起始偏移量从 SG 列表的开头中指定的值由**CurrentMdlOffset**关联的成员**NET\_缓冲区\_数据**结构。

微型端口驱动程序应调用时处理 DPC 发送完成的中断，和任何更多的微型端口驱动程序不需要 SG 列表之后， [ **NdisMFreeNetBufferSGList** ](https://msdn.microsoft.com/library/windows/hardware/ff563586)函数来释放SG 列表。

**请注意**  不调用[ **NdisMFreeNetBufferSGList** ](https://msdn.microsoft.com/library/windows/hardware/ff563586)驱动程序或硬件仍访问由描述的内存时[ **NET\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff568376)结构，它是与散播-聚集列表相关联。 

在访问之前接收到的数据，微型端口驱动程序必须调用[ **NdisMFreeNetBufferSGList** ](https://msdn.microsoft.com/library/windows/hardware/ff563586)以刷新内存缓存。

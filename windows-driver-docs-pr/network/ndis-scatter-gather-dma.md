---
title: NDIS 分散/聚合 DMA
description: NDIS 分散/聚合 DMA
ms.assetid: 70b8321b-7b21-4d11-a9c2-46b0caa26ce6
keywords:
- 微型端口驱动程序 WDK 网络，散点/集合 DMA
- NDIS 微型端口驱动程序 WDK、散播/聚集 DMA
- 散播/聚集 DMA WDK 网络
- SGDMA WDK 网络
- Nic WDK 网络，系统内存传输
- 网络接口卡 WDK 网络，s
ms.date: 06/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: fdfd21539c62e40f85ecd8017c7fd3685f82bd9c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833748"
---
# <a name="ndis-scattergather-dma"></a>NDIS 分散/聚合 DMA

[!include[NDIS DMA ARM note](ndis-dma-arm-note.md)]

NDIS 微型端口驱动程序可以使用散播/聚集 DMA （SGDMA）方法在 NIC 和系统内存之间传输数据。 成功的 DMA 传输要求数据的物理地址位于 NIC 支持的地址范围内。 HAL 为驱动程序提供了一种机制，用于获取 MDL 链的物理地址列表，并在必要时将数据双缓冲到一个物理地址范围。

在 NDIS 6.0 之前的 NDIS 版本中，微型端口驱动程序和 NDIS 中的 SGDMA 支持在某些方面受到限制，特别是在 multipacket 发送方案中无法正常工作。 NDIS 6.0 SGDMA 支持克服了这些限制，同时为微型端口驱动程序提供了简单的界面。

## <a name="history-of-ndis-sgdma"></a>NDIS SGDMA 的历史记录

在 NDIS 6.0 之前的 NDIS 版本中，NDIS 在将数据包发送到微型端口驱动程序之前，会为每个数据包获取散播集合（SG）列表。 NDIS 还处理由于碎片过多而导致恢复 SG 列表的原始尝试失败的情况。 在这种情况下，NDIS 会将数据包双重缓冲到一个连续的缓冲区，然后重试。 例如，如果数据的物理地址超过32位，并且 NIC 不支持64位 DMA，则 HAL 还可以将数据双缓冲到 NIC 支持的物理地址。

为避免出现死锁情况，NDIS 获取数据包的 SG 列表，并一次发送一个数据包。 如果在将所有数据包发送到微型端口驱动程序之前，NDIS 尝试映射这些数据包，则系统可能会耗尽资源。 在这种情况下，当为尚未发送的数据包锁定某些映射寄存器时，NDIS 会等待映射寄存器变为可用。 无法重复使用锁定的数据包。

此 SGDMA 支持方法有以下限制：

-   因为数据包在获取到微型端口驱动程序之前会被映射，所以，驱动程序无法针对太碎碎片的小型数据包或数据包进行优化。 微型端口驱动程序无法将数据包双缓冲到已知的物理地址。

-   不保证 NDIS 传递到微型端口驱动程序的物理地址数组映射到原始数据的虚拟地址。 因此，如果驱动程序在发送 MDL 链中的虚拟地址时更改数据，则对数据所做的修改不会反映在物理地址的数据中。 在这种情况下，NIC 将发送未修改的数据。

-   NDIS 限制为一次发送一个数据包，以避免因资源问题而导致死锁。 这不如发送多个数据包那么有效率。

-   因为 NDIS 无法确定微型端口驱动程序的传输功能，所以它不能为 SG 列表缓冲区预分配存储空间。 因此，NDIS 必须在运行时分配必要的存储。 这并不像预先分配存储一样高效。

-   分配 SG 列表的 HAL 函数应以 IRQL = 调度\_级别进行调用。 NDIS 没有当前的 IRQL 信息，因此必须将 IRQL 设置为调度\_级别，即使它已在调度\_级别。 如果 IRQL 已在调度\_级别，则这种情况并不高。

## <a name="benefits-of-ndis-sgdma-support"></a>NDIS SGDMA 支持的优点

在 NDIS 6.0 和更高版本的 SGDMA 接口中，NDIS 在将数据缓冲区发送到微型端口驱动程序之前不会映射该数据缓冲区。 相反，NDIS 为驱动程序提供了一个接口，用于映射网络数据。

此方法具有以下优点：

-   由于 NDIS 为映射网络数据提供了到 HAL 的接口，因此 NDIS 会阻止小型端口驱动程序的复杂性和详细信息。

-   小型端口驱动程序在映射之前有权访问数据。 因此，对原始数据所做的任何更改都会反映在 SG 列表表示的数据中，即使 NDIS 或 HAL 会对数据进行双缓冲。

-   微型端口驱动程序可以通过将小型或高碎片数据包复制到具有已知物理地址的预分配缓冲区来优化传输。 此方法可避免不需要的映射，从而提高系统性能。

-   NDIS 可以将多个缓冲区安全地发送到微型端口驱动程序。 这会减少对微型端口驱动程序的调用，从而提高系统性能。

-   小型端口驱动程序可以为 SG 列表作为传输描述符块的一部分预分配内存。 因此，不需要 NDIS 或微型端口驱动程序在运行时为 SG 列表分配内存。

-   由于微型端口驱动程序可以在 IRQL = 调度\_级别运行，因此微型端口驱动程序可避免不必要的调用来提高 IRQL 以调度\_级别。 例如，由于在中断 DPC 的上下文中完成了发送，小型端口驱动程序可以释放 SG 列表，而不会提高 IRQL。


## <a name="registering-and-deregistering-dma-channels"></a>注册和注销 DMA 通道

NDIS 微型端口驱动程序从其[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数调用[**NdisMRegisterScatterGatherDma**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterscattergatherdma)函数，以向 NDIS 注册 DMA 通道。

微型端口驱动程序将 DMA 说明传递到*DmaDescription*参数中的[**NdisMRegisterScatterGatherDma**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterscattergatherdma) 。 **NdisMRegisterScatterGatherDma**返回应足够大以容纳散点/集合列表的缓冲区大小。 小型端口驱动程序应使用此大小来预分配分散/收集列表的存储。

微型端口驱动程序还会将[**NdisMRegisterScatterGatherDma**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterscattergatherdma)的入口点传递给*MINIPORTXXX*函数，NDIS 调用该函数来处理散点/集合列表。 在 HAL 为缓冲区生成了散点/集合列表后，NDIS 将调用微型端口驱动程序的[*MiniportProcessSGList*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_process_sg_list)函数。 **NdisMRegisterScatterGatherDma**在*pNdisMiniportDmaHandle*参数中提供一个句柄，微型端口驱动程序必须在后续调用 NDIS 散播/聚集 DMA 函数时使用该句柄。

NDIS 微型端口驱动程序从其[*MiniportHaltEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)函数调用[**NdisMDeregisterScatterGatherDma**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterscattergatherdma)函数，以释放散点/集合 DMA 资源。

## <a name="allocating-and-freeing-scattergather-lists"></a>分配和释放散点/收集列表

NDIS 微型端口驱动程序在其[*MiniportSendNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_send_net_buffer_lists)函数中调用[**NdisMAllocateNetBufferSGList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismallocatenetbuffersglist)函数。 微型端口驱动程序对必须映射的每个[**NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构调用一次**NdisMAllocateNetBufferSGList** 。 资源变为可用且 HAL 列表准备就绪后，NDIS 将调用驱动程序的[*MiniportProcessSGList*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_process_sg_list)函数。 在微型端口驱动程序调用**NdisMAllocateNetBufferSGList**之前或之后，NDIS 可以调用*MiniportProcessSGList* 。

若要提高系统性能，则会从在**CurrentMdl**成员的关联[**网络\_缓冲区\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_data)结构中指定的 MDL 开头开始，生成散点/集合列表。 SG 列表中网络数据的开始时间是相对于 SG 列表的开头的偏移量，其值是在关联的**NET\_缓冲区**的**CurrentMdlOffset**成员中指定的值\_数据结构。

在为发送完成的中断处理 DPC 并在微型端口驱动程序不再需要 SG 列表的情况下，微型端口驱动程序应调用[**NdisMFreeNetBufferSGList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismfreenetbuffersglist)函数以释放 SG 列表。

**请注意**  不要调用[**NdisMFreeNetBufferSGList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismfreenetbuffersglist) ，因为驱动程序或硬件仍在访问由与散点/集合列表关联的[**NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构描述的内存。 

在访问接收的数据之前，微型端口驱动程序必须调用[**NdisMFreeNetBufferSGList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismfreenetbuffersglist)来刷新内存缓存。

---
title: 网络驱动程序的性能
description: 本部分介绍提高网络驱动程序性能的方法
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfe7da09580c75c974dd90553df56090df1e141d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839451"
---
# <a name="performance-in-network-drivers"></a>网络驱动程序中的性能


-   [最小化发送和接收路径长度](#minimizing-send-and-receive-path-length)
-   [对数据和代码进行分区以最大程度地减少跨处理器的共享](#partitioning-data-and-code-to-minimize-sharing-across-processors)
-   [避免错误共享](#avoiding-false-sharing)
-   [正确使用锁定机制](#using-locking-mechanisms-properly)
-   [使用64位 DMA](#using-64-bit-dma)
-   [确保缓冲区对齐正确](#ensuring-proper-buffer-alignment)
-   [使用 Scatter-Gather DMA](#using-scatter-gather-dma)
-   [支持接收端限制](#supporting-receive-side-throttle)

## <a name="minimizing-send-and-receive-path-length"></a>最小化发送和接收路径长度


尽管发送和接收路径不同于驱动程序的路径，但对于性能优化，还有一些通用规则：

-   优化通用路径。 Kernprof.exe 工具随 Windows 开发人员和 IDW 的版本一起提供，用于提取所需的信息。 开发人员应查看消耗最多 CPU 周期的例程，并尝试减少调用这些例程的频率或这些例程所用的时间。

-   减少 DPC 中花费的时间，使网络适配器驱动程序不会使用过多的系统资源，这将导致总体系统性能下降。

-   请确保调试代码不编译到驱动程序的最终发布版本中;这样可以避免执行多余的代码。

## <a name="partitioning-data-and-code-to-minimize-sharing-across-processors"></a>对数据和代码进行分区以最大程度地减少跨处理器的共享


需要进行分区以最大程度地减少跨处理器的共享数据和代码。 分区有助于减少系统总线使用率，并提高处理器缓存的效率。 为了最小化共享，驱动程序编写人员应考虑以下事项：

-   按照反序列化 [NDIS 微型端口驱动程序](deserialized-ndis-miniport-drivers.md)中所述，将驱动程序实现为反序列化的

-   使用每个处理器的数据结构来减少全局和共享数据访问。 这样，便可以在不同步的情况下保留统计信息计数器，这会减少代码路径长度并提高性能。 对于关键统计信息，请在查询时将每个处理器的计数器一起添加。 如果必须有全局计数器，请使用联锁操作，而不要使用自旋锁来操作计数器。 有关如何避免使用自旋锁的信息，请参阅下面的使用锁定机制。

    为此，可以使用 [**KeGetCurrentProcessorNumberEx**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-kegetcurrentprocessornumberex) 来确定当前处理器。 若要确定分配每个处理器的数据结构时的处理器数量，可以使用 [**KeQueryGroupAffinity**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-kequerygroupaffinity) 。

    关联掩码中设置的总位数指示系统中活动处理器的数量。 驱动程序不应假定掩码中的所有设置位都是连续的，因为在操作系统的未来版本中，处理器可能不连续编号。 SMP 计算机中的处理器数是从零开始的值。

    如果驱动程序维护每处理器数据，则可以使用 [**KeQueryGroupAffinity**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-kequerygroupaffinity) 函数来减少缓存行争用。

## <a name="avoiding-false-sharing"></a>避免错误共享


如果处理器请求彼此独立的共享变量，则会发生错误共享。 但是，因为这些变量在同一缓存行上，它们会在处理器之间共享。 在这种情况下，缓存行将在处理器之间来回移动，以便每次访问其中的任何变量，导致缓存刷新和重新加载增加。 这会增加系统总线利用率并降低整体系统性能。

若要避免错误共享，请使用 [**NdisGetSharedDataAlignment**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgetshareddataalignment)将重要数据结构（如自旋锁、缓冲区队列标头、单个链接列表) ）与缓存行边界对齐 (。

## <a name="using-locking-mechanisms-properly"></a>正确使用锁定机制


如果未正确使用，则旋转锁会降低性能。 驱动程序应尽可能最大程度地使用联锁操作来最大程度地降低自旋锁的使用。 但是，在某些情况下，旋转锁定可能是最佳选择。 例如，如果驱动程序在处理未指明回驱动程序的数据包数目的引用计数时获得自旋锁，则无需使用联锁操作。 有关详细信息，请参阅 [网络驱动程序中的同步和通知](synchronization-and-notification-in-network-drivers.md)。

下面是有效使用锁定机制的一些提示：

-   使用 NDIS 单向链接列表函数（如下所示）来管理资源池：

    [**NdisInitializeSListHead**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisinitializeslisthead)

    [**NdisInterlockedPushEntrySList**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisinterlockedpushentryslist)

    [**NdisInterlockedPopEntrySList**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisinterlockedpopentryslist)

    [**NdisQueryDepthSList**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisquerydepthslist)

-   如果需要使用自旋锁，请使用它来仅保护数据，而不是代码。 不要使用一个锁来保护公用路径中使用的所有数据。 例如，将发送和接收路径中使用的数据分隔成两个数据结构，以便发送路径需要锁定其数据时，接收路径不受影响。

-   如果使用的是自旋锁，并且该路径已位于 DPC 级别，请使用 [**NdisDprAcquireSpinLock**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisdpracquirespinlock) 和 [**NdisDprReleaseSpinLock**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisdprreleasespinlock) 函数，以避免在获取和释放锁时产生额外代码。

-   若要最大程度地减少自旋锁获取和释放的数量，请使用以下 NDIS RWLock 函数：

    [**NdisAllocateRWLock**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocaterwlock)

    [**NdisAcquireRWLockRead**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisacquirerwlockread)

    [**NdisAcquireRWLockWrite**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisacquirerwlockwrite)

    [**NdisReleaseRWLock**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreleaserwlock)

## <a name="using-64-bit-dma"></a>使用64位 DMA


64位 DMA 如果网络适配器支持64位 DMA，则必须采取步骤来避免 4 GB 范围以上的地址产生额外的副本。 当驱动程序调用 [**NdisMRegisterScatterGatherDma**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterscattergatherdma)时，必须在 *Flags* 参数中设置 **NDIS \_ SG \_ DMA \_ 64 \_ 位 \_ 地址** 标志。

## <a name="ensuring-proper-buffer-alignment"></a>确保缓冲区对齐正确


缓存行边界上的缓冲区对齐可提高将数据从一个缓冲区复制到另一个缓冲区时的性能。 大多数网络适配器接收缓冲区在首次分配时均正确对齐，但必须最终复制到应用程序缓冲区的用户数据未对齐，因为使用了标头空间。 对于 TCP 数据 (最常见的方案) ，由于 TCP、IP 和以太网标头的变化导致了0x36 字节的变化。 为了解决此问题，我们建议驱动程序分配一个略大的缓冲区，并以0xA 字节的偏移量插入数据包数据。 这将确保在为标头的0x36 字节移动缓冲区后，用户数据已正确对齐。 有关缓存行边界的详细信息，请参阅 [**NdisMAllocateSharedMemory**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismallocatesharedmemory)的 "备注" 部分。

## <a name="using-scatter-gather-dma"></a>使用 Scatter-Gather DMA


[NDIS 散播/聚集 DMA](ndis-scatter-gather-dma.md) 为硬件提供了支持，以便在物理内存的非连续范围之间传输数据。 Scatter-Gather DMA 使用 [**散播 \_ 聚集 \_ 列表**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_scatter_gather_list) 结构，该结构包含 **散点 \_ 集合 \_ 元素** 结构的数组和数组中元素的数目。 此结构是从传递给驱动程序的 send 函数的数据包描述符中检索的。 数组的每个元素都提供物理上连续 Scatter-Gather 区域的长度和起始物理地址。 驱动程序使用长度和地址信息传输数据。

将 Scatter-Gather 例程用于 DMA 操作可以通过静态锁定这些资源来提高系统资源的利用率，如使用映射寄存器时出现的情况。 有关详细信息，请参阅 [NDIS 散播/聚集 DMA](ndis-scatter-gather-dma.md)。

如果网络适配器支持 TCP 分段卸载 (大规模发送卸载) ，则驱动程序将需要传入它可以从 TCP/IP 获取的最大缓冲区大小（ [**NdisMRegisterScatterGatherDma**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterscattergatherdma)函数内的 *MaximumPhysicalMapping* 参数）。 这将保证驱动程序具有足够的映射寄存器来生成 Scatter-Gather 列表，并消除任何可能的缓冲分配和复制。 有关详细信息，请参阅以下主题：

- [确定任务卸载功能](determining-task-offload-capabilities.md)
- [卸载大型 TCP 数据包的段](offloading-the-segmentation-of-large-tcp-packets.md)

## <a name="supporting-receive-side-throttle"></a>支持接收端限制


为了最大限度地减少多媒体应用程序中媒体播放的中断，NDIS 6.20 和更高版本的驱动程序必须支持接收方限制 (RST) 处理接收中断。 有关详细信息，请参阅：

[NDIS 6.20 中的接收方限制](receive-side-throttle-in-ndis-6-20.md)将[微型端口驱动程序移植到 NDIS 6.20 所需的更改摘要中的](summary-of-changes-required-to-port-a-miniport-driver-to-ndis-6-20.md)"发送和接收代码路径"
 


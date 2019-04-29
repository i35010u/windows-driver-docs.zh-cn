---
title: 中的网络驱动程序的性能
description: 本部分介绍在网络驱动程序提高性能的方法
ms.assetid: 7EA23AA6-7673-4D88-91CA-BDDD8FBB2A4F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b81cd924da99bb167dc65ad39783fead6f0c5765
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366691"
---
# <a name="performance-in-network-drivers"></a>网络驱动程序中的性能


-   [最小化发送和接收路径长度](#minimizing-send-and-receive-path-length)
-   [若要最大程度减少跨处理器共享的代码和数据分区](#partitioning-data-and-code-to-minimize-sharing-across-processors)
-   [避免错误共享](#avoiding-false-sharing)
-   [正确使用锁定机制](#using-locking-mechanisms-properly)
-   [使用 64 位 DMA](#using-64-bit-dma)
-   [确保适当的缓冲区的一致性](#ensuring-proper-buffer-alignment)
-   [使用散播-聚集 DMA](#using-scatter-gather-dma)
-   [支持接收端限制](#supporting-receive-side-throttle)

## <a name="minimizing-send-and-receive-path-length"></a>最小化发送和接收路径长度


尽管发送和接收路径不同驱动程序到驱动程序，有一些常规规则，用于性能优化：

-   优化的公共路径。 Kernprof.exe 工具提供与开发人员和 IDW 版本的 Windows 中提取所需的信息。 开发人员应在使用大多数 CPU 周期，并尝试减少被调用这些例程的频率的例程或这些例程花费的时间。

-   减少所用的时间 DPC，以便网络适配器驱动程序不使用过多的系统资源，这可能导致总体系统性能下降。

-   请确保不到驱动程序; 的最终发布版本编译调试代码这样可避免执行过多的代码。

## <a name="partitioning-data-and-code-to-minimize-sharing-across-processors"></a>若要最大程度减少跨处理器共享的代码和数据分区


分区需要尽量在处理器上的共享的数据和代码。 分区有助于减少系统总线利用率并提高处理器缓存的效率。 为了尽量减少共享，驱动程序编写人员应考虑以下方面：

-   实施为反序列化的微型端口驱动程序，如中所述[反序列化的 NDIS 微型端口驱动程序](deserialized-ndis-miniport-drivers.md)。

-   使用每个处理器的数据结构来减少全局和共享数据访问。 这可将保留而不进行同步，这将减少代码路径长度并提高性能的统计信息计数器。 重要的统计数据，具有在查询时加在一起的每个处理器计数器。 如果您必须具有一个全局计数器，而不是数值调节钮锁使用互锁的操作来操作该计数器。 有关如何避免使用自旋锁的信息，请参阅使用锁定机制正确下面。

    若要简化此操作，请[ **KeGetCurrentProcessorNumberEx** ](https://msdn.microsoft.com/library/windows/hardware/ff552076)可用于确定当前的处理器。 若要确定何时分配数据结构的每个处理器的处理器数[ **KeQueryGroupAffinity** ](https://msdn.microsoft.com/library/windows/hardware/ff553007)可用。

    设置关联掩码中的位数总数表明系统中的活动的处理器数。 驱动程序不应假定因为处理器可能会不连续编号在将来版本的操作系统，将导致掩码中的所有集位连续。 SMP 计算机中的处理器数是从零开始的值。

    如果您的驱动程序维护每个处理器的数据，可以使用[ **KeQueryGroupAffinity** ](https://msdn.microsoft.com/library/windows/hardware/ff553007)函数以减少缓存行争用。

## <a name="avoiding-false-sharing"></a>避免错误共享


处理器请求是彼此独立的共享的变量时发生错误共享。 但是，变量是同一缓存行的因为它们是在处理器之间共享。 在这种情况下，缓存行的任何变量，在缓存刷新数导致增加每次访问的处理器之间来回传送，然后重新加载。 这提高了系统总线利用率并降低总体系统性能。

若要避免错误共享，重要的数据结构 （如自旋锁、 缓冲区队列标头、 单独链接的列表） 高速缓存线边界通过使用对齐[ **NdisGetSharedDataAlignment**](https://msdn.microsoft.com/library/windows/hardware/ff562671)。

## <a name="using-locking-mechanisms-properly"></a>正确使用锁定机制


如果未正确使用，则自旋锁可能会降低性能。 通过使用互锁的操作，只要有可能，驱动程序应尽量少自旋锁的使用。 但是，在某些情况下，旋转锁可能是最佳选择出于某些目的。 例如，如果驱动程序处理不返回到该驱动程序所指示的数据包数的引用计数时获取的数值调节钮锁定，不需要使用互锁的操作。 有关详细信息，请参阅[同步和网络驱动程序中的通知](synchronization-and-notification-in-network-drivers.md)。

下面是有效地使用锁定机制的一些提示：

-   用于管理资源池使用 NDIS 单向链接列表函数如下所示：

    [**NdisInitializeSListHead**](https://msdn.microsoft.com/library/windows/hardware/ff562739)

    [**NdisInterlockedPushEntrySList**](https://msdn.microsoft.com/library/windows/hardware/ff562764)

    [**NdisInterlockedPopEntrySList**](https://msdn.microsoft.com/library/windows/hardware/ff562760)

    [**NdisQueryDepthSList**](https://msdn.microsoft.com/library/windows/hardware/ff563753)

-   如果需要使用自旋锁，则可使用它们来仅保护数据，不是代码。 不要使用一个锁来保护在常见路径中使用的所有数据。 例如，独立中使用的数据的发送和接收路径到两个数据结构，以便当发送路径需要锁定其数据，接收路径不受影响。

-   如果您使用自旋锁，并且该路径已在 DPC 级别，使用[ **NdisDprAcquireSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff561749)并[ **NdisDprReleaseSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff561753)函数，避免产生额外的代码时获取和释放锁。

-   若要旋转锁的数量降至最低获取和版本中，使用这些 NDIS RWLock 函数：

    [**NdisAllocateRWLock**](https://msdn.microsoft.com/library/windows/hardware/ff561615)

    [**NdisAcquireRWLockRead**](https://msdn.microsoft.com/library/windows/hardware/ff560697)

    [**NdisAcquireRWLockWrite**](https://msdn.microsoft.com/library/windows/hardware/ff560698)

    [**NdisReleaseRWLock**](https://msdn.microsoft.com/library/windows/hardware/ff564523)

## <a name="using-64-bit-dma"></a>使用 64 位 DMA


64 位 DMA 如果网络适配器支持 64 位 DMA，必须采取步骤来避免额外的地址超过 4 GB 范围的副本。 当驱动程序调用[ **NdisMRegisterScatterGatherDma**](https://msdn.microsoft.com/library/windows/hardware/ff563659)，则**NDIS\_SG\_DMA\_64\_位\_地址**必须设置标志*标志*参数。

## <a name="ensuring-proper-buffer-alignment"></a>确保适当的缓冲区的一致性


将数据从一个缓冲区复制到另一个时，缓冲区高速缓存线边界上的对齐方式可以提高性能。 大多数网络适配器的接收缓冲区时首次分配，但最终必须复制到应用程序缓冲区的用户数据是由于使用的标头空间未对齐的正确对齐。 对于 TCP 数据 （最常见的方案），由于 TCP、 IP 和以太网标头 shift 会导致 0x36 字节的转变。 若要解决此问题，我们建议驱动程序分配略大于缓冲区和 0xA 字节的偏移量位置处插入数据包数据。 这将确保，由 0x36 字节标头向缓冲区后，用户数据正确地对齐。 有关高速缓存线边界的详细信息，请参阅备注部分[ **NdisMAllocateSharedMemory**](https://msdn.microsoft.com/library/windows/hardware/ff562782)。

## <a name="using-scatter-gather-dma"></a>使用散播-聚集 DMA


[NDIS 散播-聚集 DMA](ndis-scatter-gather-dma.md)提供硬件，并支持将数据传入和传出非连续范围的物理内存。 使用散播-聚集 DMA [**散点图\_收集\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff563664)结构，它包含一系列的**散点图\_收集\_元素**结构和数组中的元素数。 从数据包描述符传递给驱动程序的 send 函数检索此结构。 数组的每个元素提供的长度和从物理上连续的分散-集中区域的物理地址。 驱动程序使用的数据传输的长度和地址信息。

DMA 操作使用散播-聚集例程可以提高的系统使用了不锁定这些资源以静态方式，如果映射注册的资源的利用率。 有关详细信息，请参阅[NDIS 散播-聚集 DMA](ndis-scatter-gather-dma.md)。

如果网络适配器支持 TCP 分段卸载 （大量发送卸载），则该驱动程序将需要它是否能够获得到 TCP/IP 的最大缓冲区大小传入*MaximumPhysicalMapping*中的参数[ **NdisMRegisterScatterGatherDma** ](https://msdn.microsoft.com/library/windows/hardware/ff563659)函数。 这将保证该驱动程序有足够的映射寄存器生成散播-聚集列表并消除任何可能的缓冲区的分配和复制。 有关详细信息，请参阅以下主题：

- [确定任务卸载功能](determining-task-offload-capabilities.md)
- [卸载大型 TCP 数据包的分段](offloading-the-segmentation-of-large-tcp-packets.md)

## <a name="supporting-receive-side-throttle"></a>支持接收端限制


若要最大程度减少中断，多媒体应用程序、 NDIS 6.20 和更高版本的驱动程序中的媒体播放期间必须支持在处理过程中的接收端限制 (RST) 接收中断。 有关详细信息，请参阅：

[在 NDIS 6.20 接收端调节](receive-side-throttle-in-ndis-6-20.md)"发送和接收的代码路径"中[移植到 NDIS 6.20 的微型端口驱动程序所需的更改摘要](summary-of-changes-required-to-port-a-miniport-driver-to-ndis-6-20.md)
 

 






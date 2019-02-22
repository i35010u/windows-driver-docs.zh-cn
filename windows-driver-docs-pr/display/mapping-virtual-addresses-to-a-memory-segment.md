---
title: 虚拟地址映射到一个内存段
description: 虚拟地址映射到一个内存段
ms.assetid: 3ff64e33-eceb-4603-a3d9-11cb2f7dac85
keywords:
- 映射虚拟地址的内存段 WDK 显示
- 虚拟地址映射
- 虚拟地址映射 WDK 显示
- 映射 WDK 显示 CPU 虚拟地址
- 线性 aperture 空间段 WDK 显示
- aperture 空间段 WDK 显示
- 线性内存空间段 WDK 显示
- 内存空间段 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 053df494f4be2bcc4d1c1a0e4015a074d7697cfc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525420"
---
# <a name="mapping-virtual-addresses-to-a-memory-segment"></a>虚拟地址映射到一个内存段


## <span id="ddk_mapping_virtual_addresses_to_a_memory_segment_gg"></span><span id="DDK_MAPPING_VIRTUAL_ADDRESSES_TO_A_MEMORY_SEGMENT_GG"></span>


可以指定显示微型端口驱动程序，它定义了每个内存空间或 aperture 空间段，是否 CPU 虚拟地址可以直接映射到分配位于段中通过设置**CpuVisible**位域中的标志**标志**的成员[ **DXGK\_SEGMENTDESCRIPTOR** ](https://msdn.microsoft.com/library/windows/hardware/ff562035)段结构。

若要将 CPU 虚拟地址映射到一个段，段应具有通过 PCI aperture 线性访问。 换而言之，段内的任何分配的偏移量应为相同的 PCI 小孔中的偏移量。 因此，视频内存管理器可以计算出任何分配根据分配的偏移量给定的段内的总线相对物理的地址。

下图说明了如何虚拟地址映射到线性内存空间段。

![说明映射到线性内存空间段的虚拟地址的关系图](images/vrtlmap.png)

下图说明了如何虚拟地址映射到线性 aperture 空间段的基础页。

![说明映射到线性 aperture 空间段的基础页的虚拟地址的关系图](images/vrtlmap2.png)

虚拟地址映射到段的一部分之前, 的视频内存管理器调用显示微型端口驱动程序[ **DxgkDdiAcquireSwizzlingRange** ](https://msdn.microsoft.com/library/windows/hardware/ff559582)函数，以便该驱动程序可以设置用于访问的可能是 swizzled 分配位 aperture。 既不分配访问其中的 PCI 小孔中的偏移量，也不分配在 aperture 中占用的空间量，可以更改该驱动程序。 如果该驱动程序不能进行分配 CPU 访问给定这些约束 （例如，硬件可能用尽了取消调配的孔径），视频内存管理器逐出到系统内存分配，并允许应用程序访问存在的位。

如果在系统内存中是以前创建的分配的内容时用户模式显示驱动程序调用[ **pfnLockCb** ](https://msdn.microsoft.com/library/windows/hardware/ff568914)函数请求直接访问的内存，视频内存管理器返回到用户模式显示驱动程序，并显示微型端口驱动程序的系统内存缓冲区未参与访问分配。 因此，分配的内容不显示微型端口驱动程序进行修改，将保留在孔径取消调配格式。 这意味着，当可访问 CPU 的分配从视频内存中逐出，显示微型端口驱动程序必须 unswizzle 分配，以便应用程序可直接访问结果的系统内存位。

如果直接应用程序访问当前映射的分配相关联的 GPU 资源被逐出，分配的内容传输到系统内存，以便应用程序可以继续访问在同一个虚拟内容地址，但不同的物理介质。 若要设置传输，视频内存管理器会调用显示微型端口驱动程序[ **DxgkDdiBuildPagingBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff559587)函数创建分页缓冲区，并将 GPU 计划程序调用在驱动程序[ **DxgkDdiSubmitCommand** ](https://msdn.microsoft.com/library/windows/hardware/ff560790)函数进行排队到 GPU 执行单元的分页缓冲区。 特定于硬件的传输命令是分页缓冲区中。 有关详细信息，请参阅[提交命令缓冲区](submitting-a-command-buffer.md)。 视频内存管理器可确保视频到系统内存的转换是对应用程序不可见。 但是，该驱动程序必须确保字节的字节顺序分配逐出分配时排序通过 PCI aperture 的分配完全匹配。

对于 aperture 空间段，分配的基础部分已在系统内存，因此在将其移出过程中的数据没有传输 （取消调配） 是必需的。 因此，位于 aperture 空间段中的可访问 CPU 的分配不能为 swizzled 如果它由应用程序直接访问。

如果一个面可直接访问通过应用程序的 CPU，但将 swizzled aperture 空间段中，显示器驱动程序应实现在图面作为两个不同的分配。 当用户模式显示驱动程序创建此类图面时，它可以调用[ **pfnAllocateCb** ](https://msdn.microsoft.com/library/windows/hardware/ff568893)函数，并可以设置**NumAllocations**隶属[**D3DDDICB\_分配**](https://msdn.microsoft.com/library/windows/hardware/ff544137)结构为 2 并**pPrivateDriverData**的成员[ **D3DDDI\_ALLOCATIONINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff544364)中结构**pAllocationInfo** D3DDDICB 数组\_分配来指向有关 （例如其 swizzled 和 unswizzled 分配的专用数据格式）。 将由 GPU 分配包含 swizzled 格式中的位，应用程序将访问的分配包含 unswizzled 格式中的位。 视频内存管理器会调用显示微型端口驱动程序[ **DxgkDdiCreateAllocation** ](https://msdn.microsoft.com/library/windows/hardware/ff559606)函数来创建分配。 显示微型端口驱动程序解释的专用数据 (在**pPrivateDriverData**的成员[ **DXGK\_ALLOCATIONINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff560960)为每个结构分配） 传递从用户模式显示驱动程序。 视频内存管理器不知道分配; 的格式它只是会分配特定大小和对齐方式的内存的块的分配。 用户模式显示驱动程序的调用*锁*函数来锁定在图面，用于处理将导致以下操作：

1.  用户模式显示驱动程序调用[ **pfnRenderCb** ](https://msdn.microsoft.com/library/windows/hardware/ff568923)函数以提交到 Direct3D 运行时和到显示微型端口驱动程序的命令缓冲区中的 unswizzle 操作。

2.  用户模式显示驱动程序调用[ **pfnLockCb** ](https://msdn.microsoft.com/library/windows/hardware/ff568914)函数来锁定孔径取消调配分配。 请注意，用户模式显示驱动程序必须不设置 D3DDDILOCKCB\_DONOTWAIT 标志**标志**D3DDDICB 成员\_锁结构。

3.  **PfnLockCb**函数等待，直到执行传输 （取消调配） 之间分配。

4.  **PfnLockCb**函数请求显示微型端口驱动程序获取孔径取消调配分配的虚拟地址，并将虚拟地址返回到用户模式显示驱动**pData**成员[ **D3DDDICB\_锁**](https://msdn.microsoft.com/library/windows/hardware/ff544205)。

5.  用户模式显示驱动程序将孔径取消调配分配的虚拟地址返回到中的应用程序**pSurfData** D3DDDIARG 成员\_锁。

 

 






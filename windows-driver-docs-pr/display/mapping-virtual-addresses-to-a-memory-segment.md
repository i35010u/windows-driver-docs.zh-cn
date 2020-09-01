---
title: 将虚拟地址映射到内存段
description: 将虚拟地址映射到内存段
ms.assetid: 3ff64e33-eceb-4603-a3d9-11cb2f7dac85
keywords:
- 内存段 WDK 显示，映射虚拟地址
- 映射虚拟地址
- 虚拟地址映射 WDK 显示
- CPU 虚拟地址映射 WDK 显示
- 线性口径-空间段 WDK 显示
- 口径空间段 WDK 显示
- 线性内存空间段 WDK 显示
- 内存空间段 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4def34c4adadf44ade511e4e478976abac718bfe
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89064750"
---
# <a name="mapping-virtual-addresses-to-a-memory-segment"></a>将虚拟地址映射到内存段


## <span id="ddk_mapping_virtual_addresses_to_a_memory_segment_gg"></span><span id="DDK_MAPPING_VIRTUAL_ADDRESSES_TO_A_MEMORY_SEGMENT_GG"></span>


显示微型端口驱动程序可以指定它定义的每个内存空间或口径区段，无论 CPU 虚拟地址是否可以通过设置段的[**DXGK \_ SEGMENTDESCRIPTOR**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_segmentdescriptor)结构的**Flags**成员中的**CpuVisible**位字段标志，直接映射到位于该段中的分配。

若要将 CPU 虚拟地址映射到段，段应具有通过 PCI 口径的线性访问。 换句话说，段内任何分配的偏移量应与 PCI 口径中的偏移量相同。 因此，视频内存管理器可以根据分配在给定段内的偏移量来计算任何分配的与总线相关的物理地址。

下图说明了如何将虚拟地址映射到线性内存空间段。

![说明映射到线性内存空间段的虚拟地址的关系图](images/vrtlmap.png)

下图说明了如何将虚拟地址映射到线性口径段的基础页。

![说明映射到线性口径区基础页的虚拟地址的关系图](images/vrtlmap2.png)

在将虚拟地址映射到部分段之前，视频内存管理器会调用显示微型端口驱动程序的 [**DxgkDdiAcquireSwizzlingRange**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_acquireswizzlingrange) 函数，以便驱动程序可以设置用于访问可能 swizzled 的分配的位的口径。 驱动程序可以将偏移量更改为在其中访问分配的 PCI 口径，也不会更改为在口径中占用的空间量。 如果该驱动程序不能使分配 CPU 可访问，则 (例如，硬件可能用尽了 unswizzling 口径) ，视频内存管理器逐出将分配给系统内存，并使应用程序可以访问此处的位。

如果在用户模式显示驱动程序调用 [**pfnLockCb**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_lockcb) 函数来请求直接访问内存时，先前创建的分配的内容在系统内存中，则视频内存管理器会将系统内存缓冲区返回给用户模式显示驱动程序，并且不会在访问分配时涉及显示微型端口驱动程序。 因此，该分配的内容不会被显示微型端口驱动程序修改，并且仍采用 unswizzled 格式。 这意味着，从视频内存中收回 CPU 可访问的分配时，显示微型端口驱动程序必须 unswizzle 分配，以便应用程序可以直接访问生成的系统内存位。

如果逐出了与当前为直接应用程序访问映射的分配关联的 GPU 资源，则分配的内容将传输到系统内存中，以便应用程序可以继续访问同一虚拟地址但不同物理介质上的内容。 若要设置传输，视频内存管理器会调用显示微型端口驱动程序的 [**DxgkDdiBuildPagingBuffer**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer) 函数来创建分页缓冲区，并且 GPU 计划程序将调用驱动程序的 [**DxgkDdiSubmitCommand**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_submitcommand) 函数，将分页缓冲区排队到 GPU 执行单元中。 特定于硬件的传输命令在分页缓冲区中。 有关详细信息，请参阅 [提交命令缓冲区](submitting-a-command-buffer.md)。 视频内存管理器可确保视频到系统内存的转换对应用程序不可见。 但是，驱动程序必须确保在逐出分配时，通过 PCI 口径的分配的字节顺序与分配的字节顺序完全匹配。

对于口径区，分配的基础位已经在系统内存中，因此，不需要在逐出过程中传输 (unswizzling 的数据) 。 因此，如果可由应用程序直接访问，则位于口径区内的 CPU 可访问的分配不能 swizzled。

如果某个图面可以由应用程序通过 CPU 直接访问，但会在 swizzled 段中被视为，则显示驱动程序应将曲面实现为两个不同的分配。 当用户模式显示驱动程序创建这样的图面时，它可以调用[**pfnAllocateCb**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_allocatecb)函数，并可以将[**D3DDDICB \_ 分配**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddicb_allocate)结构的**NumAllocations**成员设置为2，并将 D3DDDI [** \_ ALLOCATIONINFO**](/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddi_allocationinfo) **的 pAllocationInfo 数组的** **pPrivateDriverData**成员设置为 \_ 指向有关分配 (例如，其 D3DDDICB 和 swizzled 格式) 。 GPU 将使用的分配包含 swizzled 格式的位，并且应用程序将访问的分配包含 unswizzled 格式的位。 视频内存管理器调用显示微型端口驱动程序的 [**DxgkDdiCreateAllocation**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createallocation) 函数来创建分配。 显示微型端口驱动程序将从用户模式显示驱动程序传递的每个分配) 解释[**DXGK \_ ALLOCATIONINFO**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_allocationinfo)结构的**pPrivateDriverData**成员中的专用数据 (。 视频内存管理器不识别分配的格式;它只为分配分配特定大小和对齐的内存块。 调用用户模式显示驱动程序的 *锁* 函数以锁定图面以进行处理会导致以下操作：

1.  用户模式显示驱动程序调用 [**pfnRenderCb**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb) 函数，将命令缓冲区中的 unswizzle 操作提交到 Direct3D 运行时，并将其提交到显示微型端口驱动程序。

2.  用户模式显示驱动程序调用 [**pfnLockCb**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_lockcb) 函数来锁定 unswizzled 分配。 请注意，用户模式显示驱动程序不得 \_ 在 D3DDDICB 锁结构的 **Flags** 成员中设置 D3DDDILOCKCB DONOTWAIT 标志 \_ 。

3.  **PfnLockCb**函数将等待，直到) 执行分配之间的传输 (。

4.  **PfnLockCb**函数请求显示微型端口驱动程序为 unswizzled 分配获取虚拟地址，并将虚拟地址返回到[**D3DDDICB \_ 锁定**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddicb_lock)的**pData**成员中的用户模式显示驱动程序。

5.  用户模式显示驱动程序将 unswizzled 分配的虚拟地址返回到 D3DDDIARG 锁定的 **pSurfData** 成员中的应用程序 \_ 。

 


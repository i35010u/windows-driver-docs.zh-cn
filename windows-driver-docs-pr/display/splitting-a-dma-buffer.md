---
title: 拆分 DMA 缓冲区
description: 拆分 DMA 缓冲区
ms.assetid: 6b35d5e2-f8aa-478a-a5a0-9f519ff0ba6f
keywords:
- DMA 缓冲 WDK 显示，拆分
- 拆分 DMA 缓冲区
- 拆分点 WDK 显示
- 修补程序-位置列表 WDK 显示
- 抢占 DMA 缓冲区 WDK 显示
- DMA 缓冲区 WDK 显示，抢占
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3c6b0694ddaa38a30c378f77c64405f07de98cc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829444"
---
# <a name="splitting-a-dma-buffer"></a>拆分 DMA 缓冲区


## <span id="ddk_splitting_a_dma_buffer_gg"></span><span id="DDK_SPLITTING_A_DMA_BUFFER_GG"></span>


"视频内存管理器" 使用拆分点将显示微型端口驱动程序提交的大型工作项分成需要更少的 GPU 资源即可执行的小型工作项。 例如，大 DMA 缓冲区可能会引用一组可能无法容纳在本地视频内存或非本地内存中的分配。 处理此类工作项的唯一方法是将其划分为多个较小的工作项，这些工作项需要的 GPU 资源更少。

**注意**   dma 缓冲区拆分和 dma 缓冲区抢占不同于独立的概念。 显示微型端口驱动程序必须始终支持 DMA 缓冲区拆分，即使在带有 GPU 的系统上，不可能出现 DMA 缓冲区抢占。 在不可能进行上下文保存和还原的 GPU 系统上，GPU 计划程序计划将 DMA 缓冲区的部分拆分回后，确保拆分部分不会与另一个 GPU 上下文中的另一个 DMA 缓冲区交错。 但是，分页缓冲区应在拆分 DMA 缓冲区的各个部分之间提交，因为在 DMA 缓冲区的拆分部分之间需要分页操作。
驱动程序用于生成应用程序 DMA 流的每个拆分点都由视频内存管理器使用。 在每个拆分点后，提交的 DMA 缓冲区应重新编程足够的 GPU 状态，以考虑可能插入到该位置的潜在分页缓冲区。

 

若要指定拆分点，显示微型端口驱动程序在 ALLOCATIONINDEX\_D3DDDI 的**PATCHLOCATIONLIST**成员中引用的每个分配的**SplitOffset**和**SlotId** [ **\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddi_patchlocationlist)成员中指定值。 为了跟踪特定 DMA 缓冲区内的分配使用量，视频内存管理器使用[**DXGK\_DRIVERCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_drivercaps)结构的**MaxAllocationListSlotId**成员创建数组所需的维度，驱动程序通过调用其[**DxgkDdiQueryAdapterInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_queryadapterinfo)函数提供。 此数组初始化为零，并填充为 "修补程序-位置" 列表的 "拆分部分" 条目。 修补程序位置的**D3DDDI\_PATCHLOCATIONLIST**的**SlotId**成员指示在需要进行分配的情况**下，必须**更新资源表中的哪个行。 DMA 缓冲区最大可运行到**SplitOffset**指定的点，且 GPU 不能访问该资源。 同样，如果新的修补位置拆分部分条目引用相同的**SlotId**，则会将上一个分配替换为新的分配，并且不再需要上一个分配（即，以前的分配可以分页）。

当在 DMA 缓冲区所需的资源中分页时，视频内存管理器会从第一个元素开始处理修补程序位置列表，并向下移动到最后一个元素。 由驱动程序填充的[**D3DDDI\_PATCHLOCATIONLIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddi_patchlocationlist)元素必须在其**SplitOffset**成员中包含值;元素严格递增（也就是说，分配必须按它们在流中的使用顺序出现）。 按其提供顺序在修补程序位置列表中引用的分配中的视频内存管理器页。 当到达一个点时，由于内存不足，视频内存管理器无法再进入分配页面，因此，视频内存管理器会将 DMA 缓冲区的当前部分提交给要执行的 GPU 计划程序。 DMA 缓冲区从上一个拆分点的开头开始，直到为无法引入的分配指定的**SplitOffset**值。 提交后，视频内存管理器使用资源表确定 DMA 流中当前拆分偏移量处的所需分配列表。 表中的所有分配都将保留在其当前物理位置，而不再使用的其他分配可能会被逐出。 然后，视频内存管理器将继续处理修补程序位置列表，可能会再次拆分多次。

每当绑定或未绑定分配时，驱动程序应指定拆分点。 若要指定分配是未绑定的，驱动程序可以在[**DXGK\_ALLOCATIONLIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_allocationlist)结构的**hDeviceSpecificAllocation**成员中指定**NULL**分配句柄，并在关联[**D3DDDI\_PATCHLOCATIONLIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddi_patchlocationlist)的**SlotId**成员中指定相应的值。 驱动程序应取消对大资源的绑定，增加视频内存管理器解决复杂内存放置问题的机会。

同样，驱动程序应在每个拆分点重新编程大资源。 在拍摄拆分点时，视频内存管理器会强制将之前绑定的分配保留给以前的分配。 这会导致内存碎片，这可能会导致失败，以解决可能已解决的复杂内存放置问题，而这些问题可能已在不是以前绑定的分配限制的情况下解决。 当在拆分点计算状态时，视频内存管理器将确定正在该拆分点 reprogrammed 的槽标识符（**SlotId**），并在此拆分点上忽略位置限制。这是在该拆分点上的每个修补位置列表元素。 例如，如果驱动程序使用 64 MB 纹理，则在每个拆分点处 reprogramming 纹理会使视频内存管理器可以灵活地在拆分点之间的内存中移动纹理（如有必要）。

 

 






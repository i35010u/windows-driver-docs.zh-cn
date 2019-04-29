---
title: 拆分 DMA 缓冲区
description: 拆分 DMA 缓冲区
ms.assetid: 6b35d5e2-f8aa-478a-a5a0-9f519ff0ba6f
keywords:
- DMA 缓冲区 WDK 显示拆分
- 拆分 DMA 缓冲区
- 拆分点 WDK 显示
- 修补程序位置列出 WDK 显示
- 优先 WDK 显示 DMA 缓冲区
- DMA 缓冲区 WDK 显示抢占
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c1dab57436ab0eec35ff35c6bd289dd483a710d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376019"
---
# <a name="splitting-a-dma-buffer"></a>拆分 DMA 缓冲区


## <span id="ddk_splitting_a_dma_buffer_gg"></span><span id="DDK_SPLITTING_A_DMA_BUFFER_GG"></span>


视频内存管理器使用拆分点将显示微型端口驱动程序提交到较小需要 GPU 资源较少，若要执行的工作项的大型工作项。 例如，较大的 DMA 缓冲区可能会引用可能不适合在本地的视频内存中或非本地内存的分配一组。 处理此类工作项的唯一方法是将其分成多个较小的工作项需要更少 GPU 资源。

**请注意**   DMA 缓冲区拆分和 DMA 缓冲区抢占是不同的独立概念。 显示微型端口驱动程序必须始终支持拆分甚至具有 GPU DMA 缓冲区抢占不可能的系统上的 DMA 缓冲区。 具有 GPU 上下文位置保存和还原的系统上不能，DMA 缓冲区连续不断地确保拆分部分的 GPU 计划程序计划拆分部分不交织在一起，从不同的 GPU 上下文的另一个 DMA 缓冲区。 但是，分页缓冲区应提交部分拆分 DMA 缓冲区之间因为分页操作所需的 DMA 缓冲区的拆分部分之间。
视频内存管理器使用的驱动程序使用来生成应用程序 DMA 流的每个拆分点。 每个拆分到帐户潜在的分页缓冲区可能会在该位置插入点后，提交的 DMA 缓冲区应对足够 GPU 状态。

 

若要指定拆分点，显示微型端口驱动程序指定中的值**SplitOffset**并**SlotId**的成员[ **D3DDDI\_PATCHLOCATIONLIST** ](https://msdn.microsoft.com/library/windows/hardware/ff544630)结构中引用每个分配**AllocationIndex** D3DDDI 成员\_PATCHLOCATIONLIST。 若要跟踪分配特定的 DMA 缓冲区中的使用情况，视频内存管理器创建的数组使用所需的尺寸**MaxAllocationListSlotId**的成员[ **DXGK\_DRIVERCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff561062)驱动程序通过调用提供的结构及其[ **DxgkDdiQueryAdapterInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff559746)函数。 此数组已初始化为零，并且随着处理的修补程序位置列表的拆分部分条目填充。 **SlotId**的成员**D3DDDI\_PATCHLOCATIONLIST**修补程序，将指示必须更新资源表中的哪些行位置时**SplitOffset**成员指示分配是必需的 DMA 缓冲区内的偏移量。 可以指定的点之前运行 DMA 缓冲区**SplitOffset**而无需也可以访问 GPU 资源。 同样，如果新的修补程序位置拆分部分条目引用相同**SlotId**、 新的分配，将替换为以前的分配和上一个分配不再需要 （即，以前分配可以是调出）。

当 DMA 缓冲区所需的资源中的分页，视频内存管理器处理的修补程序位置列表中的第一个元素开始，向下移动到最后一个元素。 [ **D3DDDI\_PATCHLOCATIONLIST** ](https://msdn.microsoft.com/library/windows/hardware/ff544630)填充驱动程序的元素必须包含中的值及其**SplitOffset**成员; 元素是严格递增 （即，分配必须显示在流中的使用顺序）。 视频内存管理器中会向其提供的顺序中的修补程序位置列表中引用的分配页。 当其中的视频内存管理器可以不再页-在分配中由于内存不足的情况达到某个点时，视频内存管理器将提交到执行 GPU 计划程序正在准备 DMA 缓冲区的当前部分。 最多从以前的拆分点开始运行 DMA 缓冲区**SplitOffset**无法使中分配为指定的值。 提交后，视频内存管理器确定需要在当前偏移量 DMA 流中使用拆分资源表分配的列表。 对表的所有分配都保存在其当前的物理位置，而不再使用的其他分配可能会被逐出。 视频内存管理器然后继续处理 patch 位置列表中，可能会再次拆分多次。

该驱动程序应指定每次分配是绑定或未绑定的拆分点。 若要指定分配是未绑定的该驱动程序可以指定**NULL**中的分配句柄**hDeviceSpecificAllocation**的成员[ **DXGK\_ALLOCATIONLIST** ](https://msdn.microsoft.com/library/windows/hardware/ff560975)结构中的相应值**SlotId**关联的成员[ **D3DDDI\_PATCHLOCATIONLIST**](https://msdn.microsoft.com/library/windows/hardware/ff544630). 该驱动程序应取消绑定大型资源，以提高视频内存管理器可以解决复杂的内存放置问题的可能性。

同样，该驱动程序应该对大型资源，在每个拆分点。 采用是拆分点，被强制的视频内存管理器以前分配到保留以前绑定的分配。 这将导致失败来解决复杂的内存放置问题已解决的没有以前绑定的分配限制可能会导致的内存的碎片。 视频内存管理器在计算时是拆分点的状态，确定哪些槽标识符 (**SlotId**) 正在囿该拆分点 (即，每个共享同一修补程序位置列表元素**SplitOffset**与其他元素的值)，并忽略对此拆分点的位置限制。 例如，如果驱动程序将使用 64 MB 纹理，重新编程在每个拆分点该纹理灵活的视频内存管理器移动该纹理在内存中拆分点，如有必要之间。

 

 






---
title: GPU 虚拟地址
description: 在设备驱动程序接口 (DDI) 级别的逻辑 4 KB 或 64KB 页进行管理的图形处理单元 (GPU) 的虚拟地址。
ms.assetid: 65BD05FC-06FD-4DC2-977A-7F48E72B4858
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e9eb89da04711dd2760d01fca08e2e46a34c085
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379951"
---
# <a name="gpu-virtual-address"></a>GPU 虚拟地址


在设备驱动程序接口 (DDI) 级别的逻辑 4 KB 或 64KB 页进行管理的图形处理单元 (GPU) 的虚拟地址。 这允许 GPU 虚拟地址引用系统内存，从而始终分配粒度 4 KB 或可能托管在 4 KB 或 64 KB 的内存段页。

视频内存管理器支持多级虚拟地址转换方案，其中使用多个级别的页表虚拟地址转换。 级别编号从 0 开始并且零级分配给叶级别。 从根级别的页表开始转换。 如果两个页表级别数，根页表可以调整大小以容纳具有 GPU 虚拟地址空间大小可变的进程。 每个级别所描述[ **DXGK\_页面\_表\_级别\_DESC** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_page_table_level_desc) 过程中由内核模式驱动程序已满的结构[*DxgkDdiQueryAdapterInfo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_queryadapterinfo)调用。 内核模式驱动程序还填写[ **DXGK\_GPUMMUCAPS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_gpummucaps)指针顶端才结构来描述 GPU 虚拟寻址支持。

每个进程具有自己的 GPU 虚拟地址空间。 内核模式驱动程序可以为执行设置流程的图形上下文之前将获取[ *DxgkDdiSetRootPageTable* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_setrootpagetable)设置根页表地址的调用。

下图中显示两个页表级别的情况下的虚拟地址转换。

![显示两个页表级别的情况下的虚拟地址转换。](images/gpu-virtual-address.1.png)

GPU 虚拟地址已[ **DXGK\_GPUMMUCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_gpummucaps)::**VirtualAddressBitCount**位。

低位\[0-11\]表示以字节为单位在页面中的偏移量。 下一步[ **DXGK\_页面\_表\_级别\_DESC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_page_table_level_desc)::**PageTableIndexBitCount**位表示叶级别页表中的页表项的索引。

页表中的条目数是 2<sup>DXGK\_页面\_表\_级别\_DESC::PageTableIndexBitCount</sup>和的页表大小[ **DXGK\_页上\_表\_级别\_DESC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_page_table_level_desc)::**PageTableSizeInBytes**字节。

其余位表示到根页表中的页表项的索引。 根页表是可调整大小的 2 级翻译方案和一个新[ *DxgkDdiGetRootPageTableSize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_getrootpagetablesize)DDI 引入若要获取其大小。

[ **DXGK\_PTE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_dxgk_pte)结构通过使用 DDI 来表示页表条目。 此结构表示每个条目，Microsoft DirectX 图形内核管理有关的信息。 该驱动程序使用此信息来生成特定于硬件的页表项。

## <a name="span-idcreationofpagetableallocationsspanspan-idcreationofpagetableallocationsspanspan-idcreationofpagetableallocationsspancreation-of-page-table-allocations"></a><span id="Creation_of_page_table_allocations"></span><span id="creation_of_page_table_allocations"></span><span id="CREATION_OF_PAGE_TABLE_ALLOCATIONS"></span>页表分配的创建


页表创建为隐式分配，但没有用户模式驱动程序或处理的内核模式驱动程序。

若要分配的页表，视频内存管理器分配的大小分配[ **DXGK\_页面\_表\_级别\_DESC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_page_table_level_desc)::**PageTableSizeInBytes**从在指定的段**DXGK\_页面\_表\_级别\_DESC**::**PageTableSegmentId**. 在创建后，视频内存管理器初始化到页表中的每个条目*无效*使用新[ *UpdatePageTable* ](https://docs.microsoft.com/windows-hardware/drivers/display/dxgkddiupdatepagetable)分页操作。 页表永远不会更改大小，除了 2 级转换方案中的根页表。

视频内存管理器支持重设大小的 2 级转换方案中的根页表。 创建覆盖指定的数量的地址空间的根页表时，调用新的视频内存管理器[ *DxgkDdiGetRootPageTableSize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_getrootpagetablesize)DDI 来确定所需的分配为其大小。 视频内存管理器然后分配在段中，指定该大小的分配[ **DXGK\_页面\_表\_级别\_DESC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_page_table_level_desc)::**PageTableSegmentId**对于根级别。 在创建后，视频内存管理器初始化以无效的使用新的页表中的每个条目[ *UpdatePageTable* ](https://docs.microsoft.com/windows-hardware/drivers/display/dxgkddiupdatepagetable)分页操作。 根页表可以扩大或收缩随着进程所需的视频的地址空间量扩展和缩减。 创建根页表后，调用新的视频内存管理器[ *DxgkDdiSetRootPageTable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_setrootpagetable)DDI 能够将执行内的各种上下文相关联的新创建的根页表.

在链接的显示适配器配置中，根页表创建为*LinkMirrored*分配，后者具有相同的内容和位于以下位置的链接中的每个 GPU 上的同一物理地址。 较低级别的页表都被分配作为*LinkInstanced*分配以反映其内容可能有所不同 GPU，通常由于不同对等方映射这一事实。 所有的 Gpu 上单独更新的页表内容。

## <a name="span-idgrowingandshrinkingarootpagetablespanspan-idgrowingandshrinkingarootpagetablespanspan-idgrowingandshrinkingarootpagetablespangrowing-and-shrinking-a-root-page-table"></a><span id="Growing_and_shrinking_a_root_page_table"></span><span id="growing_and_shrinking_a_root_page_table"></span><span id="GROWING_AND_SHRINKING_A_ROOT_PAGE_TABLE"></span>扩大和缩小根页表


本部分是仅适用于具有两个级别的页表的系统。 当大于两个，每个级别的页表大小的页表级别数是由虚拟寻址 caps 定义，并且为固定。

当用户模式驱动程序请求 GPU 虚拟地址时，视频内存管理器会增大可处理请求的进程的地址空间的大小。 实现这一点由不断扩大的当前根页表 （如有必要） 的大小以及为新的范围中分配新页表。

增长根页表的视频内存管理器创建另一个根页表分配，使得驻留，并初始化其项，使用[ *UpdatePageTable* ](https://docs.microsoft.com/windows-hardware/drivers/display/dxgkddiupdatepagetable)操作，并销毁旧分配。 [ *DxgkDdiGetRootPageTableSize* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_getrootpagetablesize)函数用于获取新的页表的大小以字节为单位。

若要收缩根页表，视频内存管理器创建新的页表分配、 使常驻、 将旧的页表的一部分复制到新的一个使用*CopyRootPageTable*分页操作和销毁旧分配。

大小调整操作完成之后，视频内存管理器调用[ *DxgkDdiSetRootPageTable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_setrootpagetable)DDI 能够其新的根页表相关联的受影响的上下文。

## <a name="span-idupdatingpagetablespanspan-idupdatingpagetablespanspan-idupdatingpagetablespanupdating-page-table"></a><span id="Updating_page_table"></span><span id="updating_page_table"></span><span id="UPDATING_PAGE_TABLE"></span>正在更新的页表


图面移动内存中时，视频内存管理器会更新以反映新的图面位置的页表的内容。 这可通过新[ *UpdatePageTable* ](https://docs.microsoft.com/windows-hardware/drivers/display/dxgkddiupdatepagetable)分页 DDIs。

## <a name="span-idmovingapagetablespanspan-idmovingapagetablespanspan-idmovingapagetablespanmoving-a-page-table"></a><span id="Moving_a_page_table"></span><span id="moving_a_page_table"></span><span id="MOVING_A_PAGE_TABLE"></span>移动页表


页表可能会重定位或当设备处于空闲或挂起时逐出的视频内存管理器。 视频内存管理器时移动的页表，更新要使用引用的页表的新位置的更高级别页表[ *UpdatePageTable*](https://docs.microsoft.com/windows-hardware/drivers/display/dxgkddiupdatepagetable)DDIs。

视频内存管理器时的根页表本身会保存下来，调用[ *DxgkDdiSetRootPageTable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_setrootpagetable)DDI 通知受影响的上下文，其页目录的新位置。

## <a name="span-idphysicalpagesizespanspan-idphysicalpagesizespanspan-idphysicalpagesizespanphysical-page-size"></a><span id="Physical_page_size"></span><span id="physical_page_size"></span><span id="PHYSICAL_PAGE_SIZE"></span>物理页大小


如前文所述以前的视频内存管理器支持两种页面大小。 在 4 KB 页中，始终管理系统内存，而可能会在 4 KB 或 64KB 粒度由内核模式驱动程序管理内存段。

时选择的虚拟内存管理 64KB 页中，所有分配自动对齐和大小调整，以将多个为 64 KB。

扩展为 64 KB 的所有分配可以具有很大量内存的影响。 它负责的用户模式驱动程序打包到一个更大为了避免内存浪费在小的分配。

映射到大型的 64 KB 的内存段页 GPU 虚拟地址时, 的视频内存管理器将为 16 的内存段中的连续 4 KB 页映射 4 KB 页表项。 确保虚拟地址和物理地址共享相同的 64KB 对齐方式 （即虚拟地址和物理地址的底部 16 位保证是匹配。）。

 

 






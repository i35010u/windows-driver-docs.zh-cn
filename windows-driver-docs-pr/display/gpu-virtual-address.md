---
title: GPU 虚拟地址
description: 图形处理单元 (GPU) 虚拟地址在设备驱动程序接口上的逻辑4KB 或 64 KB 页中进行管理 (DDI) 级别。
ms.assetid: 65BD05FC-06FD-4DC2-977A-7F48E72B4858
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4da5521d95aab988960260d6e283182551eca9ae
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89064206"
---
# <a name="gpu-virtual-address"></a>GPU 虚拟地址


图形处理单元 (GPU) 虚拟地址在设备驱动程序接口上的逻辑4KB 或 64 KB 页中进行管理 (DDI) 级别。 这允许 GPU 虚拟地址引用系统内存，该内存始终在4KB 粒度或内存段页面上分配，可在4KB 或64KB 进行管理。

视频内存管理器支持多级虚拟地址转换方案，在此方案中，有多个级别的页表用于转换虚拟地址。 级别从零开始编号，级别0分配给叶级。 转换从根级别页表开始。 当页表级别数为2时，可以调整根页表的大小，以适应具有可变 GPU 虚拟地址空间大小的进程。 每个级别都由 [**DXGK \_ 页 \_ 表 \_ 级别 \_ DESC**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_page_table_level_desc) 结构描述，该结构由内核模式驱动程序在 [*DxgkDdiQueryAdapterInfo*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_queryadapterinfo) 调用期间填充。 内核模式驱动程序还会填充 [**DXGK \_ GPUMMUCAPS**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_gpummucaps) cap 结构，以描述 GPU 虚拟寻址支持。

每个进程都有其自己的 GPU 虚拟地址空间。 在为执行设置进程的图形上下文之前，内核模式驱动程序将获取一个 [*DxgkDdiSetRootPageTable*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_setrootpagetable) 调用，该调用可设置根页表地址。

下面的关系图显示了两页表级别的虚拟地址转换。

![显示两个页面表级别的虚拟地址转换。](images/gpu-virtual-address.1.png)

GPU 虚拟地址具有 [**DXGK \_ GPUMMUCAPS**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_gpummucaps)：：**VirtualAddressBitCount** 位。

低位 \[ 0-11 \] 表示页中的偏移量（以字节为单位）。 下一个 [**DXGK \_ 页 \_ 表 \_ 级别 \_ DESC**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_page_table_level_desc)：：**PageTableIndexBitCount** 位表示叶级页表中页表项的索引。

页表中的条目数为 2<sup>DXGK \_ 页 \_ 表 \_ 级别 \_ desc：:P agetableindexbitcount</sup> ，页表大小为 [**DXGK \_ 页 \_ 表 \_ 级别 \_ DESC**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_page_table_level_desc)：：**PageTableSizeInBytes** 字节。

其余位表示根页表中页表项的索引。 根页表的大小可用于2级转换方案，并引入了新的 [*DxgkDdiGetRootPageTableSize*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_getrootpagetablesize)DDI 来获取其大小。

[**DXGK \_ PTE**](/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_dxgk_pte)结构通过 DDI 用于表示页表项。 此结构表示有关 Microsoft DirectX 图形内核管理的每个项的信息。 驱动程序使用此信息来生成特定于硬件的页表项。

## <a name="span-idcreation_of_page_table_allocationsspanspan-idcreation_of_page_table_allocationsspanspan-idcreation_of_page_table_allocationsspancreation-of-page-table-allocations"></a><span id="Creation_of_page_table_allocations"></span><span id="creation_of_page_table_allocations"></span><span id="CREATION_OF_PAGE_TABLE_ALLOCATIONS"></span>创建页表分配


页表创建为隐式分配，没有用户模式驱动程序或内核模式驱动程序句柄。

为了分配页表，视频内存管理器会从段分配大小 [**DXGK \_ 页 \_ 表 \_ 级别 \_ desc**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_page_table_level_desc)：：**PageTableSizeInBytes** ，并在 **DXGK \_ 页 \_ 表 \_ 级别 \_ desc**：：**PageTableSegmentId**中指定。 创建后，视频内存管理器使用新的[*UpdatePageTable*](./dxgkddiupdatepagetable.md)分页操作将页表中的每个条目初始化为*无效*。 页表从不更改大小（2级转换方案中的根页表除外）。

视频内存管理器支持调整2级转换方案中根页表的大小。 在创建包含指定地址空间的根页面表时，视频内存管理器会调用新的 [*DxgkDdiGetRootPageTableSize*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_getrootpagetablesize)DDI 来确定所需的分配大小。 然后，视频内存管理器会在段中分配该大小的分配，由 [**DXGK \_ 页 \_ 表 \_ 级别 \_ DESC**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_page_table_level_desc)：：**PageTableSegmentId** 为根级别指定。 创建后，视频内存管理器使用新的 [*UpdatePageTable*](./dxgkddiupdatepagetable.md) 分页操作将页表中的每个条目初始化为无效。 当进程所需的视频地址空间量扩展和收缩时，根页表可以增大或收缩。 创建根页表后，视频内存管理器会调用新的 [*DxgkDdiSetRootPageTable*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_setrootpagetable)DDI 将新创建的根页表与将在中执行的各种上下文相关联。

在链接的显示适配器配置中，根页表创建为 *LinkMirrored* 分配，它们具有相同的内容，并且位于链接中每个 GPU 上的相同物理地址。 较低级别的页表被分配为 *LinkInstanced* 分配，以反映其内容可能在 GPU 之间有所不同的事实，通常是由于不同的对等映射。 页面表的内容在所有 Gpu 上分别更新。

## <a name="span-idgrowing_and_shrinking_a_root_page_tablespanspan-idgrowing_and_shrinking_a_root_page_tablespanspan-idgrowing_and_shrinking_a_root_page_tablespangrowing-and-shrinking-a-root-page-table"></a><span id="Growing_and_shrinking_a_root_page_table"></span><span id="growing_and_shrinking_a_root_page_table"></span><span id="GROWING_AND_SHRINKING_A_ROOT_PAGE_TABLE"></span>增大和收缩根页表


本部分仅适用于具有两级页面表的系统。 当页表级别的数量大于2时，每个级别的页表大小由虚拟寻址 cap 定义，并是固定的。

当用户模式驱动程序请求 GPU 虚拟地址时，视频内存管理器会增大进程的地址空间大小以容纳请求。 这是通过增加当前根页表的大小来实现的 (如有必要) 并为新范围分配新的页表。

为了增加根页表，视频内存管理器会创建另一个根页表分配，使其驻留，并使用 [*UpdatePageTable*](./dxgkddiupdatepagetable.md) 操作初始化其条目，并销毁旧分配。 [*DxgkDdiGetRootPageTableSize*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_getrootpagetablesize)函数用于获取新页表的大小（以字节为单位）。

若要收缩根页表，视频内存管理器会创建一个新的页表分配，使其驻留，并使用 *CopyRootPageTable* 分页操作将旧页表的一部分复制到新页表，并销毁旧的分配。

调整大小操作完成后，视频内存管理器将调用 [*DxgkDdiSetRootPageTable*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_setrootpagetable)DDI，将受影响的上下文与新的根页面表相关联。

## <a name="span-idupdating_page_tablespanspan-idupdating_page_tablespanspan-idupdating_page_tablespanupdating-page-table"></a><span id="Updating_page_table"></span><span id="updating_page_table"></span><span id="UPDATING_PAGE_TABLE"></span>正在更新页表


当图面在内存中移动时，视频内存管理器会更新页面表的内容以反映新的图面位置。 这是通过新的 [*UpdatePageTable*](./dxgkddiupdatepagetable.md) 分页 DDIs 来完成的。

## <a name="span-idmoving_a_page_tablespanspan-idmoving_a_page_tablespanspan-idmoving_a_page_tablespanmoving-a-page-table"></a><span id="Moving_a_page_table"></span><span id="moving_a_page_table"></span><span id="MOVING_A_PAGE_TABLE"></span>移动页表


当设备处于空闲或挂起状态时，视频内存管理器可能会重新定位或逐出页表。 在移动页面表时，视频内存管理器将更新较高级别的页面表，以使用 [*UpdatePageTable*](./dxgkddiupdatepagetable.md)DDIs 引用页面表的新位置。

当重定位根页表本身时，视频内存管理器将调用 [*DxgkDdiSetRootPageTable*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_setrootpagetable)DDI 来通知其页面目录的新位置的受影响的上下文。

## <a name="span-idphysical_page_sizespanspan-idphysical_page_sizespanspan-idphysical_page_sizespanphysical-page-size"></a><span id="Physical_page_size"></span><span id="physical_page_size"></span><span id="PHYSICAL_PAGE_SIZE"></span>物理页大小


如前所述，视频内存管理器支持两种页面大小。 系统内存始终在4KB 页中进行管理，而在内核模式驱动程序确定的情况下，可以在4KB 或64KB 粒度控制内存段。

当选择在64KB 页中管理虚拟内存时，所有分配都将自动对齐并调整为 64 KB 的倍数。

将所有分配扩展到64KB 会对内存产生严重影响。 用户模式驱动程序负责将小型分配打包为一个较大的分配，以避免浪费内存。

将 GPU 虚拟地址映射到大64KB 内存段页面时，视频内存管理器会将4KB 页表项映射到内存段中的16个连续4KB 页。 保证虚拟地址和物理地址共享相同的64KB 对齐 (即，虚拟地址的底部16bits 和物理地址可保证匹配。 ) 。

 


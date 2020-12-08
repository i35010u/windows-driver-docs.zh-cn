---
title: GPU 段
description: 图形处理单元 (GPU) 对物理内存的访问在设备驱动程序界面中进行了抽象， (由分段模型 DDI) 。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f1e4b0652f433a589ae132776ade63f199eb7e0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825755"
---
# <a name="gpu-segments"></a>GPU 段


图形处理单元 (GPU) 对物理内存的访问在设备驱动程序界面中进行了抽象， (由分段模型 DDI) 。 内核模式驱动程序通过枚举一组段来表示可用的物理内存资源，这些段随后由视频内存管理器进行管理。

Windows 显示驱动程序模型中有三种类型的段 (WDDM) v2：

<span id="Memory_Segment"></span><span id="memory_segment"></span><span id="MEMORY_SEGMENT"></span>内存段  
内存段表示内存，专用于 GPU。 这可能是在集成 GPU 上的离散 GPU 或固件/驱动程序保留内存上 VRAM 的。 可以枚举多个内存段。

在 WDDM v2 中新增，内存段被管理为大小为4KB 或64KB 的物理页池。 使用 *填充* / *传输* / *放弃* / *FillVirtuall* / *TransferVirtual* 分页操作将外围数据复制到内存段并将其移出。

CPU 可以通过以下两种方式之一来访问内存段的内容。 首先，内存段可能会显示在 CPU 的物理地址空间中，在这种情况下，视频内存管理器只需将 CPU 虚拟地址直接映射到段内的分配。 在 WDDM v2 中新增，视频内存管理器还支持通过与该分段关联的可编程 CPU 主机口径来访问内存段的内容。

<span id="Aperture__Segment"></span><span id="aperture__segment"></span><span id="APERTURE__SEGMENT"></span>口径段  
光圈段是一个全局页表，用于使不连续的系统内存页在 GPU 引擎的角度上显得连续。

在 WDDM v2 中，必须报告单个光圈段。

<span id="System_Memory_Segment"></span><span id="system_memory_segment"></span><span id="SYSTEM_MEMORY_SEGMENT"></span>系统内存段  
系统内存段是表示系统内存引用的隐式段 (即来宾物理地址) 。 内核模式驱动程序不会直接枚举系统内存段。 它由视频内存管理器隐式枚举并始终被分配 `SegmentId==0` 。 若要在系统内存段中放置分配，内核模式驱动程序需要使用口径段 ID。

## <a name="span-idphysical_memory_referencespanspan-idphysical_memory_referencespanspan-idphysical_memory_referencespanphysical-memory-reference"></a><span id="Physical_memory_reference"></span><span id="physical_memory_reference"></span><span id="PHYSICAL_MEMORY_REFERENCE"></span>物理内存引用


在 DDI 中，物理内存引用始终采用段 ID 段偏移量对的形式。

## <a name="span-idaccessing_allocations_by_physical_addressspanspan-idaccessing_allocations_by_physical_addressspanspan-idaccessing_allocations_by_physical_addressspanaccessing-allocations-by-physical-address"></a><span id="Accessing_allocations_by_physical_address"></span><span id="accessing_allocations_by_physical_address"></span><span id="ACCESSING_ALLOCATIONS_BY_PHYSICAL_ADDRESS"></span>按物理地址访问分配


GPU 引擎不支持 GPU 虚拟寻址，需要通过其物理地址访问分配。 这就意味着分配如何从段获取分配的资源。 物理引用意味着必须在内存段中连续分配分配，或在口径段内占用连续范围。

若要避免不必要和昂贵的连续分配，内核模式驱动程序必须显式标识分配，这些分配需要在创建分配时设置新的 [**DXGK \_ ALLOCATIONINFOFLAGS2**](./dxgk-allocationinfoflags2.md)：：**AccessedPhysically** 标志，在物理上由呈现引擎访问。

当驻留在系统内存中时，此类分配将映射到口径段。 当驻留在内存段时，分配是连续的。 以这种方式创建的分配可以通过在物理寻址模式下操作的引擎上的分配列表进行引用。

未将此标志设置为的分配将作为内存段中的一组页或系统内存中的一组页分配，这些分配可通过 GPU 虚拟地址进行访问。 以这种方式创建的分配不能通过分配列表进行引用。 将拒绝引用分配的任何命令缓冲区提交。

主要表面被理解为以物理方式由显示控制器访问，并将在内存段中连续分配，或在显示时被映射到光圈段。 内核模式驱动程序只应在呈现引擎将在物理上访问分配时设置 **AccessedPhysically** 标志。 主图面上的隐式物理访问与显式标志之间的区别在于分配将映射到孔径。 设置 **AccessedPhysically** 标志后，只要分配为驻留，就会将分配映射到口径。 未设置此标志的主表面仅在显示时才会映射到口径。 这有助于消除对光圈段的压力，因为通常只显示几个主要表面，而其中可能存在大量的现有表面并将其呈现到 (也就是说，所有 *FlipEx* 交换链都在 *dFlip* / *iFlip* 场景) 中创建为主要和可能可显示的表面。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"></td>
<td align="left">AccessedPhysically = = 0</td>
<td align="left">AccessedPhysically = = 1</td>
<td align="left">主 && AccessedPhysically = = 0</td>
</tr>
<tr class="even">
<td align="left">内存段</td>
<td align="left"><p><strong>页集</strong></p>
<p>仅允许 GPU 虚拟访问。</p></td>
<td align="left"><p><strong>系列</strong></p>
<p>允许 GPU 物理访问</p></td>
<td align="left"><p><strong>系列</strong></p>
<p>呈现引擎仅允许 GPU 虚拟访问。</p></td>
</tr>
<tr class="odd">
<td align="left">口径段</td>
<td align="left"><p><strong>未映射</strong></p>
<p>系统内存页面，仅由 GPU 页面表映射，而不是在口径段中进行映射。</p>
<p>仅允许 GPU 虚拟访问。</p></td>
<td align="left"><p><strong>在常驻时映射</strong></p>
<p>允许 GPU 物理访问。</p></td>
<td align="left"><p><strong>显示时映射</strong></p>
<p>呈现引擎仅允许 GPU 虚拟访问。</p></td>
</tr>
</tbody>
</table>

 

 


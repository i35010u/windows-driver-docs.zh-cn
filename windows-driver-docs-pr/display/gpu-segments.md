---
title: GPU 段
description: 在设备驱动程序接口 (DDI) 中，分段模型是抽象出来的图形处理单元 (GPU) 访问的物理内存。
ms.assetid: E6CAD808-73C0-48AB-BF95-76911D5C104A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3404fd22077396dfaa607fc15ba95adf3e8439a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379957"
---
# <a name="gpu-segments"></a>GPU 段


在设备驱动程序接口 (DDI) 中，分段模型是抽象出来的图形处理单元 (GPU) 访问的物理内存。 内核模式驱动程序通过枚举的段，然后由视频内存管理器管理的一组表示 GPU 可用的物理内存资源。

有三种类型的 Windows 显示器驱动程序模型 (WDDM) v2 中的段：

<span id="Memory_Segment"></span><span id="memory_segment"></span><span id="MEMORY_SEGMENT"></span>内存段  
一个内存段表示专用于 GPU 的内存。 这可能是分立的 GPU 上的 vram 能够或集成的 GPU 上的固件/驱动程序保留的内存。 可以有多个枚举的内存段。

新 WDDM v2 中的内存段被托管作为物理页大小是 4 KB 或 64 KB 的池。 图面上的数据复制到和移出内存段中使用*填充*/*传输*/*放弃*/ *FillVirtuall*/*TransferVirtual*分页操作。

CPU 可能会访问在两种方式之一中的内存段的内容。 首先，内存段可能会看到 CPU，在其中用例的视频内存管理器只需 CPU 虚拟地址直接映射到段内分配的物理地址空间中。 新 WDDM v2 中的视频内存管理器还支持通过可编程与该时间段关联的 CPU 主机 aperture 访问内存段的内容。

<span id="Aperture__Segment"></span><span id="aperture__segment"></span><span id="APERTURE__SEGMENT"></span>Aperture 段  
Aperture 段是全局的页表用于使不连续的系统内存页的显示从 GPU 引擎的角度来看连续。

WDDM v2 中的单个 aperture 段必须被报告。

<span id="System_Memory_Segment"></span><span id="system_memory_segment"></span><span id="SYSTEM_MEMORY_SEGMENT"></span>系统内存段  
系统内存段是隐式表示系统内存引用 （即来宾物理地址）。 内核模式驱动程序不直接枚举的系统内存段。 它的视频内存管理器隐式枚举并获取分配给始终`SegmentId==0`。 若要将分配放在系统内存段，内核模式驱动程序需要使用 aperture 段 id。

## <a name="span-idphysicalmemoryreferencespanspan-idphysicalmemoryreferencespanspan-idphysicalmemoryreferencespanphysical-memory-reference"></a><span id="Physical_memory_reference"></span><span id="physical_memory_reference"></span><span id="PHYSICAL_MEMORY_REFERENCE"></span>物理内存引用


DDI 中的物理内存的引用始终采用段 ID 段偏移量对的形式。

## <a name="span-idaccessingallocationsbyphysicaladdressspanspan-idaccessingallocationsbyphysicaladdressspanspan-idaccessingallocationsbyphysicaladdressspanaccessing-allocations-by-physical-address"></a><span id="Accessing_allocations_by_physical_address"></span><span id="accessing_allocations_by_physical_address"></span><span id="ACCESSING_ALLOCATIONS_BY_PHYSICAL_ADDRESS"></span>访问分配的物理地址


不支持 GPU 虚拟寻址的 GPU 引擎需要访问通过其物理地址的分配。 这会产生上如何分配获取已分配资源的段中的含义。 物理引用意味着分配必须连续内存段中分配或 aperture 段中占据连续范围。

若要避免不必要且成本高昂的连续分配，内核模式驱动程序必须显式确定需要用来访问以物理方式呈现引擎，通过设置新的分配[ **DXGK\_ALLOCATIONINFOFLAGS2**](https://docs.microsoft.com/windows-hardware/drivers/display/dxgk-allocationinfoflags2)::**AccessedPhysically**期间分配的标志。

此类分配将映射到 aperture 段时驻留在系统内存中。 分配将连续时驻留在一个内存段中。 可以通过在引擎，在物理寻址模式下运行的分配列表引用分配，这种方法，创建。

分配，后者不具有此标记集时，将分配为一组的内存段中的页面或一组在系统内存中任何一个都通过 GPU 虚拟地址进行访问的页面。 这种方法创建的分配不能引用通过分配列表。 通过这种方式引用分配任何命令缓冲区提交将被拒绝。

主表面被理解为显示控制器以物理方式访问和将内存段中连续分配或映射到 aperture 段时显示。 内核模式驱动程序只应设置**AccessedPhysically**标志时呈现引擎将以物理方式访问分配。 分配将映射到 aperture 时主图面上隐式的物理访问权限与显式标记之间的差别。 当**AccessedPhysically**设置标志，它是常驻时分配将映射到 aperture。 主应用层不具有此标记集，仅在显示时将映射到 aperture。 若要删除光圈段上的压力本帮助通常有仅几个主要面主动显示，尽管现有并呈现给可能是数非常大 (即全部*FlipEx*交换链创建为中的主要和潜在可显示图面*dFlip*/*iFlip*方案)。

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
<td align="left">AccessedPhysically==0</td>
<td align="left">AccessedPhysically==1</td>
<td align="left">主 & & AccessedPhysically = = 0</td>
</tr>
<tr class="even">
<td align="left">内存段</td>
<td align="left"><p><strong>组页面</strong></p>
<p>允许 GPU 虚拟访问。</p></td>
<td align="left"><p><strong>连续</strong></p>
<p>允许 GPU 物理访问</p></td>
<td align="left"><p><strong>连续</strong></p>
<p>GPU 虚拟访问所允许的呈现引擎。</p></td>
</tr>
<tr class="odd">
<td align="left">Aperture 段</td>
<td align="left"><p><strong>未映射</strong></p>
<p>系统内存页，仅由 GPU 页表，不适用于 aperture 段映射。</p>
<p>允许 GPU 虚拟访问。</p></td>
<td align="left"><p><strong>当驻留时，映射</strong></p>
<p>允许 GPU 物理访问。</p></td>
<td align="left"><p><strong>映射时显示</strong></p>
<p>GPU 虚拟访问所允许的呈现引擎。</p></td>
</tr>
</tbody>
</table>

 

 

 






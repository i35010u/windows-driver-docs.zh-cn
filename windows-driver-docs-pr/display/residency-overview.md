---
title: 驻留概述
description: 驻留概述
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c216246900696134212fac993d129c46d8371026
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799609"
---
# <a name="residency-overview"></a>驻留概述


## <a name="span-idoverviewspanspan-idoverviewspanspan-idoverviewspanoverview"></a><span id="Overview"></span><span id="overview"></span><span id="OVERVIEW"></span>叙述


目前，用户模式驱动程序生成分配和修补程序位置列表信息以及它生成的每个命令缓冲区。 视频内存管理器使用此信息两个用途：

-   "分配列表" 和 "修补程序位置" 列表用于在将命令缓冲区提交给图形处理单元（ (GPU) 引擎）之前，使用实际段地址来修补命令缓冲区。 Windows 显示驱动程序模型 (WDDM) v2 的 GPU 虚拟地址支持不再需要此修补程序。
-   "分配列表" 和 "修补程序位置" 列表由视频内存管理器用来控制分配的驻留。 视频内存管理器可确保在命令缓冲区发送到特定引擎的执行之前，命令缓冲区引用的任何分配都处于驻留。

引入新的常驻模型后，仍会将驻留在设备上的显式列表中，而不是按命令缓冲区列表移动。 视频内存管理器将确保特定设备派驻要求列表上的所有分配在计划执行的任何上下文之前处于驻留。

要管理常驻，用户模式驱动程序将可以访问两个新的设备驱动程序接口 (DDIs) 、 [*MakeResident*](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_makeresidentcb) 和 [*逐出*](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_evictcb)，还需要实现新的 [*TrimResidency*](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_trimresidencyset) 回调。 *MakeResident* 会将一个或多个分配添加到设备派驻需求列表。 *逐出* 将从该列表中删除一个或多个分配。 当视频内存管理器需要用户模式驱动程序来降低其驻留要求时，将调用 *TrimResidency* 回调。

[*MakeResident*](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_makeresidentcb) 和 [*逐出*](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_evictcb) 还已更新为保留内部引用计数，这意味着对 *MakeResident* 的多个调用将需要相同数量的 *逐出* 调用来实际逐出分配。

在新的常驻模型下，按命令缓冲分配和修补程序位置列表的速度缓慢。尽管这些列表在某些情况下会存在，但他们将不再拥有对派驻的任何控制。

**重要提示**  WDDM v2 中的常驻是由设备派驻要求列表专门控制的。 对于 GPU 和每个 API 的所有引擎都是如此。

 

## <a name="span-idphasing_out_allocation_and_patch_location_listspanspan-idphasing_out_allocation_and_patch_location_listspanspan-idphasing_out_allocation_and_patch_location_listspanphasing-out-allocation-and-patch-location-list"></a><span id="Phasing_out_allocation_and_patch_location_list"></span><span id="phasing_out_allocation_and_patch_location_list"></span><span id="PHASING_OUT_ALLOCATION_AND_PATCH_LOCATION_LIST"></span>逐步取消 out 分配和修补程序位置列表


由于引入了新的常驻模型，因此，"分配" 和 "修补程序位置" 列表的角色会显著降低，并将在引入硬件辅助计划的同时完全消失。

在基于数据包的计划模型下，分配列表将继续存在，如下所示：

-   对于不支持 GPU 虚拟寻址的引擎，"分配列表" 和 "修补程序位置" 列表将继续存在，但是，它们将仅用于修补目的，不再对常驻有任何控制。 "分配列表" 和 "修补程序位置" 列表将在各种常见的 DDIs 中同时提供给用户模式驱动程序和内核模式驱动程序，但对非居民分配的任何引用都将导致 GPU 计划程序拒绝提交，并使设备出错 () 丢失。 此操作模式被视为旧模式，我们希望所有 GPU 引擎在未来的硬件版本中获得对 GPU 虚拟寻址的支持。 预期此操作模式将在 WDDM 的未来版本中删除。
-   对于支持 GPU 虚拟寻址的引擎，新的上下文创建标志 (**DXGK CONTEXTINFO 不) \_ \_ \_ \_ 需要修补** ，因为添加了，以指示特定上下文不需要任何修补。 如果指定此标志，则将不会分配任何修补程序位置列表，并且仅分配一个非常小的分配列表 (16 项) 将被分配。 分配列表将用于跟踪对主要表面的写入引用，而不是任何其他目的。 GPU 计划程序需要知道何时向主表面写入特定的命令缓冲区，以便能够正确地同步该缓冲区的执行情况，使其与主表面可能发生反向同步。

同样 *，当前在内核模式驱动程序* 的路径中使用了分配列表来向驱动程序传递有关 *当前* 操作的源和目标的信息。 在这种情况下，分配列表将继续存在以传递参数，但分配列表不会用于驻留。 在需要修补 *当前* 分配列表的 gpu 上，将包含如下所述的修补程序信息，如果任何资源在排队到计划程序的时间与计划程序在 GPU 上的执行时间之间来回移动，则会在计划 *之前对其* 重新修补。

下表总结了 WDDM v2 驱动程序应在各种用户模式驱动程序和内核模式驱动程序 DDIs 中接收分配和修补程序位置列表的时间。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">GPU 引擎</th>
<th align="left">分配列表？</th>
<th align="left">修补程序位置列表？</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">无 GPU 虚拟地址支持 (需要修补、默认) </td>
<td align="left"><p>是，完整大小，但仅用于修补目的。</p>
对不是常驻分配的任何引用都将导致提交设备处于错误 (丢失) 和计划程序拒绝提交。</td>
<td align="left">是，完整大小。</td>
</tr>
<tr class="even">
<td align="left">GPU 虚拟地址支持 (设置 <strong>DXGK_CONTEXTINFO_NO_PATCHING_REQUIRED</strong> 标志) </td>
<td align="left"><p>是，16个条目。</p>
引用通过命令缓冲区写入的主要曲面（如果有）。 供 GPU 计划程序用于在显示控制器上发生 lip 的同步。 主要表面必须已在设备派驻要求列表上，否则将拒绝该引用。</td>
<td align="left">否</td>
</tr>
<tr class="odd">
<td align="left">GPU 虚拟地址支持 + 硬件计划</td>
<td align="left">否</td>
<td align="left">否</td>
</tr>
</tbody>
</table>

 

 


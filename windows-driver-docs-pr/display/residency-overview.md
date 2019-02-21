---
title: 驻留概述
description: 驻留概述
ms.assetid: E610C2B8-354C-4DF5-8B25-6472A9313B15
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ca2d31c9921b88a1c991d6fc22d984d9f22f71a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520575"
---
# <a name="residency-overview"></a>驻留概述


## <a name="span-idoverviewspanspan-idoverviewspanspan-idoverviewspanoverview"></a><span id="Overview"></span><span id="overview"></span><span id="OVERVIEW"></span>概述


立即分配和修补程序位置列表信息以及每个命令缓冲区生成，将生成用户模式驱动程序。 此信息使用视频内存管理器有两个用途：

-   分配列表和修补程序位置列表用于修补与实际段地址的命令缓冲区，然后将它们提交到图形处理单元 (GPU) 引擎。 Windows 显示器驱动程序模型 (WDDM) v2 中的 GPU 虚拟地址支持不再需要此修补。
-   分配的控件驻留到的视频内存管理器使用的分配列表和修补程序位置列表。 视频内存管理器可确保，任何引用的命令缓冲区的分配之前做出的常驻命令缓冲区发送到的特定引擎执行。

随着新驻留模型的推出，驻留将被移至的显式列表而不是每个命令缓冲区列表在设备上。 视频内存管理器将确保确保之前计划执行的任何上下文属于该设备都是驻留在特定设备驻留要求列表上的所有分配。

若要管理驻留，用户模式驱动程序将有权访问两个新设备驱动程序接口 (DDIs) [ *MakeResident* ](https://msdn.microsoft.com/library/windows/hardware/dn906357)并[*逐出*](https://msdn.microsoft.com/library/windows/hardware/dn906355)，同时也需要实现一个新[ *TrimResidency* ](https://msdn.microsoft.com/library/windows/hardware/dn906364)回调。 *MakeResident*将添加一个或多个分配到的设备驻留要求列表。 *逐出*将从该列表中删除一个更多分配。 *TrimResidency*视频内存管理器将调用回调，当它需要用户模式驱动程序，以减少其驻留要求。

[*MakeResident* ](https://msdn.microsoft.com/library/windows/hardware/dn906357)并[*逐出*](https://msdn.microsoft.com/library/windows/hardware/dn906355)也已更新保留的内部引用计数，这意味着多次调用*MakeResident*将需要相同数目的*逐出*调用实际上中收回分配。

在新驻留模式下，每个命令缓冲区分配和修补程序位置列表是缓慢逐步淘汰。虽然这些列表将存在在某些情况下，它们将不再具有对驻留的任何控制。

**重要**  驻留 WDDM v2 中的以独占方式受设备驻留要求列表。 这适用于所有引擎的 GPU 和每个 api。

 

## <a name="span-idphasingoutallocationandpatchlocationlistspanspan-idphasingoutallocationandpatchlocationlistspanspan-idphasingoutallocationandpatchlocationlistspanphasing-out-allocation-and-patch-location-list"></a><span id="Phasing_out_allocation_and_patch_location_list"></span><span id="phasing_out_allocation_and_patch_location_list"></span><span id="PHASING_OUT_ALLOCATION_AND_PATCH_LOCATION_LIST"></span>逐步淘汰分配和修补程序位置列表


分配和修补程序的位置列表的角色将获得大大减少了与新驻留模型的简介，并将消失完全随着硬件辅助计划。

在数据包根据计划模式下，分配列表将继续存在，如下所示：

-   对于不支持 GPU 虚拟寻址的引擎，分配列表和修补程序位置列表中将继续存在，但是，它们将用于完全修补目的，将不再有任何控制驻留。 分配列表和修补程序位置列表中将提供给用户模式驱动程序和内核模式驱动程序中各种常用 DDIs，但不是常驻的分配的任何引用会导致拒绝的提交并将设备的 GPU 计划程序错误 （丢失）。 此操作模式被视为旧版，我们期望所有 GPU 引擎来获取对 GPU 支持虚拟寻址将来硬件版本。 预计，这种模式的操作将删除在将来的 WDDM 的版本。
-   为引擎支持 GPU 虚拟寻址，一个新的上下文创建标记 (**DXGK\_CONTEXTINFO\_否\_修补\_REQUIRED**) 添加，以指示特定上下文不需要任何修补。 当指定此标志时，将分配给任何修补程序位置列表和将分配给仅非常小的分配列表 （16 个条目）。 将使用分配列表来跟踪写入引用到主表面和不会用于其他目的。 GPU 计划程序需要知道当特定命令缓冲区，以便它可以正确同步方面可能会发生到主面翻转该缓冲区执行正在写入到主图面。

同样，在内核模式驱动程序中使用分配列表*存在*路径现在将信息传递给驱动程序有关的源和目标*存在*操作。 在此上下文中分配列表将继续存在，将围绕参数传递，但是，分配列表将不用于驻留。 需要修补程序的 Gpu 上*存在*分配列表将包含像今天一样的修补程序前信息和*存在*数据包之前，将重新修补安排如果的任何资源中移动它们排队到计划程序的时间和执行计划的时间之间的内存在 GPU 上。

下表总结了当 WDDM v2 驱动程序应该会收到不同的用户模式驱动程序和内核模式驱动程序 DDIs 中的分配和修补程序位置列表。

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
<td align="left">没有 GPU 虚拟地址支持 （需要修补，默认值）</td>
<td align="left"><p>是的完全大小，但单纯使用修补目的。</p>
对不是常驻的分配的任何引用将导致提交设备置于错误 （丢失） 和计划程序被拒绝的提交。</td>
<td align="left">是，完整的大小。</td>
</tr>
<tr class="even">
<td align="left">GPU 虚拟地址支持 (<strong>DXGK_CONTEXTINFO_NO_PATCHING_REQUIRED</strong>标志设置)</td>
<td align="left"><p>是的 16 个条目。</p>
引用主面上，如果任何由命令缓冲区写入。 由 GPU 计划程序同步与显示控制器上发生的 lip。 主图面上设备驻留要求列表必须已经包含或引用将被拒绝。</td>
<td align="left">否</td>
</tr>
<tr class="odd">
<td align="left">GPU 虚拟地址支持 + 硬件计划</td>
<td align="left">否</td>
<td align="left">否</td>
</tr>
</tbody>
</table>

 

 

 






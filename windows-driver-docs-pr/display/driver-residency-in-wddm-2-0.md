---
title: WDDM 2.0 中的驱动程序驻留
description: 本部分提供有关 Windows 显示驱动程序模型的驱动程序驻留更改的详细信息 (WDDM) 2.0。 从 Windows 10 开始可以使用所述功能。
ms.assetid: 9BD0138A-E957-4675-8E08-2750825A5C87
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa94901a52e03f5880be906625b90eebd2975411
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90103790"
---
# <a name="driver-residency-in-wddm-20"></a>WDDM 2.0 中的驱动程序驻留


本部分提供有关 Windows 显示驱动程序模型的驱动程序驻留更改的详细信息 (WDDM) 2.0。 从 Windows 10 开始可以使用所述功能。

## <a name="span-idin_this_sectionspanin-this-section"></a><span id="in_this_section"></span>本部分中的内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主题</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="residency-overview.md" data-raw-source="[Residency overview](residency-overview.md)">驻留概述</a></p></td>
<td align="left"><p>引入新的常驻模型后，仍会将驻留在设备上的显式列表中，而不是按命令缓冲区列表移动。 视频内存管理器将确保特定设备派驻要求列表上的所有分配在计划执行的任何上下文之前处于驻留。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="allocation-usage-tracking.md" data-raw-source="[Allocation usage tracking](allocation-usage-tracking.md)">分配用法跟踪</a></p></td>
<td align="left"><p>删除分配列表后，视频内存管理器不再能够查看特定命令缓冲区中所引用的分配。 因此，视频内存管理器不再位于跟踪分配使用情况和处理相关同步的位置。 此责任现在会落在用户模式驱动程序中。 特别是，用户模式驱动程序必须处理与对分配的直接 CPU 访问以及重命名相关的同步。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="offer-and-reclaim-changes.md" data-raw-source="[Offer and reclaim changes](offer-and-reclaim-changes.md)">供应和回收更改</a></p></td>
<td align="left"><p>对于 WDDM v2， <em>提供</em> 和 <em>回收</em> 方面的要求非常宽松。 用户模式驱动程序不再需要在内部分配中使用产品/服务和回收。 空闲/挂起的应用程序将使用 Microsoft DirectX 11.1 中引入的 <strong>剪裁</strong>API 来消除驱动程序内部资源。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="access-to-non-resident-allocation.md" data-raw-source="[Access to non-resident allocation](access-to-non-resident-allocation.md)">访问非驻留分配</a></p></td>
<td align="left"><p>图形处理单元 (GPU) 访问非常驻分配是非法的，将导致为生成错误的应用程序删除设备。</p>
<p>处理此类无效访问的两种不同模型依赖于出错引擎是否支持 GPU 虚拟寻址：</p>
<ul>
<li>对于不支持 GPU 虚拟寻址的引擎，并使用 "分配" 和 "修补程序位置" 列表修补内存引用，当用户模式驱动程序提交的分配列表引用了不在设备上的分配时，将发生无效的访问 (即，用户模式驱动程序没有在该分配) 上调用 <a href="/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_makeresidentcb" data-raw-source="[&lt;em&gt;MakeResidentCb&lt;/em&gt;](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_makeresidentcb)"><em>MakeResidentCb</em></a> 。 出现这种情况时，图形内核会将有问题的上下文/设备置于错误中。</li>
<li>对于支持 GPU 虚拟寻址但访问无效的 GPU 虚拟地址的引擎，因为在虚拟地址之后没有分配，或者没有有效的分配，但尚未进行驻留，所以 GPU 应以中断的形式引发不可恢复的页错误。 出现页错误中断时，内核模式驱动程序需要通过新的页错误通知将错误转发到图形内核。 收到此通知后，图形内核会在发生错误的引擎上启动引擎重置，并导致错误的上下文/设备出错。 如果引擎重置失败，则图形内核会将错误提升为完整的适配器范围超时检测和恢复 (TDR) 。</li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="process-residency-budgets.md" data-raw-source="[Process residency budgets](process-residency-budgets.md)">进程驻留预算</a></p></td>
<td align="left"><p>在 WDDM v2 中，将为进程分配预算，使其可以保持驻留的内存量。 此预算可能会随时间推移而变化，但通常仅当系统处于内存压力时才会受到影响。 在 Microsoft Direct3D 12 之前，将按用户模式驱动程序以<em>剪裁</em>通知形式处理预算，并使用 STATUS_NO_MEMORY <em>MakeResident</em>失败。 <strong>STATUS_NO_MEMORY</strong> <em>TrimToBudget</em> Notification、<a href="/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_evictcb" data-raw-source="[&lt;em&gt;Evict&lt;/em&gt;](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_evictcb)"><em>逐出</em></a>和 failed <a href="/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_makeresidentcb" data-raw-source="[&lt;em&gt;MakeResident&lt;/em&gt;](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_makeresidentcb)"><em>MakeResident</em></a>调用都以整数 NumBytesToTrim 值的形式返回最新的预算，这是一个整数<strong>NumBytesToTrim</strong>值，它指示需要进行剪裁以适应新预算的量。</p></td>
</tr>
</tbody>
</table>

 


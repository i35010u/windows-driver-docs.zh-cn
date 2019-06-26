---
title: WDDM 2.0 中的驱动程序驻留
description: 本部分提供有关驱动程序的详细信息驻留更改为 Windows 显示器驱动程序模型 (WDDM) 2.0。 可从 Windows 10 开始所述的功能。
ms.assetid: 9BD0138A-E957-4675-8E08-2750825A5C87
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e3906aad8c629904a7fb35f67304dc0b34fc2174
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381074"
---
# <a name="driver-residency-in-wddm-20"></a>WDDM 2.0 中的驱动程序驻留


本部分提供有关驱动程序的详细信息驻留更改为 Windows 显示器驱动程序模型 (WDDM) 2.0。 可从 Windows 10 开始所述的功能。

## <a name="span-idinthissectionspanin-this-section"></a><span id="in_this_section"></span>本部分中的内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主题</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="residency-overview.md" data-raw-source="[Residency overview](residency-overview.md)">驻留概述</a></p></td>
<td align="left"><p>随着新驻留模型的推出，驻留将被移至的显式列表而不是每个命令缓冲区列表在设备上。 视频内存管理器将确保确保之前计划执行的任何上下文属于该设备都是驻留在特定设备驻留要求列表上的所有分配。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="allocation-usage-tracking.md" data-raw-source="[Allocation usage tracking](allocation-usage-tracking.md)">分配使用情况跟踪</a></p></td>
<td align="left"><p>分配列表中消失，使用的视频内存管理器不再具有到所引用的特定命令缓冲区中分配的可见性。 因此，视频内存管理器将不再在位置来跟踪分配使用情况并处理相关的同步。 此职责现在将回退到用户模式驱动程序验证。 具体而言，用户模式驱动程序将需要处理同步相对于直接 CPU 访问权限分配以及重命名。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="offer-and-reclaim-changes.md" data-raw-source="[Offer and reclaim changes](offer-and-reclaim-changes.md)">提供和回收更改</a></p></td>
<td align="left"><p>对于 WDDM v2，规定<em>产品/服务</em>和<em>回收</em>正在放宽了。 用户模式驱动程序不再需要使用产品/服务，并在内部分配上回收。 空闲/已挂起应用程序将使用的驱动程序内部资源消除<strong>剪裁</strong>Microsoft DirectX 11.1 中引入的 API。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="access-to-non-resident-allocation.md" data-raw-source="[Access to non-resident allocation](access-to-non-resident-allocation.md)">对非驻留分配的访问</a></p></td>
<td align="left"><p>图形处理单元 (GPU) 访问不是常驻分配是非法的并会导致生成错误的应用程序中删除的设备。</p>
<p>有两个不同的模型的处理取决于是否出错的引擎支持 GPU 虚拟寻址或不访问此类无效：</p>
<ul>
<li>对于不支持 GPU 虚拟寻址，并使用的分配和修补程序修补程序内存引用到的位置列表的引擎，无效的访问发生在用户模式驱动程序提交的分配列表引用分配，这不是驻留在设备 (即称为用户模式驱动程序尚未<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_makeresidentcb" data-raw-source="[&lt;em&gt;MakeResidentCb&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_makeresidentcb)"> <em>MakeResidentCb</em> </a>在该分配)。 此操作时，图形内核将有故障的上下文/设备放入错误。</li>
<li>对于执行支持 GPU 虚拟寻址，但访问 GPU 虚拟地址是无效的引擎，或者因为后面的虚拟地址未分配或没有有效分配但尚未进行其常驻，GPU 应引发形式的中断发生了不可恢复的页面错误。 当发生页面故障中断时，内核模式驱动程序需要转发到图形内核通过新的页错误通知错误。 收到此通知时，图形内核启动引擎重置上出错的引擎，并将有故障的上下文/设备放入错误。 如果引擎重置失败，图形内核将升级到完整适配器宽超时检测和恢复 (TDR) 错误。</li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="process-residency-budgets.md" data-raw-source="[Process residency budgets](process-residency-budgets.md)">进程驻留预算</a></p></td>
<td align="left"><p>WDDM v2 中的进程将分配的内存量保持常驻的预算。 此预算随着时间推移，可以更改，但通常仅施加时系统处于内存压力下。 在 Microsoft Direct3D 12 中之前, 预算处理的窗体中的用户模式驱动程序通过<em>剪裁</em>通知并<em>MakeResident</em>失败<strong>STATUS_NO_MEMORY</strong>。 <em>TrimToBudget</em>通知<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_evictcb" data-raw-source="[&lt;em&gt;Evict&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_evictcb)"><em>逐出</em></a>，和失败<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_makeresidentcb" data-raw-source="[&lt;em&gt;MakeResident&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_makeresidentcb)"> <em>MakeResident</em> </a>所有调用将都返回在最新的预算窗体的一个整数<strong>NumBytesToTrim</strong>值，该值指示多大需要进行剪裁以适应新的预算。</p></td>
</tr>
</tbody>
</table>

 

 

 






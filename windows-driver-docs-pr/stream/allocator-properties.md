---
title: 分配器属性
description: 分配器属性
ms.assetid: 851bc3d8-46f6-46d0-87a8-81de2536492a
keywords:
- 分配器属性 WDK 视频捕获
- PROPSETID_ALLOCATOR_CONTROL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e476a82f0343f38668c4b51fe26e2badaf46c0a4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384830"
---
# <a name="allocator-properties"></a>分配器属性


[PROPSETID\_ALLOCATOR\_控制](https://msdn.microsoft.com/library/windows/hardware/ff567792)属性集包含与控制的分配和操作的视频端口图面相关的属性。 用户模式下的筛选器，例如覆盖 Mixer 中，使用 PROPSETID\_分配器\_控件。 下表描述了属性属于 PROPSETID\_分配器\_控件属性集。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>PROPSETID_ALLOCATOR_CONTROL KS 属性</th>
<th>属性说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564276" data-raw-source="[&lt;strong&gt;KSPROPERTY_ALLOCATOR_CONTROL_HONOR_COUNT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564276)"><strong>KSPROPERTY_ALLOCATOR_CONTROL_HONOR_COUNT</strong></a></p></td>
<td><p>控制如何筛选器确定要分配的视频端口覆盖图面数。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564278" data-raw-source="[&lt;strong&gt;KSPROPERTY_ALLOCATOR_CONTROL_SURFACE_SIZE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564278)"><strong>KSPROPERTY_ALLOCATOR_CONTROL_SURFACE_SIZE</strong></a></p></td>
<td><p>控件的维度的视频端口覆盖面。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564267" data-raw-source="[&lt;strong&gt;KSPROPERTY_ALLOCATOR_CONTROL_CAPTURE_CAPS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564267)"><strong>KSPROPERTY_ALLOCATOR_CONTROL_CAPTURE_CAPS</strong></a></p></td>
<td><p>介绍的视频端口的捕获功能。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564271" data-raw-source="[&lt;strong&gt;KSPROPERTY_ALLOCATOR_CONTROL_CAPTURE_INTERLEAVE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564271)"><strong>KSPROPERTY_ALLOCATOR_CONTROL_CAPTURE_INTERLEAVE</strong></a></p></td>
<td><p>返回在视频端口支持交错捕获。</p></td>
</tr>
</tbody>
</table>

 

 

 





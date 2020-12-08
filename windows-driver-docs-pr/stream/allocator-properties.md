---
title: 分配器属性
description: 分配器属性
keywords:
- 分配器属性 WDK 视频捕获
- PROPSETID_ALLOCATOR_CONTROL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e2501d958d4c43ee56fd7df2d05a6ec2f031cbb1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840591"
---
# <a name="allocator-properties"></a>分配器属性


[PROPSETID \_ 分配器 \_ 控件](./propsetid-allocator-control.md)属性集包含与控制视频端口图面的分配和操作相关的属性。 用户模式筛选器，如覆盖混音器，使用 PROPSETID \_ 分配器 \_ 控件。 下表描述了属于 PROPSETID \_ 分配器 \_ 控件属性集的属性。

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
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-allocator-control-honor-count" data-raw-source="[&lt;strong&gt;KSPROPERTY_ALLOCATOR_CONTROL_HONOR_COUNT&lt;/strong&gt;](./ksproperty-allocator-control-honor-count.md)"><strong>KSPROPERTY_ALLOCATOR_CONTROL_HONOR_COUNT</strong></a></p></td>
<td><p>控制筛选器如何确定要分配的视频端口覆盖面的数目。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-allocator-control-surface-size" data-raw-source="[&lt;strong&gt;KSPROPERTY_ALLOCATOR_CONTROL_SURFACE_SIZE&lt;/strong&gt;](./ksproperty-allocator-control-surface-size.md)"><strong>KSPROPERTY_ALLOCATOR_CONTROL_SURFACE_SIZE</strong></a></p></td>
<td><p>控制视频端口重叠图面的尺寸。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-allocator-control-capture-caps" data-raw-source="[&lt;strong&gt;KSPROPERTY_ALLOCATOR_CONTROL_CAPTURE_CAPS&lt;/strong&gt;](./ksproperty-allocator-control-capture-caps.md)"><strong>KSPROPERTY_ALLOCATOR_CONTROL_CAPTURE_CAPS</strong></a></p></td>
<td><p>描述视频端口的捕获功能。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-allocator-control-capture-interleave" data-raw-source="[&lt;strong&gt;KSPROPERTY_ALLOCATOR_CONTROL_CAPTURE_INTERLEAVE&lt;/strong&gt;](./ksproperty-allocator-control-capture-interleave.md)"><strong>KSPROPERTY_ALLOCATOR_CONTROL_CAPTURE_INTERLEAVE</strong></a></p></td>
<td><p>如果视频端口支持交错捕获，则返回。</p></td>
</tr>
</tbody>
</table>

 


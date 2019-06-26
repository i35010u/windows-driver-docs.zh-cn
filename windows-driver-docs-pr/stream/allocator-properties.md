---
title: 分配器属性
description: 分配器属性
ms.assetid: 851bc3d8-46f6-46d0-87a8-81de2536492a
keywords:
- 分配器属性 WDK 视频捕获
- PROPSETID_ALLOCATOR_CONTROL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a3f5053e9951aca7b0d5d09e1b4529615d9d2ba
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386774"
---
# <a name="allocator-properties"></a>分配器属性


[PROPSETID\_ALLOCATOR\_控制](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-allocator-control)属性集包含与控制的分配和操作的视频端口图面相关的属性。 用户模式下的筛选器，例如覆盖 Mixer 中，使用 PROPSETID\_分配器\_控件。 下表描述了属性属于 PROPSETID\_分配器\_控件属性集。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-allocator-control-honor-count" data-raw-source="[&lt;strong&gt;KSPROPERTY_ALLOCATOR_CONTROL_HONOR_COUNT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-allocator-control-honor-count)"><strong>KSPROPERTY_ALLOCATOR_CONTROL_HONOR_COUNT</strong></a></p></td>
<td><p>控制如何筛选器确定要分配的视频端口覆盖图面数。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-allocator-control-surface-size" data-raw-source="[&lt;strong&gt;KSPROPERTY_ALLOCATOR_CONTROL_SURFACE_SIZE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-allocator-control-surface-size)"><strong>KSPROPERTY_ALLOCATOR_CONTROL_SURFACE_SIZE</strong></a></p></td>
<td><p>控件的维度的视频端口覆盖面。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-allocator-control-capture-caps" data-raw-source="[&lt;strong&gt;KSPROPERTY_ALLOCATOR_CONTROL_CAPTURE_CAPS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-allocator-control-capture-caps)"><strong>KSPROPERTY_ALLOCATOR_CONTROL_CAPTURE_CAPS</strong></a></p></td>
<td><p>介绍的视频端口的捕获功能。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-allocator-control-capture-interleave" data-raw-source="[&lt;strong&gt;KSPROPERTY_ALLOCATOR_CONTROL_CAPTURE_INTERLEAVE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-allocator-control-capture-interleave)"><strong>KSPROPERTY_ALLOCATOR_CONTROL_CAPTURE_INTERLEAVE</strong></a></p></td>
<td><p>返回在视频端口支持交错捕获。</p></td>
</tr>
</tbody>
</table>

 

 

 





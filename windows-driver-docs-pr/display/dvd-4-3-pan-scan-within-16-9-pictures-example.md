---
title: DVD 4 3 16 9 内的平移扫描图片示例
description: DVD 4 3 16 9 内的平移扫描图片示例
ms.assetid: f00489e7-809d-4a5b-87c8-b2421bd6ca93
keywords:
- alpha 混合组合 WDK DirectX VA，DVD 4 3 平移-扫描示例
- 混合型的图片 WDK DirectX VA，DVD 4 3 平移扫描示例
- DVD 4 3 平移扫描示例 WDK DirectX VA
- 4 3 平移扫描示例 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 77d579ad68f13b44fae6f450048ecaa5c6111e17
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567713"
---
# <a name="dvd-43-pan-scan-within-169-pictures-example"></a>16:9 画面中的 DVD 4:3 平移扫描示例


## <span id="ddk_dvd_4_3_pan_scan_within_16_9_pictures_example_gg"></span><span id="DDK_DVD_4_3_PAN_SCAN_WITHIN_16_9_PICTURES_EXAMPLE_GG"></span>


在为 16:9 图片中 4:3 平移扫描 DVD 使用 mpeg-2，平移扫描 mpeg-2 变量不能违反中指定的限制[ **DXVA\_BlendCombination** ](https://msdn.microsoft.com/library/windows/hardware/ff563120)结构。 这些变量也必须维护所需的 DVD 规范的以下限制。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">MPEG 2 变量</th>
<th align="left">值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><em>horizontal_size</em></p></td>
<td align="left"><p>720 或 704</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>vertical_size</em></p></td>
<td align="left"><p>480 或 576</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>display_horizontal_size</em></p></td>
<td align="left"><p>540</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>display_vertical_size</em></p></td>
<td align="left"><p><em>vertical_size</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>frame_centre_vertical_offset</em></p></td>
<td align="left"><p>零</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>frame_centre_horizontal_offset</em></p></td>
<td align="left"><p>小于或等于 1440年<em>horizontal_size</em> = 720</p>
<p>小于或等于为 1312年<em>horizontal_size</em> = 704</p></td>
</tr>
</tbody>
</table>

 

中所述表述[mpeg-2 平移扫描示例](mpeg-2-pan-scan-example.md)然后可将应用直接在这种情况下。

 

 






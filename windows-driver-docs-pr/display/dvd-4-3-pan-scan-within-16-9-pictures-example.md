---
title: 4 3 16 9 图片示例中的 DVD 平移扫描
description: 4 3 16 9 图片示例中的 DVD 平移扫描
ms.assetid: f00489e7-809d-4a5b-87c8-b2421bd6ca93
keywords:
- alpha-blend 组合 WDK DirectX VA，DVD 4 3 平移扫描示例
- 混合图片 WDK DirectX VA，DVD 4 3 平移扫描示例
- DVD 4 3 平移扫描示例 WDK DirectX VA
- 4 3 平移扫描示例 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 754224a5cf1fddb52e42412a8f8647ae5611014b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838979"
---
# <a name="dvd-43-pan-scan-within-169-pictures-example"></a>16:9 画面中的 DVD 4:3 平移扫描示例


## <span id="ddk_dvd_4_3_pan_scan_within_16_9_pictures_example_gg"></span><span id="DDK_DVD_4_3_PAN_SCAN_WITHIN_16_9_PICTURES_EXAMPLE_GG"></span>


在16:9 图片内，使用 MPEG-2 用于4:3 的平移扫描时，平移扫描 MPEG-2 变量不得违反[**DXVA\_BlendCombination**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_blendcombination)结构中指定的限制。 这些变量还必须保持 DVD 规范所需的以下限制。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">MPEG-2 变量</th>
<th align="left">Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><em>horizontal_size</em></p></td>
<td align="left"><p>720或704</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>vertical_size</em></p></td>
<td align="left"><p>480或576</p></td>
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
<td align="left"><p>无</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>frame_centre_horizontal_offset</em></p></td>
<td align="left"><p>对于<em>horizontal_size</em> = 720，小于或等于1440</p>
<p>对于<em>horizontal_size</em> = 704，小于或等于1312</p></td>
</tr>
</tbody>
</table>

 

然后，在这种情况下，可以直接应用[Mpeg-2 平移扫描示例](mpeg-2-pan-scan-example.md)中所述的表述。

 

 






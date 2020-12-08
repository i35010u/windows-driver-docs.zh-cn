---
title: 分辨率功能的选项属性
description: 分辨率功能的选项属性
keywords:
- 解决功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a5fcf7afedc287fb5788261638a1eee19003e027
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807705"
---
# <a name="option-attributes-for-the-resolution-feature"></a>分辨率功能的选项属性





下表列出了与解决功能相关的属性。 有关解析功能的详细信息，请参阅 [标准功能](standard-features.md)。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>属性名称</th>
<th>特性参数</th>
<th>注释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em><strong>显示器</strong></p></td>
<td><p>数值，表示打印机分辨率的 x 和 y 值，以点/英寸为单位。</p></td>
<td><p>必需。 X 和 y 值必须等于 *<strong>TextDPI</strong> x 和 y 值，或者必须等于 *<strong>TextDPI</strong> x，y 值除以2的幂。 例如，如果 *<strong>TextDPI</strong> 为成对 (300，300) ，则 *<strong>DPI</strong> 值可能成对 (300、300) 、对 (150、150) 或对 (75、75) ，但不 () 。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>MinStripBlankPixels</strong></p></td>
<td><p>数值，表示 Unidrv 在去除空字节之前应在扫描行中遇到的最小空白字节数。</p></td>
<td><p>可选。 如果未指定，则默认值为零。 仅当 <em> <strong>StripBlanks</strong>条目指定包含时，此属性才适用。 请参阅 <a href="raster-data-emission-attributes.md" data-raw-source="[Raster Data Emission Attributes](raster-data-emission-attributes.md)">光栅数据发射特性</a>。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>PinsPerLogPass</strong></p></td>
<td><p>数值，显示打印头的一个逻辑走轮打印的扫描行数。 必须是 PinsPerPhysPass 的倍数 <em> <strong>PinsPerPhysPass</strong>，因为每个逻辑传递都包含一个或多个物理阶段。</p></td>
<td><p>可选。 如果未指定，则默认值为1。 如果打印机执行隔行扫描，需要在一组扫描行中使用打印头的多轮，则需要打印所有扫描行。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>PinsPerPhysPass</strong></p></td>
<td><p>数值，表示打印头在页面上移动时打印的扫描行数。 必须是8的倍数。</p></td>
<td><p>可选。 如果未指定，则默认值为1。</p>
<p>水平和垂直分辨率应为 PinsPerPhysPass 的倍数 <em> <strong>PinsPerPhysPass</strong>，否则输出可能是不可预知的。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>RequireUniDir?</strong></p></td>
<td><p><strong>TRUE</strong> 或 <strong>FALSE</strong>，指示指定的解决方法是否需要启用单向打印。</p></td>
<td><p>可选。 如果未指定，则默认值为 <strong>FALSE</strong>。</p></td>
</tr>
<tr class="even">
<td><p><em><strong>SpotDiameter</strong></p></td>
<td><p>表示由 *<strong>DPI</strong>指定分辨率的以像素大小的百分比表示的专色直径大小的数值。</p></td>
<td><p>必需。</p>
<p>示例：</p>
100表示专色直径等于像素大小。
200表示该专色直径为像素大小的两倍。
50表示点直径为像素大小的一半。</td>
</tr>
<tr class="odd">
<td><p></em><strong>TextDPI</strong></p></td>
<td><p>表示打印机文本分辨率的 x 和 y 值的对或数值，以点/英寸为单位。</p></td>
<td><p>必需。 请参阅 *<strong>DPI</strong> 注释。 此分辨率用于绘制字体和矢量图形。</p></td>
</tr>
</tbody>
</table>

 

有关示例，请参阅 [示例 GPD 文件](sample-gpd-files.md)。

有关其他选项属性的信息，请参阅 [所有功能的选项属性](option-attributes-for-all-features.md)。

另请参阅 [控制图像质量](controlling-image-quality.md)。

 

 





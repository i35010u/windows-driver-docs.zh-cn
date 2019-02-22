---
title: 解析功能的选项属性
description: 解析功能的选项属性
ms.assetid: f04cd119-38c7-465c-b4fd-d657aa5bfacd
keywords:
- 解析功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 529829b089f2708a8d924d76b1c65dd44ab3b434
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541081"
---
# <a name="option-attributes-for-the-resolution-feature"></a>解析功能的选项属性





下表列出了与解析功能相关联的属性。 有关解决方法功能的详细信息，请参阅[标准功能](standard-features.md)。

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
<th>备注</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em><strong>DPI</strong></p></td>
<td><p>对数字值表示的 x 和 y 值的打印机&#39;s 分辨率，以每英寸点数。</p></td>
<td><p>必需。 X 和 y 值必须等于 *<strong>TextDPI</strong> x 和 y 值，或它们必须等于 *<strong>TextDPI</strong> x 和 y 值除以 2 的幂。 例如，如果 *<strong>TextDPI</strong>然后是对 （300、 300） *<strong>DPI</strong>值可能会对 （300、 300）、 对 （150，150），或对 （75，75），但未对 （100，100）。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>MinStripBlankPixels</strong></p></td>
<td><p>表示最小空白 Unidrv 应去除封闭空白的字节数之前遇到扫描行中的字节数的数字值。</p></td>
<td><p>可选。 如果未指定，默认值为零。 此属性是相关才<em> <strong>StripBlanks</strong>条目指定 ENCLOSED。 请参阅<a href="raster-data-emission-attributes.md" data-raw-source="[Raster Data Emission Attributes](raster-data-emission-attributes.md)">光栅数据显示特性</a>。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>PinsPerLogPass</strong></p></td>
<td><p>提供打印的打印头的一次逻辑传递扫描行数的数字值。 必须为倍数<em> <strong>PinsPerPhysPass</strong>，因为每次逻辑传递包含一个或多个物理阶段。</p></td>
<td><p>可选。 如果未指定，默认值为 1。 所需打印机如果执行隔行扫描，扫描线，可以打印所有扫描行的一组需要都打印头的多个阶段。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>PinsPerPhysPass</strong></p></td>
<td><p>按打印头的移动整个页面打印数字值，该值表示扫描行数。 必须是一个，或八的倍数。</p></td>
<td><p>可选。 如果未指定，默认值为 1。</p>
<p>水平和垂直分辨率应为的倍数<em> <strong>PinsPerPhysPass</strong>，或可能不可预测的输出。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>RequireUniDir?</strong></p></td>
<td><p><strong>TRUE</strong>或<strong>FALSE</strong>，以指示是否指定的分辨率需要单向打印才可用。</p></td>
<td><p>可选。 如果未指定，默认值是<strong>FALSE</strong>。</p></td>
</tr>
<tr class="even">
<td><p><em><strong>SpotDiameter</strong></p></td>
<td><p>数值的像素大小，用于解析指定的百分比表示找出直径大小 *<strong>DPI</strong>。</p></td>
<td><p>必需。</p>
<p>示例：</p>
100 意味着找出直径等于像素的大小。
200 意味着找出直径像素大小的两倍。
50 意味着找出直径像素大小的一半。</td>
</tr>
<tr class="odd">
<td><p></em><strong>TextDPI</strong></p></td>
<td><p>对或数字值表示 x 和 y 值的打印机&#39;s 文本分辨率，以每英寸点数。</p></td>
<td><p>必需。 请参阅 *<strong>DPI</strong>注释。 此解决方法用于绘制字体和矢量图形。</p></td>
</tr>
</tbody>
</table>

 

有关示例，请参阅[示例 GPD 文件](sample-gpd-files.md)。

有关其他选项的属性的信息，请参阅[所有功能的选项属性](option-attributes-for-all-features.md)。

另请参阅[控制图像质量](controlling-image-quality.md)。

 

 





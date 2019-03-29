---
title: 设备字体属性
description: 设备字体属性
ms.assetid: 748faa90-9c31-44c2-8bb3-641a1f95eab1
keywords:
- 设备字体 WDK Unidrv
- 字体属性 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1ac6cd84875d3e93fb22f5b9a4524d5141eb000
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464057"
---
# <a name="attributes-for-device-fonts"></a>设备字体属性





下表列出了属性描述设备字体的打印机的支持。

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
<td><p><strong><em>CharPosition</strong></p></td>
<td><p>UPPERLEFT 或基线。 指示区域的边界的框打印一个字符之前应该向其定位打印头的字符。</p></td>
<td><p>可选。 如果未指定，默认值将为 UPPERLEFT。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>DefaultCTT</strong></p></td>
<td><p>表示 RC_CTT 资源标识符的默认字符转换表的数字值。</p></td>
<td><p></p>
可选。 仅适用于 TTY 打印机。
如果未指定，则不转换表。 （此属性提供仅为了向后兼容 GPC 文件中）。</td>
</tr>
<tr class="odd">
<td><p><strong><em>DefaultFont</strong></p></td>
<td><p>表示默认字体的 RC_FONT 或 RC_UFM 资源标识符的数字值。</p></td>
<td><p>所需打印机是否支持设备字体。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>LookAheadRegion</strong></p></td>
<td><p>数字 （整数） 值，该值表示如何提前驱动程序必须"查找"以确定它是否应发出文本。 此值是在<em>y</em>掌握单位，但必须可转换为整数个像素。 有关详细信息，请参阅此表后面的注释。</p></td>
<td><p>可选。 如果未指定，默认值为零。 仅用于串行打印机，(例如，HP DeskJet)，用于对文本和位图数据进行排序。</p></td>
</tr>
<tr class="odd">
<td><p><strong><em>MaxFontUsePerPage</strong></p></td>
<td><p>表示字体的最大数目的数字值每页可以使用打印机。</p></td>
<td><p>可选。 如果未指定，则没有限制。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>TextYOffset</strong></p></td>
<td><p>数值中表示的垂直距离<em>y</em>掌握的单位，按其自带字体必须重新定位以与位图字体基线对齐。</p></td>
<td><p>可选。 如果未指定，默认值为 0。 （用于某些点阵打印机。）</p></td>
</tr>
</tbody>
</table>

 

有关示例，请参阅[示例 GPD 文件](sample-gpd-files.md)。

### <a href="" id="note-on--lookaheadregion"></a>请注意在\*LookAheadRegion

若要确定向前查找区域的大小，打印机驱动程序必须执行基于当前扫描行和的值的补充\* **LookAheadRegion**属性。 因为扫描行中时以像素为单位\* **LookAheadRegion**垂直 master 数据库中为单位，该驱动程序必须将属性值转换为像素。

例如，如果的值\* **LookAheadRegion**属性为 600，且有 1200年垂直主英寸为单位，则预测先行区域 1.5 英寸的大小。 如果当前的分辨率是 300 dpi，照对应于 150 像素 （垂直） 或 150 扫描行。 如果打印机当前扫描 100 行上，必须查找扫描行 100 到 250 之间的文本基线的驱动程序。

尽管它会发出一次找到的文本，该驱动程序对于每个扫描行，请重复此过程。

 

 





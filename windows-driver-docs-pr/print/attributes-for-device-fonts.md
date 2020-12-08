---
title: 设备字体属性
description: 设备字体属性
keywords:
- 设备字体 WDK Unidrv
- 字体属性 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 843197d0658503913b8a4da86159a0ac4ce80c5c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836119"
---
# <a name="attributes-for-device-fonts"></a>设备字体属性





下表列出了描述打印机对设备字体的支持的属性。

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
<td><p><strong><em>CharPosition</strong></p></td>
<td><p>UPPERLEFT 或基线。 指示打印头在打印字符前应定位到的字符边界框区域。</p></td>
<td><p>可选。 如果未指定，则默认值为 UPPERLEFT。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>DefaultCTT</strong></p></td>
<td><p>数值，表示默认字符转换表的 RC_CTT 资源标识符。</p></td>
<td><p></p>
可选。 仅适用于 TTY 打印机。
如果未指定，则没有转换表。  (仅提供此属性是为了向后兼容 GPC 文件。 ) </td>
</tr>
<tr class="odd">
<td><p><strong><em>DefaultFont</strong></p></td>
<td><p>数值，表示默认字体的 RC_FONT 或 RC_UFM 资源标识符。</p></td>
<td><p>如果打印机支持设备字体，则为必需。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>LookAheadRegion</strong></p></td>
<td><p>数值 (整数) 值，该值表示驱动程序的提前程度，以确定它是否应发出文本。 此值为 <em>y</em> 主单元，但必须可转换为整数像素数。 有关详细信息，请参阅此表后面的注释。</p></td>
<td><p>可选。 如果未指定，则默认值为零。 仅与串行打印机一起使用， (例如 HP DeskJet) ，用于对文本和位图数据进行排序。</p></td>
</tr>
<tr class="odd">
<td><p><strong><em>MaxFontUsePerPage</strong></p></td>
<td><p>表示打印机可在每页中使用的最大字体数的数值。</p></td>
<td><p>可选。 如果未指定，则没有限制。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>TextYOffset</strong></p></td>
<td><p>表示垂直距离的数字值，以 <em>y</em> 主单位为单位，必须通过该数值重定位其，才能与位图字体基线对齐。</p></td>
<td><p>可选。 如果未指定，则默认值为 0。  (用于某些点阵打印机。 ) </p></td>
</tr>
</tbody>
</table>

 

有关示例，请参阅 [示例 GPD 文件](sample-gpd-files.md)。

### <a name="note-on-lookaheadregion"></a><a href="" id="note-on--lookaheadregion"></a>LookAheadRegion 上的注意事项 \*

若要确定预测先行区域的大小，打印机驱动程序必须根据当前扫描行和 LookAheadRegion 属性的值执行添加 \* **LookAheadRegion** 。 由于扫描行以像素为单位，而 \* *_LookAheadRegion_* 是垂直的主单位，因此驱动程序必须将属性值转换为像素。

例如，如果 \* *_LookAheadRegion_* 属性的值为600，并且每英寸有1200个垂直的主单位，则预测先行区域的大小为半英寸。 如果当前分辨率为 300 dpi，则半英寸对应于150像素 (竖) 或150扫描行。 如果打印机当前在扫描行100上，则驱动程序必须在扫描行100和250之间查找文本基线。

驱动程序会为每个扫描行重复此过程，但会发出它仅找到一次的文本。

 

 





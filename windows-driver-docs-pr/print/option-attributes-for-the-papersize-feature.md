---
title: 纸张大小功能的选项属性
description: 纸张大小功能的选项属性
ms.assetid: cfd82bc5-b89b-41c2-b542-28cb5905e37a
keywords:
- PaperSize 功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0358299ed31d7f114da95cc7c0b56609ee3c5178
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353695"
---
# <a name="option-attributes-for-the-papersize-feature"></a>纸张大小功能的选项属性





下表列出了与 PaperSize 功能相关联的属性。 有关 PaperSize 功能的详细信息，请参阅[标准功能](standard-features.md)。

**请注意**  即使要使用属性来描述不同的方向，如横向以下特性的所有纸张大小规范必须都表示纵向方向相对应。

 

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
<td><p><em><strong>BottomMargin</strong></p></td>
<td><p>数字值，该值表示最小允许下的边距，x 中主与 CUSTOMSIZE 选项相关联的用户指定的纸张大小的单位。 值是相对于物理页的底部。</p></td>
<td><p>可选。 如果未指定，默认值为 0。 仅与 CUSTOMSIZE 选项一起使用。 假定纵向方向。 请参阅<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">指定的纸张大小</a>。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>CenterPrintable？</strong></p></td>
<td><p><strong>TRUE</strong>或<strong>FALSE</strong>，，该值指示指定的值是否<em> <strong>MaxPrintableWidth</strong>居中。</p></td>
<td><p>可选。 如果未指定，可打印区域是由指定的边距右侧<em> <strong>MinLeftMargin</strong>。 仅与 CUSTOMSIZE 选项一起使用。 请参阅<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">指定的纸张大小</a>。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>CursorOrigin</strong></p></td>
<td><p>表示光标源中的位置，主单元，其中对 （0，0） 是左上的角的数字值对。 或者对于 CUSTOMSIZE，指定使用这些值<em> <strong>CustCursorOriginX</strong>和 *<strong>CustCursorOriginY</strong>。</p></td>
<td><p>可选。 如果未指定，默认值是对 （0，0）。 Unidrv 假定游标原点，相对于打印机，常量具有不同的纸张大小。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>CustCursorOriginX</strong></p></td>
<td><p>若要创建的 x 索引的值所用的 CUSTOMSIZE 参数表达式<em> <strong>CursorOrigin</strong>。</p></td>
<td><p>可选。 仅与 CUSTOMSIZE 选项一起使用。 请参阅<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">指定的纸张大小</a>。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>CustCursorOriginY</strong></p></td>
<td><p>若要创建的 y 索引值所用的 CUSTOMSIZE 参数表达式<em> <strong>CursorOrigin</strong>。</p></td>
<td><p>可选。 仅与 CUSTOMSIZE 选项一起使用。 请参阅<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">指定的纸张大小</a>。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>CustPrintableOriginX</strong></p></td>
<td><p>若要创建的 x 索引的值所用的 CUSTOMSIZE 参数表达式<em> <strong>PrintableOrigin</strong>。</p></td>
<td><p>可选。 仅与 CUSTOMSIZE 选项一起使用。 请参阅<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">指定的纸张大小</a>。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>CustPrintableOriginY</strong></p></td>
<td><p>若要创建的 y 索引值所用的 CUSTOMSIZE 参数表达式<em> <strong>PrintableOrigin</strong>。</p></td>
<td><p>可选。 仅与 CUSTOMSIZE 选项一起使用。 请参阅<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">指定的纸张大小</a>。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>CustPrintableSizeX</strong></p></td>
<td><p>CUSTOMSIZE 参数表达式，用于创建的 x 值的值<em> <strong>PrintableArea</strong>。</p></td>
<td><p>可选。 仅与 CUSTOMSIZE 选项一起使用。 请参阅<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">指定的纸张大小</a>。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>CustPrintableSizeY</strong></p></td>
<td><p>若要创建的 y 值的值所用的 CUSTOMSIZE 参数表达式<em> <strong>PrintableArea</strong>。</p></td>
<td><p>可选。 仅与 CUSTOMSIZE 选项一起使用。 请参阅<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">指定的纸张大小</a>。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>MaxSize</strong></p></td>
<td><p>对数字值表示页的最大允许长度 (x) 和中与 CUSTOMSIZE 选项相关联的用户指定的纸张大小的主单位的高度 (y) 值。</p></td>
<td><p>所需的 CUSTOMSIZE 选项。 假定纵向方向。 请参阅<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">指定的纸张大小</a>。</p></td>
</tr>
<tr class="odd">
<td><p><em><strong>MaxPrintableWidth</strong></p></td>
<td><p>数字值，该值表示 x 中的最大可打印宽度掌握与 CUSTOMSIZE 选项相关联的用户指定的纸张大小的单位。</p></td>
<td><p>所需的 CUSTOMSIZE 选项。 假定纵向方向。 请参阅<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">指定的纸张大小</a>。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>MinLeftMargin</strong></p></td>
<td><p>数字值，该值表示最小的允许左边的距，以 x 掌握与 CUSTOMSIZE 选项相关联的用户指定的纸张大小的单位。 值是相对于物理页的左边缘</p></td>
<td><p>可选。 如果未指定，默认值为 0。 仅与 CUSTOMSIZE 选项一起使用。 假定纵向方向。 请参阅<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">指定的纸张大小</a>。</p></td>
</tr>
<tr class="odd">
<td><p><em><strong>MinSize</strong></p></td>
<td><p>对数字值表示最小允许页面长度 (x) 和中与 CUSTOMSIZE 选项相关联的用户指定的纸张大小的主单位的高度 (y) 值。</p></td>
<td><p>所需的 CUSTOMSIZE 选项。 假定纵向方向。 请参阅<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">指定的纸张大小</a>。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>PageDimensions</strong></p></td>
<td><p>对数字值表示页长度 (x) 和高度 (y) 值，以 master 为单位，任何自定义 PaperSize 功能选项。</p></td>
<td><p>仅用于供应商定义的纸张大小。 请参阅<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">指定的纸张大小</a>。</p></td>
</tr>
<tr class="odd">
<td><p><em><strong>PageProtectMem</strong></p></td>
<td><p>表示打印机内存量，以千字节为单位，保护页所需的数字值。</p></td>
<td><p>如果指定 PageProtect 功能被必需。 请参阅<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">指定的纸张大小</a>。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>PrintableArea</strong></p></td>
<td><p>对表示的 x 和 y 平面长度，以 master 为单位，可打印页面区域的数字值。</p></td>
<td><p>所需的所有 PaperSize 选项 CUSTOMSIZE 除外。 请参阅<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">指定的纸张大小</a>。</p></td>
</tr>
<tr class="odd">
<td><p><em><strong>PrintableOrigin</strong></p></td>
<td><p>表示可打印区域中，在主单元，相对于在纸张的左上角原点的数字值对。</p></td>
<td><p>所需的所有 PaperSize 选项 CUSTOMSIZE 除外。 对于 CUSTOMSIZE，可以指定使用这些值 *<strong>CustPrintableOriginX</strong>和 *<strong>CustPrintableOriginY</strong>。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>RotateSize?</strong></p></td>
<td><p><strong>TRUE</strong>或<strong>FALSE</strong>，因为在横向进纸 （通常信封），该值指示是否 Unidrv 应旋转页面维度。</p></td>
<td><p>可选。 如果未指定，默认值是<strong>FALSE</strong>。 可使用任何标准选项对于 PaperSize 功能，除 CUSTOMSIZE。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>TopMargin</strong></p></td>
<td><p>表示最小的允许上边距，以 y 主单位，适用于与 CUSTOMSIZE 选项相关联的用户指定的纸张大小的数字值。 值是相对于物理页的顶部。</p></td>
<td><p>可选。 如果未指定，默认值为 0。 仅与 CUSTOMSIZE 选项一起使用。 假定纵向方向。 请参阅<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">指定的纸张大小</a>。</p></td>
</tr>
</tbody>
</table>

 

有关示例，请参阅[示例 GPD 文件](sample-gpd-files.md)。

### <a href="" id="ddk-customsize-parameter-expressions-gg"></a>CUSTOMSIZE 参数表达式

自定义参数表达式是受限制的形式[命令字符串格式](command-string-format.md)。 不允许使用文本字符串。

在表达式中的**ArgumentType**段中，以下限制适用：

-   唯一**ArgumentType**允许值为 %d。

-   不允许用括号括起来的值的范围。

在表达式中的**StandardVariableExpression**段中，以下限制适用：

-   可以使用仅在 PhysPaperWidth 和 PhysPaperLength 标准变量。

-   **最大\_重复**不允许使用运算符。

以下是表达式示例：

```cpp
*CustCursorOriginX: %d{((PhysPaperWidth-14040)/2)+300}
*CustCursorOriginY: %d{180}
*CustPrintableOriginX: %d{300}
*CustPrintableOriginY: %d{300}
*CustPrintableSizeX: %d{PhysPaperWidth-600}
*CustPrintableSizeY: %d{PhysPaperLength-600}
```

 

 





---
title: 纸张大小功能的选项属性
description: 纸张大小功能的选项属性
ms.assetid: cfd82bc5-b89b-41c2-b542-28cb5905e37a
keywords:
- PaperSize 功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0358299ed31d7f114da95cc7c0b56609ee3c5178
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79242908"
---
# <a name="option-attributes-for-the-papersize-feature"></a>纸张大小功能的选项属性





下表列出了与 PaperSize 功能相关的属性。 有关 PaperSize 功能的详细信息，请参阅[标准功能](standard-features.md)。

**请注意**   以下属性的所有纸张大小规格必须相对于纵向表示，即使这些属性用于描述不同的方向（如横向）也是如此。

 

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>属性名称</th>
<th>Attribute 参数</th>
<th>Comments</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em><strong>BottomMargin</strong></p></td>
<td><p>表示与 CUSTOMSIZE 选项关联的用户指定纸张大小的最小允许最小下边距（以 x 主单位表示）的数字值。 值相对于物理页的底部。</p></td>
<td><p>可选。 如果未指定，则默认值为 0。 仅与 CUSTOMSIZE 选项一起使用。 采用纵向方向。 请参阅<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">指定纸张大小</a>。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>CenterPrintable？</strong></p></td>
<td><p><strong>TRUE</strong>或<strong>FALSE</strong>，指示 <em><strong>MaxPrintableWidth</strong>指定的值是否居中。</p></td>
<td><p>可选。 如果未指定，可打印区域位于 <em><strong>MinLeftMargin</strong>指定的边距的右侧。 仅与 CUSTOMSIZE 选项一起使用。 请参阅<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">指定纸张大小</a>。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>CursorOrigin</strong></p></td>
<td><p>表示游标原点位置的数值，以主单位表示，其中对（0，0）是左上角。 或者，对于 CUSTOMSIZE，请使用 <em><strong>CustCursorOriginX</strong>和 *<strong>CustCursorOriginY</strong>指定这些值。</p></td>
<td><p>可选。 如果未指定，则默认值为成对（0，0）。 Unidrv 假定相对于打印机的光标原点是具有不同纸张大小的常量。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>CustCursorOriginX</strong></p></td>
<td><p>CUSTOMSIZE 参数 expression，用于创建 <em><strong>CursorOrigin</strong>的 x 索引的值。</p></td>
<td><p>可选。 仅与 CUSTOMSIZE 选项一起使用。 请参阅<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">指定纸张大小</a>。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>CustCursorOriginY</strong></p></td>
<td><p>CUSTOMSIZE 参数 expression，用于创建 <em><strong>CursorOrigin</strong>的 y 索引的值。</p></td>
<td><p>可选。 仅与 CUSTOMSIZE 选项一起使用。 请参阅<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">指定纸张大小</a>。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>CustPrintableOriginX</strong></p></td>
<td><p>CUSTOMSIZE 参数 expression，用于创建 <em><strong>PrintableOrigin</strong>的 x 索引的值。</p></td>
<td><p>可选。 仅与 CUSTOMSIZE 选项一起使用。 请参阅<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">指定纸张大小</a>。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>CustPrintableOriginY</strong></p></td>
<td><p>CUSTOMSIZE 参数 expression，用于创建 <em><strong>PrintableOrigin</strong>的 y 索引的值。</p></td>
<td><p>可选。 仅与 CUSTOMSIZE 选项一起使用。 请参阅<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">指定纸张大小</a>。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>CustPrintableSizeX</strong></p></td>
<td><p>CUSTOMSIZE 参数表达式，用于创建 <em><strong>PrintableArea</strong>的 x 值的值。</p></td>
<td><p>可选。 仅与 CUSTOMSIZE 选项一起使用。 请参阅<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">指定纸张大小</a>。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>CustPrintableSizeY</strong></p></td>
<td><p>CUSTOMSIZE 参数 expression，用于创建 <em><strong>PrintableArea</strong>的 y 值的值。</p></td>
<td><p>可选。 仅与 CUSTOMSIZE 选项一起使用。 请参阅<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">指定纸张大小</a>。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>MaxSize</strong></p></td>
<td><p>表示与 CUSTOMSIZE 选项关联的用户指定纸张大小的最大允许页面长度（x）和高度（y）值（以主单位表示）的数值对。</p></td>
<td><p>对于 CUSTOMSIZE 选项是必需的。 采用纵向方向。 请参阅<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">指定纸张大小</a>。</p></td>
</tr>
<tr class="odd">
<td><p><em><strong>MaxPrintableWidth</strong></p></td>
<td><p>数值，表示与 CUSTOMSIZE 选项关联的用户指定纸张大小的最大可打印宽度（以 x 主单位为单位）。</p></td>
<td><p>对于 CUSTOMSIZE 选项是必需的。 采用纵向方向。 请参阅<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">指定纸张大小</a>。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>MinLeftMargin</strong></p></td>
<td><p>表示与 CUSTOMSIZE 选项关联的用户指定纸张大小的最小允许左边距（以 x 主单位为单位）的数字值。 值与物理页面的左边缘相关</p></td>
<td><p>可选。 如果未指定，则默认值为 0。 仅与 CUSTOMSIZE 选项一起使用。 采用纵向方向。 请参阅<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">指定纸张大小</a>。</p></td>
</tr>
<tr class="odd">
<td><p><em><strong>MinSize</strong></p></td>
<td><p>表示与 CUSTOMSIZE 选项关联的用户指定纸张大小的最小允许页面长度（x）和高度（y）值（以主单位表示）的数字值配对。</p></td>
<td><p>对于 CUSTOMSIZE 选项是必需的。 采用纵向方向。 请参阅<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">指定纸张大小</a>。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>PageDimensions</strong></p></td>
<td><p>表示页面长度（x）和高度（y）值（以主单位表示）的数值，适用于 PaperSize 功能的任何自定义选项。</p></td>
<td><p>仅用于供应商定义的纸张大小。 请参阅<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">指定纸张大小</a>。</p></td>
</tr>
<tr class="odd">
<td><p><em><strong>PageProtectMem</strong></p></td>
<td><p>数值，表示保护页面所需的打印机内存量（以 kb 为单位）。</p></td>
<td><p>如果指定了 PageProtect 功能，则为必需。 请参阅<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">指定纸张大小</a>。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>PrintableArea</strong></p></td>
<td><p>数值，表示可打印页面区域的 x 和 y 平面长度，以主单位表示。</p></td>
<td><p>所有 PaperSize 选项（CUSTOMSIZE 除外）都是必需的。 请参阅<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">指定纸张大小</a>。</p></td>
</tr>
<tr class="odd">
<td><p><em><strong>PrintableOrigin</strong></p></td>
<td><p>一对表示可打印区域原点的数值，以主单位表示，相对于纸张的左上角。</p></td>
<td><p>所有 PaperSize 选项（CUSTOMSIZE 除外）都是必需的。 对于 CUSTOMSIZE，可以使用 *<strong>CustPrintableOriginX</strong>和 *<strong>CustPrintableOriginY</strong>指定这些值。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>RotateSize？</strong></p></td>
<td><p><strong>TRUE</strong>或<strong>FALSE</strong>，指示 Unidrv 是否应旋转页面尺寸，因为纸张（通常是信封）是侧向送入的。</p></td>
<td><p>可选。 如果未指定，则默认值为<strong>FALSE</strong>。 可以与 PaperSize 功能的任何标准选项一起使用，CUSTOMSIZE 除外。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>TopMargin</strong></p></td>
<td><p>表示与 CUSTOMSIZE 选项关联的用户指定纸张大小的最小允许最小上边距（以 y 主单位表示）的数字值。 值相对于物理页的顶部。</p></td>
<td><p>可选。 如果未指定，则默认值为 0。 仅与 CUSTOMSIZE 选项一起使用。 采用纵向方向。 请参阅<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">指定纸张大小</a>。</p></td>
</tr>
</tbody>
</table>

 

有关示例，请参阅[示例 GPD 文件](sample-gpd-files.md)。

### <a href="" id="ddk-customsize-parameter-expressions-gg"></a>CUSTOMSIZE 参数表达式

自定义参数表达式是一种受限制的[命令字符串格式](command-string-format.md)。 不允许使用文本字符串。

在表达式的**ArgumentType**段中，以下限制适用：

-   唯一允许的**ArgumentType**值为% d。

-   不允许使用括号内的值范围。

在表达式的**StandardVariableExpression**段中，以下限制适用：

-   只能使用 PhysPaperWidth 和 PhysPaperLength 标准变量。

-   不允许使用**Max\_Repeat**运算符。

以下是表达式示例：

```cpp
*CustCursorOriginX: %d{((PhysPaperWidth-14040)/2)+300}
*CustCursorOriginY: %d{180}
*CustPrintableOriginX: %d{300}
*CustPrintableOriginY: %d{300}
*CustPrintableSizeX: %d{PhysPaperWidth-600}
*CustPrintableSizeY: %d{PhysPaperLength-600}
```

 

 





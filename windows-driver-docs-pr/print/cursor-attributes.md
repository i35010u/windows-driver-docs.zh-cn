---
title: 光标属性
description: 光标属性
keywords:
- 游标属性 WDK Unidrv
- 常规打印机属性 WDK Unidrv、cursor
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00c1d18a2466aff1f906409037bd45f6d349fe6f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797435"
---
# <a name="cursor-attributes"></a>光标属性





游标属性是 [常规打印属性](general-printing-attributes.md) ，用于指定打印机的游标的特征。

下表列出了游标特性。

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
<td><p><strong><em>AbsXMovesRightOnly?</strong></p></td>
<td><p><strong>TRUE</strong> 或 <strong>FALSE</strong>。 此参数用于指定设备只能接受向右移动当前位置的绝对移动命令。 如果需要移动到当前位置的左侧，Unidrv 将首先发送一个回车符，以便发送的绝对命令位于新当前位置的右侧。</p></td>
<td><p>可选。 如果未指定，则默认值为 <strong>FALSE</strong>。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>BadCursorMoveInGrxMode</strong></p></td>
<td><p></p>表示光栅图形模式下的非法光标移动的值
<a href="lists.md" data-raw-source="[LIST](lists.md)">列表</a>。 可以是以下一个或多个 X_PORTRAIT X_LANDSCAPE Y_PORTRAIT Y_LANDSCAPE</td>
<td><p>可选。 如果未指定，则默认值为 "无限制"。 例如，LIST (X_PORTRAIT) 指示垂直方向不允许 X 方向移动。</p></td>
</tr>
<tr class="odd">
<td><p><strong><em>CursorXAfterCR</strong></p></td>
<td><p></p>
以下项之一： AT_PRINTABLE_X_ORIGIN AT_CURSOR_X_ORIGIN
<p>指示光标在回车后的 x 位置。</p></td>
<td><p>可选。 如果未指定，则默认值为 AT_CURSOR_X_ORIGIN，这是物理零位置。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>EjectPageWithFF?</strong></p></td>
<td><p><strong>TRUE</strong> 或 <strong>FALSE</strong>。 指示打印机是否使用换页符来弹出页面。</p></td>
<td><p>可选。 如果未指定，则默认值为 <strong>FALSE</strong>。</p></td>
</tr>
<tr class="odd">
<td><p><strong><em>LineSpacingMoveUnit</strong></p></td>
<td><p>正整数值。 指定 CmdSetLineSpacing 命令的移动单元。 单位以点/英寸为单位表示。 对于行间距移动单元为 1/60th 英寸的打印机，此条目应为60。</p>
<p>请注意，行距移动单元必须均匀地分为主 Y 单位。</p>
<p>* MaxLineSpacing 参数仍在主单元中，与是否指定了 *<strong>LineSpacingMoveUnit</strong> 无关。</p></td>
<td><p>可选。 默认值为1个主单元。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>MaxLineSpacing</strong></p></td>
<td><p>表示最大行距（以 y 为主单位表示）的数字值。</p></td>
<td><p>可选。 如果未指定，则 Unidrv 假定没有最大值。</p></td>
</tr>
<tr class="odd">
<td><p><strong><em>UseSpaceForXMove?</strong></p></td>
<td><p><strong>TRUE</strong> 或 <strong>FALSE</strong>。 指示是否可以使用空格字符来执行光标的 x 方向移动。</p></td>
<td><p>可选。 如果未指定，则默认值为 <strong>TRUE</strong>。</p>
<p>如果 <strong>为 TRUE，则</strong>Unidrv 将使用空格进行粗移动，并使用 null 进行微调。 如果 <strong>为 FALSE</strong>，则 Unidrv 对所有移动使用 null。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>XMoveThreshold</strong></p></td>
<td><p>数值，用 x 主单位表示，超过此值后，应使用 <strong>CmdXMoveAbsolute</strong> ，而不是 <strong>CmdXMoveRelLeft</strong> 或 <strong>CmdXMoveRelRight</strong>。</p></td>
<td><p>可选。 如果未指定，则默认值为零，这意味着应始终使用 <strong>CmdXMoveAbsolute</strong> 。 仅当指定了所有三个 x 移动命令时才适用。</p></td>
</tr>
<tr class="odd">
<td><p><strong><em>XMoveUnit</strong></p></td>
<td><p>数值（以每英寸点数为单位），表示打印机支持的最小水平移动。 例如，如果移动单元为 1/600th 英寸，则指定的值为600。</p></td>
<td><p>如果打印机支持水平移动 <a href="cursor-commands.md" data-raw-source="[cursor commands](cursor-commands.md)">光标命令</a>，则是必需的。  (如果已指定，则在计算 <a href="master-units.md" data-raw-source="[master units](master-units.md)">主单位</a>时包含此值 ) </p></td>
</tr>
<tr class="even">
<td><p><strong></em>YMoveAttributes</strong></p></td>
<td><p></p>
指示 y 移动属性的值的列表。 可以是以下项中的一个或多个： FAV_LF (优选) 的 LF 间距 SEND_CR_FIRST</td>
<td><p>可选。 如果未指定，则不采用任何属性。</p></td>
</tr>
<tr class="odd">
<td><p><strong><em>YMoveThreshold</strong></p></td>
<td><p>数值，用 y-主单位表示，超过此值后，应该使用 <strong>CmdYMoveAbsolute</strong> ，而不是 <strong>CmdYMoveRelLeft</strong> 或 <strong>CmdYMoveRelRight</strong>。</p></td>
<td><p>可选。 如果未指定，则默认值为零，这意味着应始终使用 <strong>CmdYMoveAbsolute</strong> 。 仅当指定了所有三个 y 移动命令时才适用。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>YMoveUnit</strong></p></td>
<td><p>数值（以每英寸点数为单位），表示打印机支持的最小垂直移动。 例如，如果移动单元为 1/600th 英寸，则指定的值为600。</p></td>
<td><p>如果打印机支持垂直移动 <a href="cursor-commands.md" data-raw-source="[cursor commands](cursor-commands.md)">光标命令</a>，则是必需的。  (如果已指定，则在计算 <a href="master-units.md" data-raw-source="[master units](master-units.md)">主单位</a>时包含此值 ) </p></td>
</tr>
</tbody>
</table>

 

有关示例，请参阅 [示例 GPD 文件](sample-gpd-files.md)。

 

 





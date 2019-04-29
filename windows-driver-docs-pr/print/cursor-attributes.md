---
title: 光标属性
description: 光标属性
ms.assetid: 43646e2a-bc40-430e-ac7e-6fe4cb353309
keywords:
- 游标属性 WDK Unidrv
- 常规打印机属性 WDK Unidrv、 光标
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c4604e051d424401475de3eaee82de64014e087
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365544"
---
# <a name="cursor-attributes"></a>光标属性





游标属性包括[常规打印属性](general-printing-attributes.md)，用于指定打印机的游标的特征。

下表列出了游标属性。

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
<td><p><strong><em>AbsXMovesRightOnly?</strong></p></td>
<td><p><strong>TRUE</strong>或<strong>FALSE</strong>。 此参数用于指定设备可以接受仅向右移动当前的位置的绝对移动命令。 如果需要迁移到当前位置的左侧，Unidrv 第一次发送一个回车符返回，以便绝对命令发送到新的当前位置的右侧。</p></td>
<td><p>可选。 如果未指定，默认值是<strong>FALSE</strong>。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>BadCursorMoveInGrxMode</strong></p></td>
<td><p></p>
<a href="lists.md" data-raw-source="[LIST](lists.md)">列表</a>的值表示非法的光标在光栅图形模式下的移动。 可以是一种或多种：X_PORTRAIT X_LANDSCAPE Y_PORTRAIT Y_LANDSCAPE</td>
<td><p>可选。 如果未指定，默认值为没有限制。 例如，LIST(X_PORTRAIT) 指示纵向方向不允许使用 x 方向移动。</p></td>
</tr>
<tr class="odd">
<td><p><strong><em>CursorXAfterCR</strong></p></td>
<td><p></p>
其中一种：AT_PRINTABLE_X_ORIGIN AT_CURSOR_X_ORIGIN
<p>返回一个回车符后指示光标的 x 位置。</p></td>
<td><p>可选。 如果未指定，默认值是 AT_CURSOR_X_ORIGIN，这是物理零的位置。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>EjectPageWithFF?</strong></p></td>
<td><p><strong>TRUE</strong>或<strong>FALSE</strong>。 指示打印机是否采用换页符弹出一个页面的步骤。</p></td>
<td><p>可选。 如果未指定，默认值是<strong>FALSE</strong>。</p></td>
</tr>
<tr class="odd">
<td><p><strong><em>LineSpacingMoveUnit</strong></p></td>
<td><p>正整数值。 指定 CmdSetLineSpacing 命令移动单位。 以每英寸点数表示单位。 为打印机的行距移动的单位为 1/60th 1/96 英寸为单位，此项应为 60。</p>
<p>请注意行间距移动单元必须均匀划分主 Y 单元。</p>
<p>* MaxLineSpacing 参数仍处于 master 单位独立于是否 *<strong>LineSpacingMoveUnit</strong>指定。</p></td>
<td><p>可选。 默认值为 1 个主单位。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>MaxLineSpacing</strong></p></td>
<td><p>表示的最大行间距，以 y master 单位数值。</p></td>
<td><p>可选。 如果未指定，Unidrv 假定不存在最大值。</p></td>
</tr>
<tr class="odd">
<td><p><strong><em>UseSpaceForXMove?</strong></p></td>
<td><p><strong>TRUE</strong>或<strong>FALSE</strong>。 指示是否可以使用空格字符来执行光标的 x 方向移动。</p></td>
<td><p>可选。 如果未指定，默认值是<strong>，则返回 TRUE</strong>。</p>
<p>如果<strong>，则返回 TRUE</strong>，Unidrv 有关粗略移动使用空间并且包含 null 值，细移动。 如果<strong>FALSE</strong>，Unidrv 使用 null 值的所有移动。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>XMoveThreshold</strong></p></td>
<td><p>数字值，以 x master 单位，表示移动阈值超过该阈值<strong>CmdXMoveAbsolute</strong>应使用而不是<strong>CmdXMoveRelLeft</strong>或<strong>CmdXMoveRelRight</strong>.</p></td>
<td><p>可选。 如果未指定，默认值为零，含义<strong>CmdXMoveAbsolute</strong>应始终使用。 仅当指定所有三个 x 移动命令才适用。</p></td>
</tr>
<tr class="odd">
<td><p><strong><em>XMoveUnit</strong></p></td>
<td><p>数字值，以每英寸点数，表示最小水平运动打印机都能够。 例如，如果移动单位为 1/600th 1/96 英寸为单位，指定的值为 600。</p></td>
<td><p>所需打印机是否支持水平运动<a href="cursor-commands.md" data-raw-source="[cursor commands](cursor-commands.md)">游标命令</a>。 (如果指定，包括此值时计算<a href="master-units.md" data-raw-source="[master units](master-units.md)">掌握单位</a>。)</p></td>
</tr>
<tr class="even">
<td><p><strong></em>YMoveAttributes</strong></p></td>
<td><p></p>
值，该值指示 y 移动特性列表。 可以是一种或多种：FAV_LF （优选 LF 间距） SEND_CR_FIRST</td>
<td><p>可选。 如果未指定，则假定没有属性。</p></td>
</tr>
<tr class="odd">
<td><p><strong><em>YMoveThreshold</strong></p></td>
<td><p>数字值，以 y master 单位，表示移动阈值超过该阈值<strong>CmdYMoveAbsolute</strong>应使用而不是<strong>CmdYMoveRelLeft</strong>或<strong>CmdYMoveRelRight</strong>.</p></td>
<td><p>可选。 如果未指定，默认值为零，含义<strong>CmdYMoveAbsolute</strong>应始终使用。 仅当指定所有三个 y 移动命令才适用。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>YMoveUnit</strong></p></td>
<td><p>数字值，以每英寸点数，表示最小的垂直移动打印机都能够。 例如，如果移动单位为 1/600th 1/96 英寸为单位，指定的值为 600。</p></td>
<td><p>如果打印机支持的垂直移动所需<a href="cursor-commands.md" data-raw-source="[cursor commands](cursor-commands.md)">游标命令</a>。 (如果指定，包括此值时计算<a href="master-units.md" data-raw-source="[master units](master-units.md)">掌握单位</a>。)</p></td>
</tr>
</tbody>
</table>

 

有关示例，请参阅[示例 GPD 文件](sample-gpd-files.md)。

 

 





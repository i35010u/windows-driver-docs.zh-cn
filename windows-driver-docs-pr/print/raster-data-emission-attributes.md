---
title: 光栅数据发射属性
description: 光栅数据发射属性
keywords:
- 数据发射光栅打印属性 WDK Unidrv
- 发射光栅印刷特性 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a0e09d50937bce52a885bc94b6651c1d40fb86a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807099"
---
# <a name="raster-data-emission-attributes"></a>光栅数据发射属性





下表列出了说明打印机支持的光栅数据的属性。

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
<td><p><em><strong>CursorXAfterSendBlockData</strong></p></td>
<td><p>指示在发送光栅数据块后光标的 x 位置的常量值。 可以是以下项之一：</p>
AT_GRXDATA_END AT_GRXDATA_ORIGIN AT_CURSOR_X_ORIGIN 表示图形块开始处的像素、块中最后一个像素之后的像素或游标原点。</td>
<td><p>可选。 如果未指定，则默认值为 AT_GRXDATA_END。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>CursorYAfterSendBlockData</strong></p></td>
<td><p>指示在发送光栅数据块后游标的 y 位置的常量值。 可以是以下项之一：</p>
NO_MOVE AUTO_INCREMENT</td>
<td><p>可选。 如果未指定，则默认值为 NO_MOVE，这意味着光标的 y 位置保持不变。</p></td>
</tr>
<tr class="odd">
<td><p><em><strong>MaxMultipleRowBytes</strong></p></td>
<td><p>数值，指示在设置 * SendMultipleRows 的设备上下载光栅数据时使用的最大大小光栅块为 <strong>TRUE</strong>。</p></td>
<td><p>默认值为 32 KB。 允许的最大值为 256 KB。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>MirrorRasterByte </strong> ？</p></td>
<td><p><strong>TRUE</strong> 或 <strong>FALSE</strong>，指示 Unidrv 是否应 (反转) 图像数据的每个字节进行镜像。</p></td>
<td><p>可选。 如果未指定，则默认值为 <strong>FALSE</strong>。</p></td>
</tr>
<tr class="odd">
<td><p><em><strong>MirrorRasterPage?</strong></p></td>
<td><p><strong>TRUE</strong> 或 <strong>FALSE</strong>，指示是否对输出进行镜像。 如果 <strong>为 TRUE</strong>，则此属性会使页面上的所有内容都作为光栅打印，然后在与条带相反的方向上进行镜像。 这意味着纵向页面向右镜像;横向页面从上到下进行镜像。</p>
<p>此属性最适用于在透明胶片或背面打印胶片上打印。</p></td>
<td><p>可选。 默认值为 <strong>FALSE</strong>。</p>
<p>此属性是可重定位的全局特性。 它可能会显示为根级别属性 (在没有配置依赖项时，将看到 <a href="root-level-only-attributes.md" data-raw-source="[Root-Level-Only Attributes](root-level-only-attributes.md)">仅限根级别的特性</a>) ，或者根据每个媒体类型显示 * 选项或 * 案例构造。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>MoveToX0BeforeSetColor?</strong></p></td>
<td><p><strong>TRUE</strong> 或 <strong>FALSE</strong>，指示在可以发送显式颜色选择命令之前是否必须将游标的 x 坐标设置为零。</p></td>
<td><p>可选。 如果未指定，则默认值为 <strong>FALSE</strong>。 仅当<strong>TRUE</strong> <em> <strong>UseExpColorSelectCmd？</strong>也为<strong>True</strong>时，才可以为 true。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>OptimizeLeftBound?</strong></p></td>
<td><p><strong>TRUE</strong> 或 <strong>FALSE</strong>，指示 Unidrv 是否应删除每个带区左侧边界处的空白。</p></td>
<td><p>可选。 如果未指定，则默认值为 <strong>FALSE</strong>。</p></td>
</tr>
<tr class="even">
<td><p><em><strong>OutputDataFormat</strong></p></td>
<td><p>H_BYTE 或 V_BYTE，指示数据字节中的位是映射到水平像素还是垂直像素。</p></td>
<td><p>可选。 如果未指定，则默认值为 H_BYTE。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>PreAnalysisOptions</strong></p></td>
<td><p>数值，值为0、1、2、4或8。</p>
<p>有关每个 attribute 参数的含义的信息，请参阅 <a href="preanalysis-infrastructure.md" data-raw-source="[Preanalysis Infrastructure](preanalysis-infrastructure.md)">Preanalysis 基础结构</a>。</p></td>
<td><p>可选。 如果未指定，则默认值为1。</p></td>
</tr>
<tr class="even">
<td><p><em><strong>RasterSendAllData?</strong></p></td>
<td><p><strong>TRUE</strong> 或 <strong>FALSE</strong>，指示 Unidrv 是否应发送所有光栅数据，包括空白扫描行和扫描行中的空白。</p></td>
<td><p>可选。 如果未指定，则默认值为 <strong>FALSE</strong>。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>SendMultipleRows?</strong></p></td>
<td><p><strong>TRUE</strong> 或 <strong>FALSE</strong>，指示由 CmdSendBlockData 指定的命令是否可以一次发送多个块。</p></td>
<td></td>
</tr>
<tr class="even">
<td><p><em><strong>StripBlanks</strong></p></td>
<td><p>指示应去除光栅数据块中的空白的列表。 可以是以下一个或多个：</p>
前导包含尾随</td>
<td><p>可选。 如果未指定，则 Unidrv 不会去除任何空白。 另请参阅 *<strong>MinStripBlankPixels</strong> 在 <a href="option-attributes-for-the-resolution-feature.md" data-raw-source="[Option Attributes for the Resolution Feature](option-attributes-for-the-resolution-feature.md)">解决功能的选项属性</a>中。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>UseExpColorSelectCmd?</strong></p></td>
<td><p><strong>TRUE</strong> 或 <strong>FALSE</strong>，指示打印机是否需要显式颜色选择命令，不同于颜色光栅数据。</p></td>
<td><p>可选。 如果未指定，则默认值为 <strong>FALSE</strong>。 点阵打印机要求值为 <strong>TRUE</strong>。</p></td>
</tr>
</tbody>
</table>

 

有关与光栅数据发射相关的命令的信息，请参阅 [光栅数据发射命令](raster-data-emission-commands.md)。

有关示例，请参阅 [示例 GPD 文件](sample-gpd-files.md)。

 

 





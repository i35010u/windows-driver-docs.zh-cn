---
title: 光栅数据发射属性
description: 光栅数据发射属性
ms.assetid: 98366b64-f96b-4275-ba25-8483abf705aa
keywords:
- 数据发出光栅打印属性 WDK Unidrv
- 发出光栅打印属性 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8351112bd3860494a3823205f3f5021a5927ee9d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372438"
---
# <a name="raster-data-emission-attributes"></a>光栅数据发射属性





下表列出了属性描述为光栅数据发出的打印机的支持。

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
<td><p><em><strong>CursorXAfterSendBlockData</strong></p></td>
<td><p>发送的光栅数据块后，指示光标的 x 位置的常量值。 可以是：</p>
这意味着图形块，块或游标源中的最后一个之后的像素的开始处的像素 AT_GRXDATA_END AT_GRXDATA_ORIGIN AT_CURSOR_X_ORIGIN。</td>
<td><p>可选。 如果未指定，默认值将为 AT_GRXDATA_END。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>CursorYAfterSendBlockData</strong></p></td>
<td><p>发送的光栅数据块后，指示光标的 y 位置的常量值。 可以是：</p>
NO_MOVE AUTO_INCREMENT</td>
<td><p>可选。 如果未指定，默认值将为 NO_MOVE，这意味着光标的 y 位置保持不变。</p></td>
</tr>
<tr class="odd">
<td><p><em><strong>MaxMultipleRowBytes</strong></p></td>
<td><p>数字值，该值指示下载设置的设备上的光栅数据时要使用的最大大小光栅块 * SendMultipleRows？向<strong>，则返回 TRUE</strong>。</p></td>
<td><p>默认值为 32 KB。 最大允许值为 256 KB。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>MirrorRasterByte</strong>?</p></td>
<td><p><strong>TRUE</strong>或<strong>FALSE</strong>，以指示是否 Unidrv 应镜像 （反转） 图像数据的每个字节。</p></td>
<td><p>可选。 如果未指定，默认值是<strong>FALSE</strong>。</p></td>
</tr>
<tr class="odd">
<td><p><em><strong>MirrorRasterPage?</strong></p></td>
<td><p><strong>TRUE</strong>或<strong>FALSE</strong>，以指示输出是否是要镜像。 当<strong>，则返回 TRUE</strong>，该特性会导致要然后镜像中条带的相反方向和作为光栅，打印的页面上的所有内容。 这意味着，纵向页面镜像左到右;横向页面是镜像的上到下。</p>
<p>此属性是最适用于打印透明胶片或背面打印胶片。</p></td>
<td><p>可选。 默认值是<strong>FALSE</strong>。</p>
<p>此属性是可重定位的全局属性。 它可能显示为根级别属性 (请参阅<a href="root-level-only-attributes.md" data-raw-source="[Root-Level-Only Attributes](root-level-only-attributes.md)">Root-Level-Only 属性</a>) 时有没有配置依赖关系，或它可能会显示与 * 选项或 * 用例构造根据每个媒体类型。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>MoveToX0BeforeSetColor?</strong></p></td>
<td><p><strong>TRUE</strong>或<strong>FALSE</strong>，以指示是否将光标的 x 坐标必须设置为零才能将发送显式颜色选择命令。</p></td>
<td><p>可选。 如果未指定，默认值是<strong>FALSE</strong>。 可以是<strong>，则返回 TRUE</strong>仅当<em> <strong>UseExpColorSelectCmd？</strong>也<strong>TRUE</strong>。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>OptimizeLeftBound?</strong></p></td>
<td><p><strong>TRUE</strong>或<strong>FALSE</strong>，以指示 Unidrv 是否应删除左侧空白绑定的每个带区。</p></td>
<td><p>可选。 如果未指定，默认值是<strong>FALSE</strong>。</p></td>
</tr>
<tr class="even">
<td><p><em><strong>OutputDataFormat</strong></p></td>
<td><p>H_BYTE 或 V_BYTE，指示数据字节中的位将映射到像素水平或垂直像素。</p></td>
<td><p>可选。 如果未指定，默认值将为 H_BYTE。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>PreAnalysisOptions</strong></p></td>
<td><p>数字值，其中一个 0、 1、 2、 4 或 8。</p>
<p>每个特性参数的含义的信息，请参阅<a href="preanalysis-infrastructure.md" data-raw-source="[Preanalysis Infrastructure](preanalysis-infrastructure.md)">Preanalysis 基础结构</a>。</p></td>
<td><p>可选。 如果未指定，默认值为 1。</p></td>
</tr>
<tr class="even">
<td><p><em><strong>RasterSendAllData?</strong></p></td>
<td><p><strong>TRUE</strong>或<strong>FALSE</strong>，以指示是否应将 Unidrv 发送所有光栅数据，包括空白扫描行和扫描行中的空白。</p></td>
<td><p>可选。 如果未指定，默认值是<strong>FALSE</strong>。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>SendMultipleRows?</strong></p></td>
<td><p><strong>TRUE</strong>或<strong>FALSE</strong>，以指示是否指定 CmdSendBlockData 的命令可以发送多个阻止一次。</p></td>
<td></td>
</tr>
<tr class="even">
<td><p><em><strong>StripBlanks</strong></p></td>
<td><p>指示应去除光栅数据块中的空格的列表。 可以是一种或多种：</p>
领先的封闭尾随</td>
<td><p>可选。 如果未指定，Unidrv 不去除任何空格。 另请参阅 *<strong>MinStripBlankPixels</strong>中<a href="option-attributes-for-the-resolution-feature.md" data-raw-source="[Option Attributes for the Resolution Feature](option-attributes-for-the-resolution-feature.md)">解析功能的选项属性</a>。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>UseExpColorSelectCmd?</strong></p></td>
<td><p><strong>TRUE</strong>或<strong>FALSE</strong>，与颜色光栅数据分开的该值指示打印机是否需要显式颜色选择命令。</p></td>
<td><p>可选。 如果未指定，默认值是<strong>FALSE</strong>。 点阵打印机需要的值<strong>，则返回 TRUE</strong>。</p></td>
</tr>
</tbody>
</table>

 

有关光栅数据发出与关联的命令的信息，请参阅[光栅数据发出命令](raster-data-emission-commands.md)。

有关示例，请参阅[示例 GPD 文件](sample-gpd-files.md)。

 

 





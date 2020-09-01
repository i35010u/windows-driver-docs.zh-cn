---
title: 色彩模式功能的选项属性
description: 色彩模式功能的选项属性
ms.assetid: e6f68a50-f044-406e-b92c-8449d126bceb
keywords:
- ColorMode 功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51209ca2740b4bf929d8c7ca98ce0405956bdf1d
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217440"
---
# <a name="option-attributes-for-the-colormode-feature"></a>色彩模式功能的选项属性





下表列出了与 ColorMode 功能相关的属性。 有关 ColorMode 功能的详细信息，请参阅 [标准功能](standard-features.md)。

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
<td><p><em><strong>颜色？</strong></p></td>
<td><p><strong>TRUE</strong> 或 <strong>FALSE</strong>，指示选项是否生成颜色。</p></td>
<td><p>可选。 如果未指定，则 *<strong>DrvBPP</strong> 1 的默认值为<strong>TRUE</strong> &gt; 。 若要创建灰色缩放，请将 *<strong>DrvBPP</strong> 1 设置为<strong>FALSE</strong> &gt; 。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>ColorPlaneOrder</strong></p></td>
<td><p>指示 Unidrv 应发送颜色平面数据的顺序的列表。</p>
<p>示例：</p>
列出 (黄色、洋红色、青色、黑色) 列表 (红色、绿色、蓝色) 
<p>可在列表中重复颜色。</p></td>
<td><p>如果 <em> <strong>DevNumOfPlanes</strong>大于1，则为必需。 指定的颜色数必须等于 *<strong>DevNumOfPlanes</strong>。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>DevBPP</strong></p></td>
<td><p>数值，表示打印机支持的彩色数据的位数。</p></td>
<td><p>可选。 如果未指定，则默认值为1。</p></td>
</tr>
<tr class="even">
<td><p><em><strong>DevNumOfPlanes</strong></p></td>
<td><p>数值，表示打印机支持的颜色平面的数量。</p></td>
<td><p>可选。 如果未指定，则默认值为1。 为彩色打印机 (，值1称为像素模式。 ) </p></td>
</tr>
<tr class="odd">
<td><p></em><strong>DrvBPP</strong></p></td>
<td><p>数值，指示 Unidrv 应用于其位图呈现缓冲区的每个像素位数。 位图格式是与 Windows <a href="https://docs.microsoft.com/windows-hardware/drivers/#wdkgloss-device-independent-bitmap--dib-" data-raw-source="&lt;em&gt;device-independent bitmap (DIB)&lt;/em&gt;"><em>设备无关的位图 (DIB) </em></a>，有效值为1、4、8、16、24或32。</p></td>
<td><p>可选。 如果未指定，则默认值为1。 为彩色打印机 (，值1称为 "平面模式"。 ) </p>
<p>Windows Dib 始终使用一种颜色平面。</p></td>
</tr>
<tr class="even">
<td><p><em><strong>IPCallbackID</strong></p></td>
<td><p>正数值，传递给呈现插件的 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-imageprocessing" data-raw-source="[&lt;strong&gt;IPrintOemUni::ImageProcessing&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-imageprocessing)"><strong>IPrintOemUni：： ImageProcessing</strong></a> 方法作为其 <strong>IPCallbackID</strong> 参数。</p></td>
<td><p>如果提供了包含<strong>IPrintOemUni：： ImageProcessing</strong>方法的<a href="rendering-plug-ins.md" data-raw-source="[rendering plug-in](rendering-plug-ins.md)">呈现插件</a>，则是必需的。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>PaletteProgrammable?</strong></p></td>
<td><p><strong>TRUE</strong> 或 <strong>FALSE</strong>，指示调色板是否为可编程调色板。</p></td>
<td><p>可选。 如果未指定，则默认值为 <strong>FALSE</strong>。</p></td>
</tr>
<tr class="even">
<td><p><em><strong>PaletteSize</strong></p></td>
<td><p>数值，表示调色板中与指定选项一起使用的条目数。</p></td>
<td><p>可选。 如果未指定，则默认值为2。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>RasterMode</strong></p></td>
<td><p>直接或索引，指示是将光栅数据直接发送到打印机还是通过调色板编制索引。</p></td>
<td><p>可选。 如果未指定，则对默认值进行索引。</p></td>
</tr>
</tbody>
</table>

 

有关示例，请参阅 [示例 GPD 文件](sample-gpd-files.md)。

有关其他选项属性的信息，请参阅 [所有功能的选项属性](option-attributes-for-all-features.md)。

另请参阅 [控制图像质量](controlling-image-quality.md)。

 


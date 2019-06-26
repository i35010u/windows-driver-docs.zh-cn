---
title: 色彩模式功能的选项属性
description: 色彩模式功能的选项属性
ms.assetid: e6f68a50-f044-406e-b92c-8449d126bceb
keywords:
- ColorMode 功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3080bdf44a9e1bc5eb9c603f27753c988e666c9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385959"
---
# <a name="option-attributes-for-the-colormode-feature"></a>色彩模式功能的选项属性





下表列出了与 ColorMode 功能相关联的属性。 有关 ColorMode 功能的详细信息，请参阅[标准功能](standard-features.md)。

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
<td><p><em><strong>颜色？</strong></p></td>
<td><p><strong>TRUE</strong>或<strong>FALSE</strong>，以指示是否选项将生成颜色。</p></td>
<td><p>可选。 如果未指定，默认值是<strong>，则返回 TRUE</strong>为 *<strong>DrvBPP</strong> &gt; 1。 若要创建灰色缩放，将设置为<strong>FALSE</strong>使用 *<strong>DrvBPP</strong> &gt; 1。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>ColorPlaneOrder</strong></p></td>
<td><p>指示 Unidrv 应在其中发送颜色平面数据的顺序的列表。</p>
<p>示例：</p>
列表 （黄色、 洋红、 蓝绿色、 黑色） 的列表 （红色、 绿色、 蓝色）
<p>可以在列表中重复使用颜色。</p></td>
<td><p>需要<em> <strong>DevNumOfPlanes</strong>大于 1。 指定的颜色数必须等于 *<strong>DevNumOfPlanes</strong>。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>DevBPP</strong></p></td>
<td><p>数字值，该值指示打印机支持的颜色数据的每个像素的比特数。</p></td>
<td><p>可选。 如果未指定，默认值为 1。</p></td>
</tr>
<tr class="even">
<td><p><em><strong>DevNumOfPlanes</strong></p></td>
<td><p>数字值，该值指示打印机支持的颜色平面数。</p></td>
<td><p>可选。 如果未指定，默认值为 1。 （有关彩色打印机的值为 1 称为像素模式。）</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>DrvBPP</strong></p></td>
<td><p>数字值，该值指示每个像素 Unidrv 应为其位图呈现缓冲区使用的比特数。 位图格式是 Windows <a href="https://docs.microsoft.com/windows-hardware/drivers/#wdkgloss-device-independent-bitmap--dib-" data-raw-source="&lt;em&gt;device-independent bitmap (DIB)&lt;/em&gt;"><em>与设备无关位图 (DIB)</em></a>，和有效的值为 1、 4、 8、 16、 24、 或 32。</p></td>
<td><p>可选。 如果未指定，默认值为 1。 （有关彩色打印机的值为 1 被称为"平面模式"。）</p>
<p>Windows Dib 始终使用一个颜色平面。</p></td>
</tr>
<tr class="even">
<td><p><em><strong>IPCallbackID</strong></p></td>
<td><p>传递给呈现插件的正数值的值<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuni-imageprocessing" data-raw-source="[&lt;strong&gt;IPrintOemUni::ImageProcessing&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuni-imageprocessing)"> <strong>IPrintOemUni::ImageProcessing</strong> </a>方法作为其<strong>IPCallbackID</strong>参数。</p></td>
<td><p>需要<a href="rendering-plug-ins.md" data-raw-source="[rendering plug-in](rendering-plug-ins.md)">呈现插件</a>提供，其中包含<strong>IPrintOemUni::ImageProcessing</strong>方法。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>PaletteProgrammable?</strong></p></td>
<td><p><strong>TRUE</strong>或<strong>FALSE</strong>，以指示是否是可编程的调色板。</p></td>
<td><p>可选。 如果未指定，默认值是<strong>FALSE</strong>。</p></td>
</tr>
<tr class="even">
<td><p><em><strong>PaletteSize</strong></p></td>
<td><p>表示与指定的选项一起使用的调色板中的条目数的数字值。</p></td>
<td><p>可选。 如果未指定，默认值为 2。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>RasterMode</strong></p></td>
<td><p>直接或索引，以指示是否光栅数据直接发送到打印机，或通过颜色面板索引。</p></td>
<td><p>可选。 如果未指定，默认值编制索引。</p></td>
</tr>
</tbody>
</table>

 

有关示例，请参阅[示例 GPD 文件](sample-gpd-files.md)。

有关其他选项的属性的信息，请参阅[所有功能的选项属性](option-attributes-for-all-features.md)。

另请参阅[控制图像质量](controlling-image-quality.md)。

 

 





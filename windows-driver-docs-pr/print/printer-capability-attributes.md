---
title: 打印机功能属性
description: 打印机功能属性
keywords:
- 打印机功能属性 WDK Unidrv
- 常规打印机属性 WDK Unidrv，打印机功能
- 功能属性 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 90b3cb40fda51fbec43bfcd9d4878bf52f55c475
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807359"
---
# <a name="printer-capability-attributes"></a>打印机功能属性





打印机功能属性是 [常规打印属性](general-printing-attributes.md) ，用于将诸如页面边距、旋转和文本打印功能等打印机特征指定为影响所有纸张大小和方向。

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
<td><p><em><strong>MemoryUsage</strong></p></td>
<td><p></p>
指示存储在打印机内存中的数据类型的常量列表。 可以是以下一个或多个：字体光栅向量
<p>如果列出了数据类型但打印机不支持该数据类型，则会将其忽略。</p></td>
<td><p>可选。 如果未指定，则默认值为 LIST (字体、光栅、矢量) 。 有关详细信息，请参阅 <a href="describing-printer-memory-configurations.md" data-raw-source="[Describing Printer Memory Configurations](describing-printer-memory-configurations.md)">描述打印机内存配置</a>。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>OEMCustomData</strong></p></td>
<td><p>在调用 IPrintOemDriverUni 时，要提供给 <a href="rendering-plug-ins.md" data-raw-source="[rendering plug-in](rendering-plug-ins.md)">呈现插件</a> 的带引号的文本字符串 <a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvgetgpddata" data-raw-source="[&lt;strong&gt;IPrintOemDriverUni::DrvGetGPDData&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvgetgpddata)"><strong>：:D rvgetgpddata</strong></a>。</p></td>
<td><p>如果呈现插件调用 <strong>IPrintOemDriverUni：:D rvgetgpddata</strong>，则是必需的。</p>
<p>文本字符串内容的解释由呈现插件决定。</p>
<p>此属性是可重定位的全局属性;它可能位于根级别 (查看) 的 <a href="root-level-only-attributes.md" data-raw-source="[Root-Level-Only Attributes](root-level-only-attributes.md)">仅限根级别的属性</a> ，表示它不依赖于打印机配置，或者，如果存在某种依赖项，则它可能会随 <em> 选项或 * 用例构造出现。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>OutputOrderReversed?</strong></p></td>
<td><p><strong>TRUE</strong> 或 <strong>FALSE</strong>，指示是否从最后一页向第一页排序多页文档。</p></td>
<td><p>可选。 如果未指定，则默认值为 <strong>FALSE</strong>。</p>
<p>EXTERN_GLOBAL 符号不应用于 <em> <strong>OutputOrderReversed？</strong>。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>ReselectFont</strong></p></td>
<td><p></p>
常量列表，指示操作之后 Unidrv 必须重新选择当前字体。 可以是以下内容： AFTER_GRXDATA-CmdSend<em>Xxxx</em><a href="raster-data-emission-commands.md" data-raw-source="[raster data emission commands](raster-data-emission-commands.md)">数据的任何数据的</a>
AFTER_XMOVE 在任何 x 移动 <a href="cursor-commands.md" data-raw-source="[cursor commands](cursor-commands.md)">游标命令</a>之后。
AFTER_FF CmdFF 命令后。</td>
<td><p>可选。 如果未指定，则 Unidrv 不会重新选择字体。</p></td>
</tr>
<tr class="odd">
<td><p><em><strong>ReverseBandOrderForEvenPages?</strong></p></td>
<td><p><strong>TRUE</strong> 或 <strong>FALSE</strong>，指示是否启用反向条带。 此属性用于支持具有自动双工功能的打印机;也就是说，能够在纸张的两面上进行打印的打印机。</p>
<p>此表的后面部分包含详细信息。</p></td>
<td><p>此属性的默认值为 <strong>FALSE</strong>。 将此特性设置为 <strong>TRUE</strong> 可启用反向分级顺序。</p>
<p>此属性是可重定位的全局属性;它可能位于根级别 (查看) 的 <a href="root-level-only-attributes.md" data-raw-source="[Root-Level-Only Attributes](root-level-only-attributes.md)">仅限根级别的属性</a> ，表示它不依赖于打印机配置，或者，如果存在某种依赖关系，则它可能与 * Option 或 * Case 构造出现在一起。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>RotateCoordinate?</strong></p></td>
<td><p><strong>TRUE</strong> 或 <strong>FALSE</strong>，指示打印机是否支持命令旋转坐标系以匹配页面方向。</p></td>
<td><p>可选。 如果未指定，则默认值为 <strong>FALSE</strong>。 如果 <strong>为 TRUE</strong>，则 <em> "方向" 功能的选项项必须指定打印机命令。 不能放置在<a href="conditional-statements.md" data-raw-source="[&lt;/em&gt;Case](conditional-statements.md)"> </em> Case</a>条目中。</p></td>
</tr>
<tr class="odd">
<td><p><em><strong>RotateFont?</strong></p></td>
<td><p><strong>TRUE</strong> 或 <strong>FALSE</strong>，指示打印机是否自动旋转字体以匹配页面方向。</p></td>
<td><p>可选。 如果未指定，则默认值为 <strong>FALSE</strong>。 如果 <strong>为 true</strong>，则 *<strong>RotateCoordinate？</strong> 也必须为 <strong>true</strong>。 不能置于 * Case 条目中。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>RotateRaster?</strong></p></td>
<td><p><strong>TRUE</strong> 或 <strong>FALSE</strong>，指示打印机是否自动旋转光栅数据以匹配页面方向。</p></td>
<td><p>可选。 如果未指定，则默认值为 <strong>FALSE</strong>。 如果<strong>为 true</strong>，则 <em> <strong>RotateCoordinate？</strong>也必须为<strong>true</strong>。 不能置于 * Case 条目中。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>TextCaps</strong></p></td>
<td><p>指示打印机文本功能的常数列表。 可以包含 Microosft Windows SDK 文档的<strong>GetDeviceCaps</strong>说明中描述的一个或多个 TC_<em>xxx</em>标志。</p></td>
<td><p>可选。 如果未指定，Unidrv 将假定不支持任何文本功能。</p></td>
</tr>
</tbody>
</table>

 

有关示例，请参阅 [示例 GPD 文件](sample-gpd-files.md)。

### <a name="additional-information-about-reversebandorderforevenpages"></a><a href="" id="additional-information-about--reversebandorderforevenpages-"></a>有关 ReverseBandOrderForEvenPages 的其他信息 \* ？

自动双工功能的副作用是，刚刚打印的页面的下边缘将回送到打印机，以成为下一页的上边缘。 若要保持第二页相对于第一个页面的方向，必须以相反顺序向打印机发送第二页的光栅图像。 换而言之，如果打印机首先发送顶部扫描行来打印正面，则必须先打印后侧下扫描行。

当 \* **ReverseBandOrderForEvenPages** 为 **TRUE** 且双工处于开启时，Unidrv 将按偶数 (页的反向顺序枚举每个带区，以使偶数页) 的背面。 OEM 呈现插件需要在将数据发送到打印机之前仅缓存一个数据带区。 不会反转每个带区内的扫描行的顺序，因此插件仍必须处理该任务，并且还必须反转每个扫描行中的位的顺序。 虽然这是插件额外的工作，但优点在于插件不需要缓存任何光栅数据，并且可以立即开始将数据发送到打印机。

**注意** \*仅当 "双面打印" 设置为 "长边翻转" 时才计算 *_ReverseBandOrderForEvenPages？_* 属性。 当双工设置为 "短边翻转" 时，将忽略此属性。

 

" \* *_ReverseBandOrderForEvenPages"_* 属性的值和驱动程序模拟的旋转都将影响对带区的枚举方式，如下表所示。 如果 "ReverseBandOrderForEvenPages" 为 True，并且选择了 "双工"，则在列中 **指定的带** 区枚举顺序适用 \* *_ReverseBandOrderForEvenPages?_* ，并且要打印的页面为第二个 (或 "后) 端"。 **TRUE** 否则，将应用带有 " **FALSE** " 的列。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>Driver-Simulated 旋转</th>
<th><strong>TRUE</strong> 和偶数页</th>
<th><strong>FALSE</strong> 或奇数页</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CCW_ROTATE90</p></td>
<td><p>SW_LTOR</p></td>
<td><p>SW_RTOL</p></td>
</tr>
<tr class="even">
<td><p>CCW_ROTATE270</p></td>
<td><p>SW_RTOL</p></td>
<td><p>SW_LTOR</p></td>
</tr>
<tr class="odd">
<td><p>无旋转</p></td>
<td><p>SW_UP</p></td>
<td><p>SW_DOWN</p></td>
</tr>
</tbody>
</table>

 

图例： SW \_ LTOR = 从左到右，软件 \_ RTOL = 从右到左，软件 \_ 启动 = 从下到上，软件关闭 = 从 \_ 上到下。

OEM 呈现插件可以支持自动双面打印，而无需使用 \* *_ReverseBandOrderForEvenPages？_* 属性。 此插件只需缓存整个页面的所有数据并将其发送到打印机（从底部扫描行开始）即可。 此扫描行以及该页上的所有其他行都必须按相反的顺序发送。

**注意**   在将数据发送到打印机时，OEM 呈现插件负责为每个扫描行反转位的顺序，以及每个带区的扫描行的顺序。 若要确定何时必须完成此操作，可以通过使用索引 SVI PageNumber 调用 [**IPrintOemDriverUni：:D rvgetstandardvariable**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvgetstandardvariable)来获取 PageNumber 标准变量的值 \_ 。 如果页码为奇数，则无需反转。 如果数字为偶数并且选择了双工，则需要进行反向。

 


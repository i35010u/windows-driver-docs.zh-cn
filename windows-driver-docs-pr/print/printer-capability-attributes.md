---
title: 打印机功能属性
description: 打印机功能属性
ms.assetid: 3ee98eee-8f46-4bf0-ac2c-f47f8402fa86
keywords:
- 打印机功能特性 WDK Unidrv
- 常规打印机属性 WDK Unidrv，打印机功能
- 功能属性 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3eefb56f0fc8d4f93c6b7d370972197e986141c6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380533"
---
# <a name="printer-capability-attributes"></a>打印机功能属性





打印机功能属性[常规打印属性](general-printing-attributes.md)，用于指定此类打印机特征作为页边距、 旋转和文本会影响所有纸张大小和方向的打印功能。

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
<td><p><em><strong>MemoryUsage</strong></p></td>
<td><p></p>
常数来指示打印机内存中存储的数据类型的列表。 可以是一种或多种：字体光栅向量
<p>如果数据类型是列出，但不是支持的打印机，则忽略它。</p></td>
<td><p>可选。 如果未指定，默认值将为列表 （字体，光栅，矢量）。 有关详细信息，请参阅<a href="describing-printer-memory-configurations.md" data-raw-source="[Describing Printer Memory Configurations](describing-printer-memory-configurations.md)">描述打印机内存配置</a>。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>OEMCustomData</strong></p></td>
<td><p>带引号的文本字符串要提供给<a href="rendering-plug-ins.md" data-raw-source="[rendering plug-in](rendering-plug-ins.md)">呈现插件</a>当调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff553128" data-raw-source="[&lt;strong&gt;IPrintOemDriverUni::DrvGetGPDData&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553128)"> <strong>IPrintOemDriverUni::DrvGetGPDData</strong></a>。</p></td>
<td><p>如果呈现插件调用所需<strong>IPrintOemDriverUni::DrvGetGPDData</strong>。</p>
<p>文本字符串内容的解释取决于插件的呈现。</p>
<p>此属性是可重定位的全局属性;可能会将它放置在根级别 (请参阅<a href="root-level-only-attributes.md" data-raw-source="[Root-Level-Only Attributes](root-level-only-attributes.md)">Root-Level-Only 特性</a>) 以表示它不依赖于对打印机配置，或可能会与一起<em>选项或 * 用例构造是否存在一些依赖关系。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>OutputOrderReversed?</strong></p></td>
<td><p><strong>TRUE</strong>或<strong>FALSE</strong>，以指示是否多页文档按从最后一页到第一个。</p></td>
<td><p>可选。 如果未指定，默认值是<strong>FALSE</strong>。</p>
<p>不应与使用 EXTERN_GLOBAL 符号<em> <strong>OutputOrderReversed？</strong>。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>ReselectFont</strong></p></td>
<td><p></p>
常数来指示的操作在其后 Unidrv 必须重新选择当前字体的列表。 可以是以下值：AFTER_GRXDATA-之后任何 CmdSend<em>Xxxx</em>数据<a href="raster-data-emission-commands.md" data-raw-source="[raster data emission commands](raster-data-emission-commands.md)">光栅数据发出命令</a>。
AFTER_XMOVE-任何 x 移动后的<a href="cursor-commands.md" data-raw-source="[cursor commands](cursor-commands.md)">游标命令</a>。
AFTER_FF-CmdFF 的命令。</td>
<td><p>可选。 如果未指定，因此 Unidrv 都不重新选择字体。</p></td>
</tr>
<tr class="odd">
<td><p><em><strong>ReverseBandOrderForEvenPages?</strong></p></td>
<td><p><strong>TRUE</strong>或<strong>FALSE</strong>，以指示是否启用反向条带。 此属性用于通过自动双工功能; 支持的打印机也就是说，可以打印一张纸的两面上的打印机。</p>
<p>此表后面的部分包含的详细信息。</p></td>
<td><p>此属性的默认值是<strong>FALSE</strong>。 此属性设置为<strong>，则返回 TRUE</strong>启用反向具有带区的顺序。</p>
<p>此属性是可重定位的全局属性;可能会将它放置在根级别 (请参阅<a href="root-level-only-attributes.md" data-raw-source="[Root-Level-Only Attributes](root-level-only-attributes.md)">Root-Level-Only 属性</a>) 以表示它不依赖于对打印机配置，或可能会与一起 * 选项或 * 用例构造是否存在一些依赖关系。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>RotateCoordinate?</strong></p></td>
<td><p><strong>TRUE</strong>或<strong>FALSE</strong>，以指示打印机是否支持命令旋转坐标系统以匹配页面方向。</p></td>
<td><p>可选。 如果未指定，默认值是<strong>FALSE</strong>。 如果<strong>，则返回 TRUE</strong>，<em>定向功能，必须指定打印机命令选项的条目。 不能置于<a href="conditional-statements.md" data-raw-source="[&lt;/em&gt;Case](conditional-statements.md)"></em>用例</a>条目。</p></td>
</tr>
<tr class="odd">
<td><p><em><strong>RotateFont?</strong></p></td>
<td><p><strong>TRUE</strong>或<strong>FALSE</strong>，以指示打印机是否自动轮换字体以匹配页面方向。</p></td>
<td><p>可选。 如果未指定，默认值是<strong>FALSE</strong>。 如果<strong>，则返回 TRUE</strong>，然后 *<strong>RotateCoordinate？</strong>还必须<strong>TRUE</strong>。 不能放在 * Case 条目。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>RotateRaster?</strong></p></td>
<td><p><strong>TRUE</strong>或<strong>FALSE</strong>，以指示打印机是否自动轮换光栅数据，以匹配页面方向。</p></td>
<td><p>可选。 如果未指定，默认值是<strong>FALSE</strong>。 如果<strong>，则返回 TRUE</strong>，然后<em> <strong>RotateCoordinate？</strong>也必须<strong>TRUE</strong>。 不能放在 * Case 条目。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>TextCaps</strong></p></td>
<td><p>常数来指示打印机的文本功能的列表。 可以包含一个或多个 TC_<em>xxx</em>获得有关 Microosft Windows SDK 文档的说明中所述的标志<strong>GetDeviceCaps</strong>。</p></td>
<td><p>可选。 如果未指定，Unidrv 假定没有文本功能支持。</p></td>
</tr>
</tbody>
</table>

 

有关示例，请参阅[示例 GPD 文件](sample-gpd-files.md)。

### <a href="" id="additional-information-about--reversebandorderforevenpages-"></a>有关其他信息\*ReverseBandOrderForEvenPages？

自动双工能力的一个副作用是页的页面的，只需打印的下边缘反馈到打印机，进入下一步的上边缘。 若要维护的方向相对于第一个的第二页，第二个页的光栅图像必须发送到打印机按相反的顺序。 换而言之，如果打印机打印的第一次发送前扫描行前端，它必须首先打印后端底部扫描行。

当\* **ReverseBandOrderForEvenPages？** 是**TRUE**和双工是上、 Unidrv 枚举每个带区按相反的顺序为偶数的页面 （的奇数页正反两面）。 OEM 呈现插件需要将其发送到打印机之前缓存的数据只有一个带区。 不会反转扫描行中每个带区的顺序，该插件仍必须处理该任务中，因此它也必须撤消每个扫描行中的位的顺序。 虽然这是插件的额外工作，但优点是，该插件不需要缓存光栅的任何数据，可以开始将数据立即发送到打印机。

**请注意**   \* **ReverseBandOrderForEvenPages？** 仅在进行双面打印设置为"长边翻转"计算属性。 当进行双面打印设置为"短边翻转"时，将忽略此属性。

 

值\* **ReverseBandOrderForEvenPages？** 属性和枚举的方法带区下, 表中所示的驱动程序模拟旋转影响。 带区的枚举顺序中的列指定探究 **，则返回 TRUE**时适用\* **ReverseBandOrderForEvenPages？** 是**TRUE**，和双工是选择，而该页要打印的第二个 （或后） 端。 否则列探究**FALSE**适用。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>驱动程序模拟旋转</th>
<th><strong>TRUE</strong> ，甚至页</th>
<th><strong>FALSE</strong>或奇数页</th>
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
<td><p>没有旋转</p></td>
<td><p>SW_UP</p></td>
<td><p>SW_DOWN</p></td>
</tr>
</tbody>
</table>

 

图例：SW\_LTOR = 从左到右，SW\_RTOL = 右到左，SW\_最多 = 底部到顶部，SW\_上到下按下 =。

呈现插件的 OEM 可以支持自动进行双面打印，而无需使用\* **ReverseBandOrderForEvenPages？** 属性。 该插件可以这样做只需缓存的所有数据的整个页面，并将其发送到打印机，从底部扫描行开始。 扫描行中，以及所有其他该页面上，必须按相反的顺序发送。

**请注意**  呈现插件的 OEM 负责反转的位与每个扫描行的顺序和每个带区扫描行的顺序，如将数据发送到打印机。 若要确定必须完成这的时，PageNumber 标准变量的值可以通过调用获取[ **IPrintOemDriverUni::DrvGetStandardVariable**](https://msdn.microsoft.com/library/windows/hardware/ff553129)，使用索引 SVI\_PAGENUMBER。 如果页数字为奇数，则需要不反转。 如果数字为偶数，并选择双面打印时，需要进行反转。

 

 

 





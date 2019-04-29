---
title: 标准变量
description: 标准变量
ms.assetid: d3f85c0f-7387-4301-8b1e-904471aed4b0
keywords:
- GPD 文件条目 WDK Unidrv，标准变量
- 变量 WDK GPD 文件
- 标准变量 WDK GPD 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22d19d4fd97a53252283a725f635876d166a8607
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375187"
---
# <a name="standard-variables"></a>标准变量





GPD 语言定义一组标准可以使用的命令字符串中引用的变量[命令字符串格式](command-string-format.md)。 Unidrv 驱动程序将值分配给这些变量。 从 GPD 文件的角度来说，变量是只读的。

标准的所有变量都作为双字节整数都存储。

以下[打印机命令](printer-commands.md)条目指定的命令字符串发送到 4 个 P HP LaserJet 光栅数据块的准备就绪后：

```cpp
*Command: CmdSendBlockData: "<1B>*b" %d{NumOfDataBytes} "W"
```

下表包含所有标准变量，按字母顺序。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>标准变量名称</th>
<th>ReplTest1</th>
<th>备注</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>BlueValue</strong></p></td>
<td><p>当前颜色中蓝色分量。</p></td>
<td><p>用在 CmdDefinePaletteEntry 命令字符串中有效。 (另请参阅<strong>GreenValue</strong>， <strong>RedValue</strong>。)</p></td>
</tr>
<tr class="even">
<td><p><strong>CurrentFontID</strong></p></td>
<td><p>当前已下载的软字体的标识号。</p></td>
<td><p>如果当前打印作业包含已下载的软字体，有效。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CurrentPaletteIndex</strong></p></td>
<td><p>调色板中的当前索引。</p></td>
<td><p>用在 CmdSelectPaletteEntry 命令字符串中有效。 (另请参阅<strong>GreenValue</strong>， <strong>RedValue</strong>。)</p></td>
</tr>
<tr class="even">
<td><p><strong>CursorOriginX</strong></p></td>
<td><p>以主单位表示光标原点的 x 坐标。</p></td>
<td><p>每当打印作业正在进行中时有效。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CursorOriginY</strong></p></td>
<td><p>以主单位表示光标原点的 Y 坐标。</p></td>
<td><p>每当打印作业正在进行中时有效。</p></td>
</tr>
<tr class="even">
<td><p><strong>DestX</strong></p></td>
<td><p>游标目标，以 master 为单位，相对于游标原点的 x 坐标。</p></td>
<td><p>用在 CmdXMoveAbsolute 命令字符串中有效。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DestXRel</strong></p></td>
<td><p>游标目标，以 master 为单位，相对于当前光标的 X 坐标位置。</p></td>
<td><p>用在 CmdXMoveRelLeft 和 CmdXMoveRelRight 命令字符串中有效。</p></td>
</tr>
<tr class="even">
<td><p><strong>DestY</strong></p></td>
<td><p>游标目标，以 master 为单位，相对于游标原点的 Y 坐标。</p></td>
<td><p>用在 CmdYMoveAbsolute 命令字符串中有效。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DestYRel</strong></p></td>
<td><p>游标目标，以 master 为单位，相对于当前游标位置的 Y 坐标。</p></td>
<td><p>用在 CmdYMoveRelUp 和 CmdYMoveRelDown 命令字符串中有效。</p></td>
</tr>
<tr class="even">
<td><p><strong>FontBold</strong></p></td>
<td><p>如果当前的字体为粗体，则设置为一个或零否则。</p></td>
<td><p>指定一种字体时有效。</p></td>
</tr>
<tr class="odd">
<td><p><strong>FontHeight</strong></p></td>
<td><p>采用主单位的当前字体的高度。</p></td>
<td><p>指定一种字体时有效。</p></td>
</tr>
<tr class="even">
<td><p><strong>FontItalic</strong></p></td>
<td><p>如果当前字体为斜体，则为零; 否则为，设置为一个。</p></td>
<td><p>指定一种字体时有效。</p></td>
</tr>
<tr class="odd">
<td><p><strong>FontMaxWidth</strong></p></td>
<td><p>该字体中设置为所有标志符号的最大字符增量。</p></td>
<td><p>指定一种字体时有效。</p></td>
</tr>
<tr class="even">
<td><p><strong>FontStrikeThru</strong></p></td>
<td><p>如果启用删除线的当前字体，则为零; 否则为，设置为一个。</p></td>
<td><p>指定一种字体时有效。</p></td>
</tr>
<tr class="odd">
<td><p><strong>FontUnderLine</strong></p></td>
<td><p>设置当前字体带下划线，如果一个或零; 否则为。</p></td>
<td><p>指定一种字体时有效。</p></td>
</tr>
<tr class="even">
<td><p><strong>FontWidth</strong></p></td>
<td><p>中的当前字体主单位的宽度。</p></td>
<td><p>指定一种字体时有效。</p></td>
</tr>
<tr class="odd">
<td><p><strong>GraphicsXRes</strong></p></td>
<td><p>图形，以 dpi 为单位的当前水平分辨率。</p></td>
<td><p>每当打印作业正在进行中时有效。</p></td>
</tr>
<tr class="even">
<td><p><strong>GraphicsYRes</strong></p></td>
<td><p>当前垂直分辨率的图形，以 dpi 为单位。</p></td>
<td><p>每当打印作业正在进行中时有效。</p></td>
</tr>
<tr class="odd">
<td><p><strong>GrayPercentage</strong></p></td>
<td><p>灰色级别 （百分比） 要用于灰色填充。</p></td>
<td><p>用在 CmdRectGrayFill 命令字符串中有效。</p></td>
</tr>
<tr class="even">
<td><p><strong>GreenValue</strong></p></td>
<td><p>当前颜色中绿色分量。</p></td>
<td><p>用在 CmdDefinePaletteEntry 命令字符串中有效。 (另请参阅<strong>BlueValue</strong>， <strong>RedValue</strong>。)</p></td>
</tr>
<tr class="odd">
<td><p><strong>LinefeedSpacing</strong></p></td>
<td><p>垂直空间量，以主单元，它表示一个换行符。</p></td>
<td><p>用在 CmdSetLineSpacing 命令字符串中有效。</p></td>
</tr>
<tr class="even">
<td><p><strong>NextFontID</strong></p></td>
<td><p>要下载的下一步软字体的标识号。</p></td>
<td><p>用在 CmdSetFontID 命令字符串中有效。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NextGlyph</strong></p></td>
<td><p>若要下载的下一步的标志符号的双字节代码。</p></td>
<td><p>用在 CmdSetCharCode 命令字符串中有效。</p></td>
</tr>
<tr class="even">
<td><p><strong>NumOfCopies</strong></p></td>
<td><p>用户请求的副本数。</p></td>
<td><p>每当打印作业正在进行中时有效。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NumOfDataBytes</strong></p></td>
<td><p>光栅数据准备好进行传输的字节数。</p></td>
<td><p>可用于在任何 CmdSend<em>XXX</em>数据命令字符串。</p>
<p>如果压缩数据，值是压缩后的字节数。</p></td>
</tr>
<tr class="even">
<td><p><strong>PageNumber</strong></p></td>
<td><p>当前正在打印的页的页码。 请注意，这不会不一定对应于应用程序的页码，但而不是数乘以<a href="https://msdn.microsoft.com/library/windows/hardware/ff556281" data-raw-source="[&lt;em&gt;DrvSendPage&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556281)"> <em>DrvSendPage</em> </a>已调用。</p>
<p>此值初始化<a href="https://msdn.microsoft.com/library/windows/hardware/ff556296" data-raw-source="[&lt;strong&gt;DrvStartDoc&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556296)"> <strong>DrvStartDoc</strong> </a> ，并通过递增<strong>DrvSendPage</strong>。</p>
<p>例如，如果 N = 4 选择，则<strong>PageNumber</strong>仅当正在打印文档的第五个页时递增至 2。</p>
<p>再举一例，如果 （后至前） 按相反的顺序打印文档<strong>PageNumber</strong>标准变量仍报告作为第一页打印的第一页，即使这是文档的最后一页。</p>
<p>此行为需要适当地支持自动进行双面打印功能。</p>
<p>应使用 OEM <strong>PageNumber</strong>仅以确定当前页是否为前端或后端。</p></td>
<td><p>每当打印作业正在进行中时有效。</p></td>
</tr>
<tr class="odd">
<td><p><strong>PaletteIndexToProgram</strong></p></td>
<td><p>程序的下一个条目的颜色调色板中的索引。</p></td>
<td><p>用在 CmdDefinePaletteEntry 命令字符串中有效。 (另请参阅<strong>RedValue</strong>， <strong>GreenValue</strong>， <strong>BlueValue</strong>， <strong>CurrentPaletteIndex</strong>。)</p></td>
</tr>
<tr class="even">
<td><p><strong>PatternBrushID</strong></p></td>
<td><p>下载的模式画笔的标识号。</p></td>
<td><p>有效用于 CmdDownloadPattern 和 CmdSelectPattern 命令字符串。</p></td>
</tr>
<tr class="odd">
<td><p><strong>PatternBrushSize</strong></p></td>
<td><p>大小，以字节为单位的当前模式画笔。</p></td>
<td><p>有效用于 CmdDownloadPattern 命令字符串。</p></td>
</tr>
<tr class="even">
<td><p><strong>PatternBrushType</strong></p></td>
<td><p></p>
当前模式画笔类型。 值可以是：2：明暗度的模式 3:交叉阴影模式 4:用户定义的模式</td>
<td><p>有效用于 CmdDownloadPattern 和 CmdSelectPattern 命令字符串。</p></td>
</tr>
<tr class="odd">
<td><p><strong>PhysPaperLength</strong></p></td>
<td><p>纵向模式，以 y master 单位的长度当前正在使用纸张。</p></td>
<td><p>每当打印作业正在进行中时有效。</p></td>
</tr>
<tr class="even">
<td><p><strong>PhysPaperWidth</strong></p></td>
<td><p>纵向模式宽度，以主单位，表示当前正在使用的纸张。</p></td>
<td><p>每当打印作业正在进行中时有效。</p></td>
</tr>
<tr class="odd">
<td><p><strong>PrintDirInCCDegrees</strong></p></td>
<td><p>旋转，以度为单位按逆时针方向，测量的量。</p></td>
<td><p>在驱动程序将发送的 CmdSetSimpleRotation 或 CmdSetAnyRotation 命令字符串时有效。</p></td>
</tr>
<tr class="even">
<td><p><strong>RasterDataHeightInPixels</strong></p></td>
<td><p>以像素为单位表示的当前数据的图像的高度。</p></td>
<td><p>可用于在任何 CmdSend<em>XXX</em>数据命令字符串，并在 CmdSetSrcBmpHeight 命令字符串。 压缩不会修改此值。</p></td>
</tr>
<tr class="odd">
<td><p><strong>RasterDataWidthInBytes</strong></p></td>
<td><p>扫描行中包含的字节数。</p></td>
<td><p>可用于在任何 CmdSend<em>XXX</em>数据命令字符串，并在 CmdSetSrcBmpWidth 命令字符串。 压缩不会修改此值。</p></td>
</tr>
<tr class="even">
<td><p><strong>RectXSize</strong></p></td>
<td><p>矩形宽度，单位 x master。</p></td>
<td><p>用在 CmdSetRectWidth 命令字符串中有效。</p></td>
</tr>
<tr class="odd">
<td><p><strong>RectYSize</strong></p></td>
<td><p>矩形长度 （以 y master 为单位）。</p></td>
<td><p>用在 CmdSetRectHeight 命令字符串中有效。</p></td>
</tr>
<tr class="even">
<td><p><strong>RedValue</strong></p></td>
<td><p>当前颜色中红色分量。</p></td>
<td><p>用在 CmdDefinePaletteEntry 命令字符串中有效。 (另请参阅<strong>GreenValue</strong>， <strong>BlueValue</strong>。)</p></td>
</tr>
<tr class="odd">
<td><p><strong>TextXRes</strong></p></td>
<td><p>对于文本，以 dpi 为单位的当前水平分辨率。</p></td>
<td><p>每当打印作业正在进行中时有效。</p></td>
</tr>
<tr class="even">
<td><p><strong>TextYRes</strong></p></td>
<td><p>对于文本，以 dpi 为单位的当前垂直分辨率。</p></td>
<td><p>每当打印作业正在进行中时有效。</p></td>
</tr>
</tbody>
</table>

 

 

 





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
ms.openlocfilehash: 85b9f35dba3e62d360af1677ec95be29c1b710b6
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209245"
---
# <a name="standard-variables"></a>标准变量





GPD 语言定义一组标准变量，可以使用 [命令字符串格式](command-string-format.md)在命令字符串中引用这些变量。 Unidrv 驱动程序将值分配给这些变量。 从 GPD 文件的角度来看，变量是只读的。

所有标准变量均存储为 DWORD 整数。

以下 [打印机命令](printer-commands.md) 条目指定了在一个光栅数据块就绪时发送给 HP LaserJet 4P 的命令字符串：

```cpp
*Command: CmdSendBlockData: "<1B>*b" %d{NumOfDataBytes} "W"
```

下表按字母顺序包含所有标准变量。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>标准变量名称</th>
<th>值</th>
<th>注释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>BlueValue</strong></p></td>
<td><p>当前颜色的蓝色分量。</p></td>
<td><p>在 CmdDefinePaletteEntry 命令字符串中有效。  (另请参阅 <strong>GreenValue</strong>、 <strong>RedValue</strong>。 ) </p></td>
</tr>
<tr class="even">
<td><p><strong>CurrentFontID</strong></p></td>
<td><p>当前下载的软字体的标识号。</p></td>
<td><p>如果当前打印作业包含下载的软字体，则有效。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CurrentPaletteIndex</strong></p></td>
<td><p>调色板中的当前索引。</p></td>
<td><p>在 CmdSelectPaletteEntry 命令字符串中有效。  (另请参阅 <strong>GreenValue</strong>、 <strong>RedValue</strong>。 ) </p></td>
</tr>
<tr class="even">
<td><p><strong>CursorOriginX</strong></p></td>
<td><p>光标原点的 X 坐标，以主单位表示。</p></td>
<td><p>当打印作业正在进行时有效。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CursorOriginY</strong></p></td>
<td><p>光标原点的 Y 坐标（以主单位表示）。</p></td>
<td><p>当打印作业正在进行时有效。</p></td>
</tr>
<tr class="even">
<td><p><strong>DestX</strong></p></td>
<td><p>光标目标的 X 坐标，以主单位表示，相对于游标原点。</p></td>
<td><p>在 CmdXMoveAbsolute 命令字符串中有效。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DestXRel</strong></p></td>
<td><p>光标目标的 X 坐标，以主单位表示，相对于当前光标位置。</p></td>
<td><p>适用于 CmdXMoveRelLeft 和 CmdXMoveRelRight 命令字符串。</p></td>
</tr>
<tr class="even">
<td><p><strong>DestY</strong></p></td>
<td><p>光标目标的 Y 坐标，以主单位表示，相对于游标原点。</p></td>
<td><p>在 CmdYMoveAbsolute 命令字符串中有效。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DestYRel</strong></p></td>
<td><p>光标目标的 Y 坐标，以主单位表示，相对于当前光标位置。</p></td>
<td><p>适用于 CmdYMoveRelUp 和 CmdYMoveRelDown 命令字符串。</p></td>
</tr>
<tr class="even">
<td><p><strong>FontBold</strong></p></td>
<td><p>如果当前字体为粗体，则设置为 1; 否则设置为零。</p></td>
<td><p>指定字体时有效。</p></td>
</tr>
<tr class="odd">
<td><p><strong>FontHeight</strong></p></td>
<td><p>当前字体的高度（以主单位为单位）。</p></td>
<td><p>指定字体时有效。</p></td>
</tr>
<tr class="even">
<td><p><strong>FontItalic</strong></p></td>
<td><p>如果当前字体为斜体，则设置为 1; 否则设置为零。</p></td>
<td><p>指定字体时有效。</p></td>
</tr>
<tr class="odd">
<td><p><strong>FontMaxWidth</strong></p></td>
<td><p>设置为字体中所有标志符号的最大字符增量。</p></td>
<td><p>指定字体时有效。</p></td>
</tr>
<tr class="even">
<td><p><strong>FontStrikeThru</strong></p></td>
<td><p>如果为当前字体启用了删除线，则设置为 1; 否则设置为零。</p></td>
<td><p>指定字体时有效。</p></td>
</tr>
<tr class="odd">
<td><p><strong>FontUnderLine</strong></p></td>
<td><p>如果当前字体带有下划线，则设置为 1; 否则设置为零。</p></td>
<td><p>指定字体时有效。</p></td>
</tr>
<tr class="even">
<td><p><strong>FontWidth</strong></p></td>
<td><p>当前字体的宽度（以主单位为单位）。</p></td>
<td><p>指定字体时有效。</p></td>
</tr>
<tr class="odd">
<td><p><strong>GraphicsXRes</strong></p></td>
<td><p>图形的当前水平分辨率（DPI）。</p></td>
<td><p>当打印作业正在进行时有效。</p></td>
</tr>
<tr class="even">
<td><p><strong>GraphicsYRes</strong></p></td>
<td><p>图形的当前垂直分辨率（DPI）。</p></td>
<td><p>当打印作业正在进行时有效。</p></td>
</tr>
<tr class="odd">
<td><p><strong>GrayPercentage</strong></p></td>
<td><p>灰色级别 (要用于灰色填充的百分比) 。</p></td>
<td><p>在 CmdRectGrayFill 命令字符串中有效。</p></td>
</tr>
<tr class="even">
<td><p><strong>GreenValue</strong></p></td>
<td><p>当前颜色的绿色分量。</p></td>
<td><p>在 CmdDefinePaletteEntry 命令字符串中有效。  (另请参阅 <strong>BlueValue</strong>、 <strong>RedValue</strong>。 ) </p></td>
</tr>
<tr class="odd">
<td><p><strong>LinefeedSpacing</strong></p></td>
<td><p>以主单位表示的垂直空间量，表示换行。</p></td>
<td><p>在 CmdSetLineSpacing 命令字符串中有效。</p></td>
</tr>
<tr class="even">
<td><p><strong>NextFontID</strong></p></td>
<td><p>要下载的下一个软字体的标识号。</p></td>
<td><p>在 CmdSetFontID 命令字符串中有效。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NextGlyph</strong></p></td>
<td><p>要下载的下一个标志符号的双字节代码。</p></td>
<td><p>在 CmdSetCharCode 命令字符串中有效。</p></td>
</tr>
<tr class="even">
<td><p><strong>NumOfCopies</strong></p></td>
<td><p>用户请求的副本数。</p></td>
<td><p>当打印作业正在进行时有效。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NumOfDataBytes</strong></p></td>
<td><p>可供传输的光栅数据的字节数。</p></td>
<td><p>适用于任何 CmdSend<em>XXX</em>数据命令字符串。</p>
<p>如果压缩数据，则值为压缩后的字节数。</p></td>
</tr>
<tr class="even">
<td><p><strong>PageNumber</strong></p></td>
<td><p>当前正在打印的页的页码。 请注意，这并不一定对应于应用程序的页码，而是不一定对应于 <a href="https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvsendpage" data-raw-source="[&lt;em&gt;DrvSendPage&lt;/em&gt;](/windows/win32/api/winddi/nf-winddi-drvsendpage)"><em>DrvSendPage</em></a> 的调用次数。</p>
<p>此值由 <a href="https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvstartdoc" data-raw-source="[&lt;strong&gt;DrvStartDoc&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvstartdoc)"><strong>DrvStartDoc</strong></a> 初始化，并由 <strong>DrvSendPage</strong>递增。</p>
<p>例如，如果选择了 "N 向上 = 4"，则仅当打印文档的第五页时， <strong>PageNumber</strong> 才会递增为2。</p>
<p>再举一个例子，如果以相反的顺序打印文档 (回前) <strong>PageNumber</strong> 标准变量仍会报告第一页要打印为第1页，即使这是文档的最后一页。</p>
<p>若要正确支持自动双工功能，则需要此行为。</p>
<p>OEM 只应使用 <strong>PageNumber</strong> 来确定当前页是前端还是背面。</p></td>
<td><p>当打印作业正在进行时有效。</p></td>
</tr>
<tr class="odd">
<td><p><strong>PaletteIndexToProgram</strong></p></td>
<td><p>为要编程的下一项提供调色板索引。</p></td>
<td><p>在 CmdDefinePaletteEntry 命令字符串中有效。  (另请参阅 <strong>RedValue</strong>、 <strong>GreenValue</strong>、 <strong>BlueValue</strong>、 <strong>CurrentPaletteIndex</strong>。 ) </p></td>
</tr>
<tr class="even">
<td><p><strong>PatternBrushID</strong></p></td>
<td><p>已下载模式画笔的标识号。</p></td>
<td><p>与 CmdDownloadPattern 和 CmdSelectPattern 命令字符串一起使用时有效。</p></td>
</tr>
<tr class="odd">
<td><p><strong>PatternBrushSize</strong></p></td>
<td><p>当前模式画笔的大小（以字节为单位）。</p></td>
<td><p>与 CmdDownloadPattern 命令字符串一起使用时有效。</p></td>
</tr>
<tr class="even">
<td><p><strong>PatternBrushType</strong></p></td>
<td><p></p>
当前模式画笔的类型。 值可以为：2：底纹模式3：交叉影线模式4：用户定义的模式</td>
<td><p>与 CmdDownloadPattern 和 CmdSelectPattern 命令字符串一起使用时有效。</p></td>
</tr>
<tr class="odd">
<td><p><strong>PhysPaperLength</strong></p></td>
<td><p>当前正在使用的纸张的纵向模式长度（以 y 为主单位表示）。</p></td>
<td><p>当打印作业正在进行时有效。</p></td>
</tr>
<tr class="even">
<td><p><strong>PhysPaperWidth</strong></p></td>
<td><p>当前正在使用的纸张的纵向模式宽度（以主单位表示）。</p></td>
<td><p>当打印作业正在进行时有效。</p></td>
</tr>
<tr class="odd">
<td><p><strong>PrintDirInCCDegrees</strong></p></td>
<td><p>旋转量，以度为单位。</p></td>
<td><p>当驱动程序发送 CmdSetSimpleRotation 或 CmdSetAnyRotation 命令字符串时有效。</p></td>
</tr>
<tr class="even">
<td><p><strong>RasterDataHeightInPixels</strong></p></td>
<td><p>当前数据表示的图像的高度（以像素为单位）。</p></td>
<td><p>适用于任何 CmdSend<em>XXX</em>数据命令字符串和 CmdSetSrcBmpHeight 命令字符串。 压缩不会修改此值。</p></td>
</tr>
<tr class="odd">
<td><p><strong>RasterDataWidthInBytes</strong></p></td>
<td><p>扫描行中包含的字节数。</p></td>
<td><p>适用于任何 CmdSend<em>XXX</em>数据命令字符串和 CmdSetSrcBmpWidth 命令字符串。 压缩不会修改此值。</p></td>
</tr>
<tr class="even">
<td><p><strong>RectXSize</strong></p></td>
<td><p>矩形宽度，以 x 主单位表示。</p></td>
<td><p>在 CmdSetRectWidth 命令字符串中有效。</p></td>
</tr>
<tr class="odd">
<td><p><strong>RectYSize</strong></p></td>
<td><p>矩形长度，以 y 为主单位表示。</p></td>
<td><p>在 CmdSetRectHeight 命令字符串中有效。</p></td>
</tr>
<tr class="even">
<td><p><strong>RedValue</strong></p></td>
<td><p>当前颜色的红色分量。</p></td>
<td><p>在 CmdDefinePaletteEntry 命令字符串中有效。  (另请参阅 <strong>GreenValue</strong>、 <strong>BlueValue</strong>。 ) </p></td>
</tr>
<tr class="odd">
<td><p><strong>TextXRes</strong></p></td>
<td><p>文本的当前水平分辨率（DPI）。</p></td>
<td><p>当打印作业正在进行时有效。</p></td>
</tr>
<tr class="even">
<td><p><strong>TextYRes</strong></p></td>
<td><p>文本的当前垂直分辨率（DPI）。</p></td>
<td><p>当打印作业正在进行时有效。</p></td>
</tr>
</tbody>
</table>

 

 


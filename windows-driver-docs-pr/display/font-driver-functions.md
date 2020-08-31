---
title: 字体驱动程序函数
description: 字体驱动程序函数
ms.assetid: 95bf5a3b-29f8-43d2-9f24-22cfe257ead4
keywords:
- 字体 WDK 图形，驱动程序函数
- GDI WDK Windows 2000 显示、字体、驱动程序函数
- 图形驱动程序 WDK Windows 2000 显示、字体、驱动程序函数
- DrvLoadFontFile
- DrvUnloadFontFile
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00b70e9ab8373c0340ef62626f279cab38289fce
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066706"
---
# <a name="font-driver-functions"></a>字体驱动程序函数


## <span id="ddk_font_driver_functions_gg"></span><span id="DDK_FONT_DRIVER_FUNCTIONS_GG"></span>


除了前面的主题中所述的函数外，下表还列出了字体驱动程序应支持的其他一些功能。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">函数</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvloadfontfile" data-raw-source="[&lt;strong&gt;DrvLoadFontFile&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvloadfontfile)"><strong>DrvLoadFontFile</strong></a></p></td>
<td align="left"><p>指定用于创建字体实现的文件;驱动程序必须准备要使用的文件。 字体驱动程序所必需的。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvqueryadvancewidths" data-raw-source="[&lt;strong&gt;DrvQueryAdvanceWidths&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvqueryadvancewidths)"><strong>DrvQueryAdvanceWidths</strong></a></p></td>
<td align="left"><p>要求驱动程序为一组指定的字形发送 GDI 字符提前宽度。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvqueryfontcaps" data-raw-source="[&lt;strong&gt;DrvQueryFontCaps&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvqueryfontcaps)"><strong>DrvQueryFontCaps</strong></a></p></td>
<td align="left"><p>将定义字体驱动程序功能的一组位复制到指定的缓冲区。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvqueryfontfile" data-raw-source="[&lt;strong&gt;DrvQueryFontFile&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvqueryfontfile)"><strong>DrvQueryFontFile</strong></a></p></td>
<td align="left"><p>根据查询的模式，返回字体文件或说明性字符串中的字体数量。 字体驱动程序所必需的。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nc-winddi-pfn_drvqueryglyphattrs" data-raw-source="[&lt;strong&gt;DrvQueryGlyphAttrs&lt;/strong&gt;](/windows/desktop/api/winddi/nc-winddi-pfn_drvqueryglyphattrs)"><strong>DrvQueryGlyphAttrs</strong></a></p></td>
<td align="left"><p>返回有关字体标志符号的信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvunloadfontfile" data-raw-source="[&lt;strong&gt;DrvUnloadFontFile&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvunloadfontfile)"><strong>DrvUnloadFontFile</strong></a></p></td>
<td align="left"><p>通知驱动程序不再需要字体文件，以便驱动程序可以进行必要的清理。 字体驱动程序所必需的。</p></td>
</tr>
</tbody>
</table>

 

GDI 使用要用于创建字体实现的特定文件调用 *DrvLoadFontFile* 函数。 此函数只在字体驱动程序中是必需的。 调用函数 *DrvLoadFontFile* 时，驱动程序将执行准备文件以供使用所需的转换。

*DrvLoadFontFile* 返回一个唯一的标识符，该标识符允许 GDI 使用 gdi 维护字体使用情况表请求正确的字体。 加载字体后，GDI 不会调用同一字体再次加载。

当不再需要指定的字体文件时，GDI 将调用 *DrvUnloadFontFile* 。 *DrvUnloadFontFile*函数仅在字体驱动程序中是必需的。 *DrvUnloadFontFile* 会导致删除所有暂存文件，并释放所有已分配的系统资源。

GDI 将调用 *DrvQueryFontFile* 函数以返回有关驱动程序加载的字体文件的信息。 *DrvQueryFontFile* 仅在字体驱动程序中是必需的。 *IMode*指定要返回的信息的类型。 如果 *iMode* 是 QFF \_ 说明，则该函数将返回一个字符串，Microsoft 基于 NT 的操作系统使用该字符串描述该字体文件。 如果 *iMode* 是 QFF \_ NUMFACES，则该函数将返回字体文件中的面部数。 面部是通过从1到面的范围的索引进行标识。

 


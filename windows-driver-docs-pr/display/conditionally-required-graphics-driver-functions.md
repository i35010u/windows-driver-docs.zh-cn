---
title: 在不同的条件下需要的图形驱动程序函数
description: 在不同的条件下需要的图形驱动程序函数
ms.assetid: db5816e2-83a1-491d-99f5-d693fefcf1fd
keywords:
- GDI WDK Windows 2000 显示，功能，有条件地需要
- 图形驱动程序 WDK Windows 2000 显示、功能、有条件地需要
- 函数 WDK 图形，有条件地需要
- 绘制 WDK GDI，函数，有条件地需要
- GDI WDK Windows 2000 显示，DDI，有条件地要求函数
- 图形驱动程序 WDK Windows 2000 显示，DDI，有条件地需要的函数
- DDI WDK 图形，有条件地需要的函数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 20e2425ee55ccd9dd75e4a3d4a2c5f95d0d9dd1f
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89064904"
---
# <a name="conditionally-required-graphics-driver-functions"></a>在不同的条件下需要的图形驱动程序函数


## <span id="ddk_conditionally_required_graphics_driver_functions_gg"></span><span id="DDK_CONDITIONALLY_REQUIRED_GRAPHICS_DRIVER_FUNCTIONS_GG"></span>


除始终需要的函数外，可能还需要某些其他函数，具体取决于驱动程序的实现方式。 下表列出了有条件要求的函数。 如果驱动程序管理其自己的主表面 (则使用 **EngCreateDeviceSurface** 通常允许 GDI 管理这些操作中的大部分或全部。 显示支持可设置调色板的还必须支持 [**DrvSetPalette**](/windows/desktop/api/winddi/nf-winddi-drvsetpalette) 函数。

通常，打印机驱动程序比显示驱动程序要定义或绘制字体更常见。 处理字体不需要显示驱动程序。 如果硬件具有居民字体，则驱动程序必须向 GDI 提供有关此字体的信息。 此信息包括字体指标、从 Unicode 映射到各个标志符号标识、各个标志符号特性和字偶间距调整表。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">入口点</th>
<th align="left">需要时</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvcopybits" data-raw-source="[&lt;strong&gt;DrvCopyBits&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvcopybits)"><strong>DrvCopyBits</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/#wdkgloss-device-managed-surface" data-raw-source="&lt;em&gt;Device-managed surfaces&lt;/em&gt;"><em>设备管理的图面</em></a></p></td>
<td align="left"><p>转换设备托管的光栅图面和 GDI 标准格式的位图。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdescribepixelformat" data-raw-source="[&lt;strong&gt;DrvDescribePixelFormat&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvdescribepixelformat)"><strong>DrvDescribePixelFormat</strong></a></p></td>
<td align="left"><p>显示支持具有不同像素格式的窗口在单个表面上</p></td>
<td align="left"><p>描述 PDEV 的像素格式。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvgettruetypefile" data-raw-source="[&lt;strong&gt;DrvGetTrueTypeFile&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvgettruetypefile)"><strong>DrvGetTrueTypeFile</strong></a></p></td>
<td align="left"><p>TrueType 字体驱动程序</p></td>
<td align="left"><p>授予对内存映射的 TrueType 字体文件的 GDI 访问权限。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvloadfontfile" data-raw-source="[&lt;strong&gt;DrvLoadFontFile&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvloadfontfile)"><strong>DrvLoadFontFile</strong></a></p></td>
<td align="left"><p>字体驱动程序</p></td>
<td align="left"><p>指定字体实现要使用的文件。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvqueryfont" data-raw-source="[&lt;strong&gt;DrvQueryFont&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvqueryfont)"><strong>DrvQueryFont</strong></a></p></td>
<td align="left"><p>打印机驱动程序</p></td>
<td align="left"><p>检索给定字体的 GDI 结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvqueryfontcaps" data-raw-source="[&lt;strong&gt;DrvQueryFontCaps&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvqueryfontcaps)"><strong>DrvQueryFontCaps</strong></a></p></td>
<td align="left"><p>字体驱动程序</p></td>
<td align="left"><p>询问驱动程序的字体驱动程序功能。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvqueryfontdata" data-raw-source="[&lt;strong&gt;DrvQueryFontData&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvqueryfontdata)"><strong>DrvQueryFontData</strong></a></p></td>
<td align="left"><p>打印机驱动程序</p></td>
<td align="left"><p>检索有关已实现字体的信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvqueryfontfile" data-raw-source="[&lt;strong&gt;DrvQueryFontFile&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvqueryfontfile)"><strong>DrvQueryFontFile</strong></a></p></td>
<td align="left"><p>字体驱动程序</p></td>
<td align="left"><p>询问驱动程序的字体文件信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvqueryfonttree" data-raw-source="[&lt;strong&gt;DrvQueryFontTree&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvqueryfonttree)"><strong>DrvQueryFontTree</strong></a></p></td>
<td align="left"><p>打印机驱动程序</p></td>
<td align="left"><p>查询树结构，该结构定义三种类型的字体映射之一。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvquerytruetypeoutline" data-raw-source="[&lt;strong&gt;DrvQueryTrueTypeOutline&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvquerytruetypeoutline)"><strong>DrvQueryTrueTypeOutline</strong></a></p></td>
<td align="left"><p>TrueType 字体驱动程序</p></td>
<td align="left"><p>返回 GDI 的 TrueType 标志符号句柄。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvquerytruetypetable" data-raw-source="[&lt;strong&gt;DrvQueryTrueTypeTable&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvquerytruetypetable)"><strong>DrvQueryTrueTypeTable</strong></a></p></td>
<td align="left"><p>TrueType 字体驱动程序</p></td>
<td align="left"><p>授予对 TrueType 字体文件的 GDI 访问权限。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvresetpdev" data-raw-source="[&lt;strong&gt;DrvResetPDEV&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvresetpdev)"><strong>DrvResetPDEV</strong></a></p></td>
<td align="left"><p>允许文档中的模式更改的设备</p></td>
<td align="left"><p>将驱动程序状态从旧的 PDEV 传输到新的 PDEV。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsetpalette" data-raw-source="[&lt;strong&gt;DrvSetPalette&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvsetpalette)"><strong>DrvSetPalette</strong></a></p></td>
<td align="left"><p>显示支持可设置调色板</p></td>
<td align="left"><p>认识到指定设备的调色板。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsetpixelformat" data-raw-source="[&lt;strong&gt;DrvSetPixelFormat&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvsetpixelformat)"><strong>DrvSetPixelFormat</strong></a></p></td>
<td align="left"><p>显示支持具有不同像素格式的窗口在单个表面上</p></td>
<td align="left"><p>设置窗口的像素格式。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstrokepath" data-raw-source="[&lt;strong&gt;DrvStrokePath&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvstrokepath)"><strong>DrvStrokePath</strong></a></p></td>
<td align="left"><p>设备管理的图面</p></td>
<td align="left"><p>呈现显示的路径。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvswapbuffers" data-raw-source="[&lt;strong&gt;DrvSwapBuffers&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvswapbuffers)"><strong>DrvSwapBuffers</strong></a></p></td>
<td align="left"><p>支持具有双缓冲的像素格式的驱动程序</p></td>
<td align="left"><p>显示图面隐藏缓冲区的内容。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtextout" data-raw-source="[&lt;strong&gt;DrvTextOut&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvtextout)"><strong>DrvTextOut</strong></a></p></td>
<td align="left"><p>定义字体的设备托管的图面或驱动程序</p></td>
<td align="left"><p>在指定位置 (字形) 渲染一组字符图像。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvunloadfontfile" data-raw-source="[&lt;strong&gt;DrvUnloadFontFile&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvunloadfontfile)"><strong>DrvUnloadFontFile</strong></a></p></td>
<td align="left"><p>字体驱动程序</p></td>
<td align="left"><p>通知驱动程序不需要字体文件。</p></td>
</tr>
</tbody>
</table>

 

 


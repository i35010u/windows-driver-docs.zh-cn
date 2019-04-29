---
title: 在不同的条件下需要的图形驱动程序函数
description: 在不同的条件下需要的图形驱动程序函数
ms.assetid: db5816e2-83a1-491d-99f5-d693fefcf1fd
keywords:
- GDI WDK Windows 2000 显示、 有条件地所需的功能
- 显示图形驱动程序 WDK Windows 2000，有条件地所需的功能
- 有条件地所需功能 WDK 图形
- 绘制 WDK GDI 函数中，有条件地需要
- 有条件地 GDI WDK Windows 2000 显示，DDI 所需的函数
- 驱动程序 WDK Windows 2000 显示图形 DDI，有条件地所需的功能
- DDI WDK 图形，有条件地所需的功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1cca1fcf72c7d18e8658557ea9bd498de08f35d9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355379"
---
# <a name="conditionally-required-graphics-driver-functions"></a>在不同的条件下需要的图形驱动程序函数


## <span id="ddk_conditionally_required_graphics_driver_functions_gg"></span><span id="DDK_CONDITIONALLY_REQUIRED_GRAPHICS_DRIVER_FUNCTIONS_GG"></span>


除了始终都需要提供的函数，某些其他函数可能是必需的具体取决于如何实现一个驱动程序。 下表中列出的有条件地所需的函数。 如果该驱动程序管理其自己的主表面 (使用**EngCreateDeviceSurface**通常允许 GDI 来管理大多数或所有这些操作。 此外必须支持显示支持可设置调色板[ **DrvSetPalette** ](https://msdn.microsoft.com/library/windows/hardware/ff556282)函数。

很多常见的打印机驱动程序比显示器驱动程序来定义或绘制字体。 显示驱动程序不需要处理字体。 如果硬件具有常驻字体，驱动程序必须提供到 GDI 有关此字体的信息。 此信息包括字体规格，从 Unicode 到单个标志符号标识、 单个标志符号属性和字距调整表的映射。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">入口点</th>
<th align="left">在需要时</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556182" data-raw-source="[&lt;strong&gt;DrvCopyBits&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556182)"><strong>DrvCopyBits</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556277#wdkgloss-device-managed-surface" data-raw-source="&lt;em&gt;Device-managed surfaces&lt;/em&gt;"><em>设备管理的图面</em></a></p></td>
<td align="left"><p>设备管理光栅图面和 GDI 标准格式位图之间进行转换。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556190" data-raw-source="[&lt;strong&gt;DrvDescribePixelFormat&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556190)"><strong>DrvDescribePixelFormat</strong></a></p></td>
<td align="left"><p>支持具有不同的像素格式的 windows 的单个图面的显示</p></td>
<td align="left"><p>介绍 PDEV 的像素格式。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556235" data-raw-source="[&lt;strong&gt;DrvGetTrueTypeFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556235)"><strong>DrvGetTrueTypeFile</strong></a></p></td>
<td align="left"><p>TrueType 字体驱动程序</p></td>
<td align="left"><p>一个内存映射 TrueType 字体文件，GDI 访问。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556247" data-raw-source="[&lt;strong&gt;DrvLoadFontFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556247)"><strong>DrvLoadFontFile</strong></a></p></td>
<td align="left"><p>字体驱动程序</p></td>
<td align="left"><p>指定要用于字体的实现文件。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556262" data-raw-source="[&lt;strong&gt;DrvQueryFont&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556262)"><strong>DrvQueryFont</strong></a></p></td>
<td align="left"><p>打印机驱动程序</p></td>
<td align="left"><p>检索给定的字体的 GDI 结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556263" data-raw-source="[&lt;strong&gt;DrvQueryFontCaps&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556263)"><strong>DrvQueryFontCaps</strong></a></p></td>
<td align="left"><p>字体驱动程序</p></td>
<td align="left"><p>字体驱动程序功能，要求提供驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556264" data-raw-source="[&lt;strong&gt;DrvQueryFontData&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556264)"><strong>DrvQueryFontData</strong></a></p></td>
<td align="left"><p>打印机驱动程序</p></td>
<td align="left"><p>检索有关已实现的字体的信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556265" data-raw-source="[&lt;strong&gt;DrvQueryFontFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556265)"><strong>DrvQueryFontFile</strong></a></p></td>
<td align="left"><p>字体驱动程序</p></td>
<td align="left"><p>要求驱动程序提供的字体文件信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556266" data-raw-source="[&lt;strong&gt;DrvQueryFontTree&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556266)"><strong>DrvQueryFontTree</strong></a></p></td>
<td align="left"><p>打印机驱动程序</p></td>
<td align="left"><p>查询定义的三种类型的字体映射一个树状结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556269" data-raw-source="[&lt;strong&gt;DrvQueryTrueTypeOutline&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556269)"><strong>DrvQueryTrueTypeOutline</strong></a></p></td>
<td align="left"><p>TrueType 字体驱动程序</p></td>
<td align="left"><p>返回到 GDI TrueType 标志符号句柄。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556271" data-raw-source="[&lt;strong&gt;DrvQueryTrueTypeTable&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556271)"><strong>DrvQueryTrueTypeTable</strong></a></p></td>
<td align="left"><p>TrueType 字体驱动程序</p></td>
<td align="left"><p>TrueType 字体文件，GDI 访问。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556276" data-raw-source="[&lt;strong&gt;DrvResetPDEV&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556276)"><strong>DrvResetPDEV</strong></a></p></td>
<td align="left"><p>允许文档中的模式更改的设备</p></td>
<td align="left"><p>将驱动程序状态从旧 PDEV 传输到新 PDEV。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556282" data-raw-source="[&lt;strong&gt;DrvSetPalette&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556282)"><strong>DrvSetPalette</strong></a></p></td>
<td align="left"><p>支持可设置调色板的显示</p></td>
<td align="left"><p>认识到指定设备的调色板。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556285" data-raw-source="[&lt;strong&gt;DrvSetPixelFormat&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556285)"><strong>DrvSetPixelFormat</strong></a></p></td>
<td align="left"><p>支持具有不同的像素格式的 windows 的单个图面的显示</p></td>
<td align="left"><p>设置窗口的像素格式。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556316" data-raw-source="[&lt;strong&gt;DrvStrokePath&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556316)"><strong>DrvStrokePath</strong></a></p></td>
<td align="left"><p>设备管理的图面</p></td>
<td align="left"><p>呈现上显示的路径。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556322" data-raw-source="[&lt;strong&gt;DrvSwapBuffers&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556322)"><strong>DrvSwapBuffers</strong></a></p></td>
<td align="left"><p>支持使用双缓冲的像素格式的驱动程序</p></td>
<td align="left"><p>显示面上的隐藏缓冲区的内容。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff557277" data-raw-source="[&lt;strong&gt;DrvTextOut&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557277)"><strong>DrvTextOut</strong></a></p></td>
<td align="left"><p>设备管理的图面或定义字体的驱动程序</p></td>
<td align="left"><p>呈现一组指定位置处的字符图像 （标志符号）。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff557287" data-raw-source="[&lt;strong&gt;DrvUnloadFontFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557287)"><strong>DrvUnloadFontFile</strong></a></p></td>
<td align="left"><p>字体驱动程序</p></td>
<td align="left"><p>会通知驱动程序不需要字体文件。</p></td>
</tr>
</tbody>
</table>

 

 

 






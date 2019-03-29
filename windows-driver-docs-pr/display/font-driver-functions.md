---
title: 字体驱动程序函数
description: 字体驱动程序函数
ms.assetid: 95bf5a3b-29f8-43d2-9f24-22cfe257ead4
keywords:
- 字体 WDK 图形，驱动程序函数
- GDI WDK Windows 2000 显示、 字体、 驱动程序函数
- 图形驱动程序 WDK Windows 2000 显示，字体，驱动程序功能
- DrvLoadFontFile
- DrvUnloadFontFile
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d5560ff7b1bdffd5057a3a6fef235db53211fe92
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350304"
---
# <a name="font-driver-functions"></a>字体驱动程序函数


## <span id="ddk_font_driver_functions_gg"></span><span id="DDK_FONT_DRIVER_FUNCTIONS_GG"></span>


在前面的主题中所述的函数，除了下表列出了几个其他字体驱动程序应支持的函数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">函数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556247" data-raw-source="[&lt;strong&gt;DrvLoadFontFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556247)"><strong>DrvLoadFontFile</strong></a></p></td>
<td align="left"><p>指定要用于创建字体的实现; 的文件该驱动程序必须准备供使用的文件。 所需的字体驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556259" data-raw-source="[&lt;strong&gt;DrvQueryAdvanceWidths&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556259)"><strong>DrvQueryAdvanceWidths</strong></a></p></td>
<td align="left"><p>要求驱动程序将发送 GDI 字符的一组指定的标志符号的步进宽度。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556263" data-raw-source="[&lt;strong&gt;DrvQueryFontCaps&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556263)"><strong>DrvQueryFontCaps</strong></a></p></td>
<td align="left"><p>将复制到指定的缓冲区定义的字体驱动程序功能的位数组。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556265" data-raw-source="[&lt;strong&gt;DrvQueryFontFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556265)"><strong>DrvQueryFontFile</strong></a></p></td>
<td align="left"><p>具体取决于查询的模式，在字体文件或描述性字符串中返回字体的实际面部数。 所需的字体驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556267" data-raw-source="[&lt;strong&gt;DrvQueryGlyphAttrs&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556267)"><strong>DrvQueryGlyphAttrs</strong></a></p></td>
<td align="left"><p>返回有关字体的标志符号的信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff557287" data-raw-source="[&lt;strong&gt;DrvUnloadFontFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557287)"><strong>DrvUnloadFontFile</strong></a></p></td>
<td align="left"><p>会通知驱动程序，因此驱动程序可以执行必要的清理不再需要的字体文件。 所需的字体驱动程序。</p></td>
</tr>
</tbody>
</table>

 

GDI 调用*DrvLoadFontFile*函数中要用来创建字体的实现的特定文件。 此函数是必需的字体驱动程序。 当函数*DrvLoadFontFile*是调用，该驱动程序执行准备使用的文件进行必要的转换。

*DrvLoadFontFile*返回允许 GDI 请求正确的字体使用 GDI 维护字体使用表的唯一标识符。 一旦加载一种字体，GDI 将不会调用要重新加载的相同字体。

GDI 调用*DrvUnloadFontFile*当不再需要指定的字体文件。 *DrvUnloadFontFile*仅在字体驱动程序中需要函数。 *DrvUnloadFontFile*会导致所有临时文件是要释放的已删除和所有已分配的系统资源。

GDI 调用*DrvQueryFontFile*函数以返回有关已加载的驱动程序的字体文件的信息。 *DrvQueryFontFile*仅在字体驱动程序中需要。 指定要返回的信息类型*iMode*。 如果*iMode*是 QFF\_说明，该函数返回一个字符串，Microsoft 基于 NT 的操作系统使用来描述字体文件。 如果*iMode*是 QFF\_NUMFACES，该函数返回的实际面部数字体文件中。 人脸的面部数从 1 范围内的索引进行标识。

 

 






---
title: GDI 字体和文本服务
description: GDI 字体和文本服务
ms.assetid: c315f3ec-ddee-42d9-8bfb-7bb2e0d1d4b2
keywords:
- 字体 WDK GDI
- GDI WDK Windows 2000 显示，字体
- 图形驱动程序 WDK Windows 2000 显示，字体
- 绘制 WDK GDI，字体
- GDI WDK Windows 2000 显示，文本输出
- 图形驱动程序 WDK Windows 2000 显示，文本输出
- 绘制 WDK GDI，文本输出
- 文本输出 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 25efe82d1dec04c845b198a2d6f43818bc7c7d9c
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90107342"
---
# <a name="gdi-font-and-text-services"></a>GDI 字体和文本服务


## <span id="ddk_gdi_font_and_text_services_gg"></span><span id="DDK_GDI_FONT_AND_TEXT_SERVICES_GG"></span>


GDI 为字体管理和文本输出提供支持。 [**FONTOBJ**](/windows/desktop/api/winddi/ns-winddi-_fontobj)结构和相关函数为驱动程序授予对特定字体实例的访问权限。 若要支持文本输出，驱动程序可以访问 [**STROBJ**](/windows/desktop/api/winddi/ns-winddi-_strobj) 结构和相关函数。 下表列出了 FONTOBJ 和 STROBJ 相关的函数。

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
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-engcomputeglyphset" data-raw-source="[&lt;strong&gt;EngComputeGlyphSet&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-engcomputeglyphset)"><strong>EngComputeGlyphSet</strong></a></p></td>
<td align="left"><p>计算设备上支持的字形集。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-engfntcachealloc" data-raw-source="[&lt;strong&gt;EngFntCacheAlloc&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-engfntcachealloc)"><strong>EngFntCacheAlloc</strong></a></p></td>
<td align="left"><p>为缓存的字体文件分配内存。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-engfntcachefault" data-raw-source="[&lt;strong&gt;EngFntCacheFault&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-engfntcachefault)"><strong>EngFntCacheFault</strong></a></p></td>
<td align="left"><p>如果字体驱动程序在读取或写入字体数据缓存时遇到错误，则将错误报告给字体引擎。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-engfntcachelookup" data-raw-source="[&lt;strong&gt;EngFntCacheLookUp&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-engfntcachelookup)"><strong>EngFntCacheLookUp</strong></a></p></td>
<td align="left"><p>检索指向缓存的字体文件数据的指针。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-enggetcurrentcodepage" data-raw-source="[&lt;strong&gt;EngGetCurrentCodePage&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-enggetcurrentcodepage)"><strong>EngGetCurrentCodePage</strong></a></p></td>
<td align="left"><p>返回系统的默认 OEM 和 ANSI 代码页。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-enggettype1fontlist" data-raw-source="[&lt;strong&gt;EngGetType1FontList&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-enggettype1fontlist)"><strong>EngGetType1FontList</strong></a></p></td>
<td align="left"><p>检索本地和远程安装的 PostScript 类型1字体的列表。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-engtextout" data-raw-source="[&lt;strong&gt;EngTextOut&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-engtextout)"><strong>EngTextOut</strong></a></p></td>
<td align="left"><p>这是 <a href="/windows/desktop/api/winddi/nf-winddi-drvtextout" data-raw-source="[&lt;strong&gt;DrvTextOut&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvtextout)"><strong>DrvTextOut</strong></a> 函数的 GDI 模拟。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-fontobj_cgetallglyphhandles" data-raw-source="[&lt;strong&gt;FONTOBJ_cGetAllGlyphHandles&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-fontobj_cgetallglyphhandles)"><strong>FONTOBJ_cGetAllGlyphHandles</strong></a></p></td>
<td align="left"><p>允许驱动程序检索 GDI 字体的每个字形句柄。 驱动程序使用此服务下载整个字体。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-fontobj_cgetglyphs" data-raw-source="[&lt;strong&gt;FONTOBJ_cGetGlyphs&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-fontobj_cgetglyphs)"><strong>FONTOBJ_cGetGlyphs</strong></a></p></td>
<td align="left"><p>将标志符号句柄转换为指向字体使用者的关联标志符号数据的指针。 这些指针在下一次调用 <strong>FONTOBJ_cGetGlyphs</strong>之前有效。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-fontobj_pfdg" data-raw-source="[&lt;strong&gt;FONTOBJ_pfdg&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-fontobj_pfdg)"><strong>FONTOBJ_pfdg</strong></a></p></td>
<td align="left"><p>检索指向与指定字体关联的 <a href="/windows/desktop/api/winddi/ns-winddi-_fd_glyphset" data-raw-source="[&lt;strong&gt;FD_GLYPHSET&lt;/strong&gt;](/windows/desktop/api/winddi/ns-winddi-_fd_glyphset)"><strong>FD_GLYPHSET</strong></a> 结构的指针。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-fontobj_pifi" data-raw-source="[&lt;strong&gt;FONTOBJ_pifi&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-fontobj_pifi)"><strong>FONTOBJ_pifi</strong></a></p></td>
<td align="left"><p>检索指向描述关联字体的 <a href="/windows/desktop/api/winddi/ns-winddi-_ifimetrics" data-raw-source="[&lt;strong&gt;IFIMETRICS&lt;/strong&gt;](/windows/desktop/api/winddi/ns-winddi-_ifimetrics)"><strong>IFIMETRICS</strong></a> 结构的指针。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-fontobj_pjopentypetablepointer" data-raw-source="[&lt;strong&gt;FONTOBJ_pjOpenTypeTablePointer&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-fontobj_pjopentypetablepointer)"><strong>FONTOBJ_pjOpenTypeTablePointer</strong></a></p></td>
<td align="left"><p>返回指向 OpenType 表的视图的指针。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-fontobj_pqueryglyphattrs" data-raw-source="[&lt;strong&gt;FONTOBJ_pQueryGlyphAttrs&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-fontobj_pqueryglyphattrs)"><strong>FONTOBJ_pQueryGlyphAttrs</strong></a></p></td>
<td align="left"><p>返回有关字体标志符号的信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-fontobj_pvtruetypefontfile" data-raw-source="[&lt;strong&gt;FONTOBJ_pvTrueTypeFontFile&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-fontobj_pvtruetypefontfile)"><strong>FONTOBJ_pvTrueTypeFontFile</strong></a></p></td>
<td align="left"><p>检索指向 TrueType、OpenType 或 Type1 字体文件的视图的指针。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-fontobj_pwszfontfilepaths" data-raw-source="[&lt;strong&gt;FONTOBJ_pwszFontFilePaths&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-fontobj_pwszfontfilepaths)"><strong>FONTOBJ_pwszFontFilePaths</strong></a></p></td>
<td align="left"><p>检索与字体关联 (s) 的文件路径。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-fontobj_pxogetxform" data-raw-source="[&lt;strong&gt;FONTOBJ_pxoGetXform&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-fontobj_pxogetxform)"><strong>FONTOBJ_pxoGetXform</strong></a></p></td>
<td align="left"><p>检索关联字体的名义到设备转换。 驱动程序需要此转换才能实现驱动程序提供的字体。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-fontobj_vgetinfo" data-raw-source="[&lt;strong&gt;FONTOBJ_vGetInfo&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-fontobj_vgetinfo)"><strong>FONTOBJ_vGetInfo</strong></a></p></td>
<td align="left"><p>返回描述关联的字体的信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-strobj_benum" data-raw-source="[&lt;strong&gt;STROBJ_bEnum&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-strobj_benum)"><strong>STROBJ_bEnum</strong></a></p></td>
<td align="left"><p>枚举指定 STROBJ 中的标志符号标识和位置。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-strobj_benumpositionsonly" data-raw-source="[&lt;strong&gt;STROBJ_bEnumPositionsOnly&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-strobj_benumpositionsonly)"><strong>STROBJ_bEnumPositionsOnly</strong></a></p></td>
<td align="left"><p>枚举指定文本字符串的标志符号标识和位置，但不创建缓存的标志符号位图。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-strobj_bgetadvancewidths" data-raw-source="[&lt;strong&gt;STROBJ_bGetAdvanceWidths&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-strobj_bgetadvancewidths)"><strong>STROBJ_bGetAdvanceWidths</strong></a></p></td>
<td align="left"><p>返回指定字符串的可能宽度的向量。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-strobj_dwgetcodepage" data-raw-source="[&lt;strong&gt;STROBJ_dwGetCodePage&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-strobj_dwgetcodepage)"><strong>STROBJ_dwGetCodePage</strong></a></p></td>
<td align="left"><p>返回与指定 STROBJ 关联的代码页。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-strobj_fxbreakextra" data-raw-source="[&lt;strong&gt;STROBJ_fxBreakExtra&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-strobj_fxbreakextra)"><strong>STROBJ_fxBreakExtra</strong></a></p></td>
<td align="left"><p>检索在显示和/或打印对齐文本时要添加到字符串中的每个空格字符的额外空间量。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-strobj_venumstart" data-raw-source="[&lt;strong&gt;STROBJ_vEnumStart&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-strobj_venumstart)"><strong>STROBJ_vEnumStart</strong></a></p></td>
<td align="left"><p>为指定的 STROBJ 重新启动 <a href="/windows/desktop/api/winddi/ns-winddi-_glyphpos" data-raw-source="[&lt;strong&gt;GLYPHPOS&lt;/strong&gt;](/windows/desktop/api/winddi/ns-winddi-_glyphpos)"><strong>GLYPHPOS</strong></a> 数组的枚举。 此函数应在后续枚举之前由驱动程序调用。</p></td>
</tr>
</tbody>
</table>

 


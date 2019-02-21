---
title: GDI 字体和文本服务
description: GDI 字体和文本服务
ms.assetid: c315f3ec-ddee-42d9-8bfb-7bb2e0d1d4b2
keywords:
- WDK GDI 字体
- GDI WDK Windows 2000 显示字体
- 图形驱动程序 WDK Windows 2000 显示字体
- 绘制 WDK GDI，字体
- GDI WDK Windows 2000 显示、 文本输出
- 图形驱动程序 WDK Windows 2000 显示、 文本输出
- 绘制 WDK GDI，文本输出
- 文本输出 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f058562bb7ec4eaef5f5ec1ebc237d947853ee5b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526473"
---
# <a name="gdi-font-and-text-services"></a>GDI 字体和文本服务


## <span id="ddk_gdi_font_and_text_services_gg"></span><span id="DDK_GDI_FONT_AND_TEXT_SERVICES_GG"></span>


GDI 字体管理和文本输出提供支持。 [ **FONTOBJ** ](https://msdn.microsoft.com/library/windows/hardware/ff565974)结构和相关的函数让驱动程序访问的特定实例的一种字体。 若要支持文本输出，该驱动程序有权访问[ **STROBJ** ](https://msdn.microsoft.com/library/windows/hardware/ff569738)结构和相关的函数。 下表列出了与 FONTOBJ 和 STROBJ 相关的函数。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564192" data-raw-source="[&lt;strong&gt;EngComputeGlyphSet&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564192)"><strong>EngComputeGlyphSet</strong></a></p></td>
<td align="left"><p>计算设备上设置受支持的标志符号。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564877" data-raw-source="[&lt;strong&gt;EngFntCacheAlloc&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564877)"><strong>EngFntCacheAlloc</strong></a></p></td>
<td align="left"><p>缓存的字体文件分配内存。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564882" data-raw-source="[&lt;strong&gt;EngFntCacheFault&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564882)"><strong>EngFntCacheFault</strong></a></p></td>
<td align="left"><p>如果字体驱动程序遇到错误读取或写入的字体数据缓存到字体引擎报告错误。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564887" data-raw-source="[&lt;strong&gt;EngFntCacheLookUp&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564887)"><strong>EngFntCacheLookUp</strong></a></p></td>
<td align="left"><p>检索指向缓存的字体文件数据。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564917" data-raw-source="[&lt;strong&gt;EngGetCurrentCodePage&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564917)"><strong>EngGetCurrentCodePage</strong></a></p></td>
<td align="left"><p>返回系统&#39;s 默认 OEM 和 ANSI 代码页。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564956" data-raw-source="[&lt;strong&gt;EngGetType1FontList&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564956)"><strong>EngGetType1FontList</strong></a></p></td>
<td align="left"><p>检索本地和远程安装的 PostScript Type 1 字体的列表。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565034" data-raw-source="[&lt;strong&gt;EngTextOut&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565034)"><strong>EngTextOut</strong></a></p></td>
<td align="left"><p>这是 GDI 模拟<a href="https://msdn.microsoft.com/library/windows/hardware/ff557277" data-raw-source="[&lt;strong&gt;DrvTextOut&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557277)"> <strong>DrvTextOut</strong> </a>函数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565977" data-raw-source="[&lt;strong&gt;FONTOBJ_cGetAllGlyphHandles&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565977)"><strong>FONTOBJ_cGetAllGlyphHandles</strong></a></p></td>
<td align="left"><p>使驱动程序以检索每个字形句柄的 GDI 字体。 该驱动程序使用此服务下载整个字体。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565982" data-raw-source="[&lt;strong&gt;FONTOBJ_cGetGlyphs&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565982)"><strong>FONTOBJ_cGetGlyphs</strong></a></p></td>
<td align="left"><p>将标志符号句柄到指向关联的标志符号数据的指针转换为字体使用者。 直到下一步调用这些指针是否有效<strong>FONTOBJ_cGetGlyphs</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565989" data-raw-source="[&lt;strong&gt;FONTOBJ_pfdg&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565989)"><strong>FONTOBJ_pfdg</strong></a></p></td>
<td align="left"><p>检索指向<a href="https://msdn.microsoft.com/library/windows/hardware/ff565625" data-raw-source="[&lt;strong&gt;FD_GLYPHSET&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565625)"> <strong>FD_GLYPHSET</strong> </a>结构与指定的字体相关联。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565990" data-raw-source="[&lt;strong&gt;FONTOBJ_pifi&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565990)"><strong>FONTOBJ_pifi</strong></a></p></td>
<td align="left"><p>检索指向<a href="https://msdn.microsoft.com/library/windows/hardware/ff567418" data-raw-source="[&lt;strong&gt;IFIMETRICS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567418)"> <strong>IFIMETRICS</strong> </a>结构，描述关联的字体。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565993" data-raw-source="[&lt;strong&gt;FONTOBJ_pjOpenTypeTablePointer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565993)"><strong>FONTOBJ_pjOpenTypeTablePointer</strong></a></p></td>
<td align="left"><p>返回一个指向 OpenType 表的视图。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565996" data-raw-source="[&lt;strong&gt;FONTOBJ_pQueryGlyphAttrs&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565996)"><strong>FONTOBJ_pQueryGlyphAttrs</strong></a></p></td>
<td align="left"><p>返回有关字体的信息&#39;s 标志符号。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566001" data-raw-source="[&lt;strong&gt;FONTOBJ_pvTrueTypeFontFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566001)"><strong>FONTOBJ_pvTrueTypeFontFile</strong></a></p></td>
<td align="left"><p>检索指向 TrueType、 OpenType 或类型 1 的字体文件的视图。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566003" data-raw-source="[&lt;strong&gt;FONTOBJ_pwszFontFilePaths&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566003)"><strong>FONTOBJ_pwszFontFilePaths</strong></a></p></td>
<td align="left"><p>检索与字体相关联的文件路径。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566008" data-raw-source="[&lt;strong&gt;FONTOBJ_pxoGetXform&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566008)"><strong>FONTOBJ_pxoGetXform</strong></a></p></td>
<td align="left"><p>检索到设备 Notional 转换相关联的字体。 此转换是必需的驱动程序即可实现驱动程序所提供的字体。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566013" data-raw-source="[&lt;strong&gt;FONTOBJ_vGetInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566013)"><strong>FONTOBJ_vGetInfo</strong></a></p></td>
<td align="left"><p>返回描述关联的字体的信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569739" data-raw-source="[&lt;strong&gt;STROBJ_bEnum&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff569739)"><strong>STROBJ_bEnum</strong></a></p></td>
<td align="left"><p>枚举标志符号标识和指定 STROBJ 中的位置。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569740" data-raw-source="[&lt;strong&gt;STROBJ_bEnumPositionsOnly&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff569740)"><strong>STROBJ_bEnumPositionsOnly</strong></a></p></td>
<td align="left"><p>枚举标志符号标识和位置指定的文本字符串，但不会创建缓存的标志符号位图。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569741" data-raw-source="[&lt;strong&gt;STROBJ_bGetAdvanceWidths&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff569741)"><strong>STROBJ_bGetAdvanceWidths</strong></a></p></td>
<td align="left"><p>返回指定的标志符号组成的指定字符串的可能性大宽度的向量。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569742" data-raw-source="[&lt;strong&gt;STROBJ_dwGetCodePage&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff569742)"><strong>STROBJ_dwGetCodePage</strong></a></p></td>
<td align="left"><p>返回与指定 STROBJ 关联的代码页。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569743" data-raw-source="[&lt;strong&gt;STROBJ_fxBreakExtra&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff569743)"><strong>STROBJ_fxBreakExtra</strong></a></p></td>
<td align="left"><p>检索要添加到字符串中每个空格字符时显示和/或打印对齐的文本的额外空间量。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569745" data-raw-source="[&lt;strong&gt;STROBJ_vEnumStart&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff569745)"><strong>STROBJ_vEnumStart</strong></a></p></td>
<td align="left"><p>重新启动的枚举<a href="https://msdn.microsoft.com/library/windows/hardware/ff566824" data-raw-source="[&lt;strong&gt;GLYPHPOS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566824)"> <strong>GLYPHPOS</strong> </a>指定 STROBJ 的数组。 在后续枚举之前驱动程序应调用此函数。</p></td>
</tr>
</tbody>
</table>

 

 

 






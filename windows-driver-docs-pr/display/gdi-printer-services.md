---
title: GDI 打印机服务
description: GDI 打印机服务
ms.assetid: b63c9822-f737-42fb-a831-31d16b3495c9
keywords:
- GDI WDK Windows 2000 显示，打印机服务
- 图形驱动程序 WDK Windows 2000 显示，打印机服务
- 绘制 WDK GDI，打印机服务
- 打印机服务 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d604ec0aea2afee21c48d75005344dd68775fec7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374639"
---
# <a name="gdi-printer-services"></a>GDI 打印机服务


## <span id="ddk_gdi_printer_services_gg"></span><span id="DDK_GDI_PRINTER_SERVICES_GG"></span>


GDI 提供了大量的打印机驱动程序编写人员感兴趣的服务。 下表列出了这些服务。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564850" data-raw-source="[&lt;strong&gt;EngEnumForms&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564850)"><strong>EngEnumForms</strong></a></p></td>
<td align="left"><p>枚举指定打印机支持的窗体。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564938" data-raw-source="[&lt;strong&gt;EngGetForm&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564938)"><strong>EngGetForm</strong></a></p></td>
<td align="left"><p>获取指定的窗体 FORM_INFO_1 详细信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564945" data-raw-source="[&lt;strong&gt;EngGetPrinter&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564945)"><strong>EngGetPrinter</strong></a></p></td>
<td align="left"><p>检索有关指定的打印机信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564948" data-raw-source="[&lt;strong&gt;EngGetPrinterData&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564948)"><strong>EngGetPrinterData</strong></a></p></td>
<td align="left"><p>检索指定的打印机的配置数据。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564951" data-raw-source="[&lt;strong&gt;EngGetPrinterDataFileName&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564951)"><strong>EngGetPrinterDataFileName</strong></a></p></td>
<td align="left"><p>检索打印机的数据文件的字符串名称。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564954" data-raw-source="[&lt;strong&gt;EngGetPrinterDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564954)"><strong>EngGetPrinterDriver</strong></a></p></td>
<td align="left"><p>检索为指定的打印机驱动程序数据。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564972" data-raw-source="[&lt;strong&gt;EngMapFontFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564972)"><strong>EngMapFontFile</strong></a></p></td>
<td align="left"><p>已过时。 请参阅此表中的条目<strong>EngMapFontFileFD</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564973" data-raw-source="[&lt;strong&gt;EngMapFontFileFD&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564973)"><strong>EngMapFontFileFD</strong></a></p></td>
<td align="left"><p>如有必要，将字体文件映射到系统内存中，并将指针返回到文件中的字体数据的基位置。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564975" data-raw-source="[&lt;strong&gt;EngMarkBandingSurface&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564975)"><strong>EngMarkBandingSurface</strong></a></p></td>
<td align="left"><p>将指定的打印机面标记为联合的图面。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565020" data-raw-source="[&lt;strong&gt;EngSetPrinterData&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565020)"><strong>EngSetPrinterData</strong></a></p></td>
<td align="left"><p>已过时。 为指定的打印机设置的配置数据。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565441" data-raw-source="[&lt;strong&gt;EngUnmapFontFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565441)"><strong>EngUnmapFontFile</strong></a></p></td>
<td align="left"><p>已过时。 请参阅此表中的条目<strong>EngUnmapFontFileFD</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565445" data-raw-source="[&lt;strong&gt;EngUnmapFontFileFD&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565445)"><strong>EngUnmapFontFileFD</strong></a></p></td>
<td align="left"><p>取消映射系统内存中的指定的字体文件。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565467" data-raw-source="[&lt;strong&gt;EngWritePrinter&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565467)"><strong>EngWritePrinter</strong></a></p></td>
<td align="left"><p>允许打印机图形数据流发送到打印机硬件的 Dll。</p></td>
</tr>
</tbody>
</table>

 

 

 






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
ms.openlocfilehash: 0a454dca896140f004e12ba6627e124b84053259
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354729"
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
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engenumforms" data-raw-source="[&lt;strong&gt;EngEnumForms&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engenumforms)"><strong>EngEnumForms</strong></a></p></td>
<td align="left"><p>枚举指定打印机支持的窗体。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-enggetform" data-raw-source="[&lt;strong&gt;EngGetForm&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-enggetform)"><strong>EngGetForm</strong></a></p></td>
<td align="left"><p>获取指定的窗体 FORM_INFO_1 详细信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-enggetprinter" data-raw-source="[&lt;strong&gt;EngGetPrinter&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-enggetprinter)"><strong>EngGetPrinter</strong></a></p></td>
<td align="left"><p>检索有关指定的打印机信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-enggetprinterdata" data-raw-source="[&lt;strong&gt;EngGetPrinterData&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-enggetprinterdata)"><strong>EngGetPrinterData</strong></a></p></td>
<td align="left"><p>检索指定的打印机的配置数据。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-enggetprinterdatafilename" data-raw-source="[&lt;strong&gt;EngGetPrinterDataFileName&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-enggetprinterdatafilename)"><strong>EngGetPrinterDataFileName</strong></a></p></td>
<td align="left"><p>检索打印机的数据文件的字符串名称。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-enggetprinterdriver" data-raw-source="[&lt;strong&gt;EngGetPrinterDriver&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-enggetprinterdriver)"><strong>EngGetPrinterDriver</strong></a></p></td>
<td align="left"><p>检索为指定的打印机驱动程序数据。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engmapfontfile" data-raw-source="[&lt;strong&gt;EngMapFontFile&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engmapfontfile)"><strong>EngMapFontFile</strong></a></p></td>
<td align="left"><p>已过时。 请参阅此表中的条目<strong>EngMapFontFileFD</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engmapfontfilefd" data-raw-source="[&lt;strong&gt;EngMapFontFileFD&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engmapfontfilefd)"><strong>EngMapFontFileFD</strong></a></p></td>
<td align="left"><p>如有必要，将字体文件映射到系统内存中，并将指针返回到文件中的字体数据的基位置。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engmarkbandingsurface" data-raw-source="[&lt;strong&gt;EngMarkBandingSurface&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engmarkbandingsurface)"><strong>EngMarkBandingSurface</strong></a></p></td>
<td align="left"><p>将指定的打印机面标记为联合的图面。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engsetprinterdata" data-raw-source="[&lt;strong&gt;EngSetPrinterData&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engsetprinterdata)"><strong>EngSetPrinterData</strong></a></p></td>
<td align="left"><p>已过时。 为指定的打印机设置的配置数据。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engunmapfontfile" data-raw-source="[&lt;strong&gt;EngUnmapFontFile&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engunmapfontfile)"><strong>EngUnmapFontFile</strong></a></p></td>
<td align="left"><p>已过时。 请参阅此表中的条目<strong>EngUnmapFontFileFD</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engunmapfontfilefd" data-raw-source="[&lt;strong&gt;EngUnmapFontFileFD&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engunmapfontfilefd)"><strong>EngUnmapFontFileFD</strong></a></p></td>
<td align="left"><p>取消映射系统内存中的指定的字体文件。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engwriteprinter" data-raw-source="[&lt;strong&gt;EngWritePrinter&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engwriteprinter)"><strong>EngWritePrinter</strong></a></p></td>
<td align="left"><p>允许打印机图形数据流发送到打印机硬件的 Dll。</p></td>
</tr>
</tbody>
</table>

 

 

 






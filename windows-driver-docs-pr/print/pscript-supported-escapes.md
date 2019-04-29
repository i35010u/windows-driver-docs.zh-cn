---
title: Pscript 支持的转义符
description: Pscript 支持的转义符
ms.assetid: c0133355-fa3b-4117-bd38-b6a8b3898f94
keywords:
- PostScript 打印机驱动程序 WDK 打印，转义符
- Pscript WDK 打印，转义符
- 转义符 WDK Pscript
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24b5cb6b6cb2f0bb6e26622921a34fa492e64ca9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373469"
---
# <a name="pscript-supported-escapes"></a>Pscript 支持的转义符





Pscript5 打印机驱动程序支持以下转义符。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>退出</th>
<th>含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>BEGIN_PATH</p></td>
<td><p>打开一个路径。</p></td>
</tr>
<tr class="even">
<td><p>CHECKJPEGFORMAT</p></td>
<td><p>确定打印机是否可以处理 JPEG 图像。 有关此转义的详细信息，请参阅 Microsoft Windows SDK 文档中的 CHECKJPEGFORMAT。</p>
<p>此转义生成调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff556260" data-raw-source="[&lt;strong&gt;DrvQueryDeviceSupport&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556260)"> <strong>DrvQueryDeviceSupport</strong> </a>函数。</p></td>
</tr>
<tr class="odd">
<td><p>CHECKPNGFORMAT</p></td>
<td><p>确定打印机是否可以处理的 PNG 映像。 有关此转义的详细信息，请参阅 Windows SDK 文档中的 CHECKPNGFORMAT。</p>
<p>此转义生成调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff556260" data-raw-source="[&lt;strong&gt;DrvQueryDeviceSupport&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556260)"> <strong>DrvQueryDeviceSupport</strong> </a>函数。</p></td>
</tr>
<tr class="even">
<td><p>CLIP_TO_PATH</p></td>
<td><p>定义由路径界定的剪辑区域。</p></td>
</tr>
<tr class="odd">
<td><p>DOWNLOADHEADER</p></td>
<td><p>下载所有 procsets （也就是说，组的 PostScript 过程）。</p></td>
</tr>
<tr class="even">
<td><p>DRAWPATTERNRECT</p></td>
<td><p>通过 Hewlett Packard LaserJet 或 LaserJet 兼容打印机使用的模式和规则的功能的页控件语言 (PCL) 中创建空白、 灰度或纯黑色的矩形。 灰度是包含特定的黑色和白色像素的灰色模式。 有关此转义的详细信息，请参阅 Windows SDK 文档中的 DRAWPATTERNRECT。</p>
<p>此转义符，与在驱动程序相关联<a href="https://msdn.microsoft.com/library/windows/hardware/ff556217" data-raw-source="[&lt;strong&gt;DrvEscape&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556217)"> <strong>DrvEscape</strong> </a>函数。</p></td>
</tr>
<tr class="odd">
<td><p>ENCAPSULATED_POSTSCRIPT</p></td>
<td><p>内嵌的 PostScript (EPS) 数据发送到打印机。</p>
<p>Microsoft Windows NT 4.0 打印机驱动程序不支持此转义。</p>
<p>此转义符，与在驱动程序相关联<a href="https://msdn.microsoft.com/library/windows/hardware/ff556203" data-raw-source="[&lt;strong&gt;DrvDrawEscape&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556203)"> <strong>DrvDrawEscape</strong> </a>函数。</p></td>
</tr>
<tr class="even">
<td><p>END_PATH</p></td>
<td><p>结束路径。</p></td>
</tr>
<tr class="odd">
<td><p>EPSPRINTING</p></td>
<td><p>指示开始或结束 EPS 打印。</p>
<p>图形设备接口 (GDI) 截获此转义，并将其翻译为非 DrvEscape DDI 调用。 打印机驱动程序不会接收此转义。</p></td>
</tr>
<tr class="even">
<td><p>GET_PS_FEATURESETTING</p></td>
<td><p>获取有关指定的功能设置为 PostScript 驱动程序的信息。</p>
<p>有关此转义的详细信息，请参阅 Windows SDK 文档中的 GET_PS_FEATURESETTING。</p></td>
</tr>
<tr class="odd">
<td><p>GETTECHNOLOGY</p></td>
<td><p>获取打印机的普通的技术类型。 打印机驱动程序后 Windows 3.0 编写的 Windows 操作系统版本可能不支持此转义。</p></td>
</tr>
<tr class="even">
<td><p>传递</p></td>
<td><p>数据将直接发送到在兼容性模式或 GDI 为中心的模式下的 PostScript 打印机驱动程序。 在 PostScript 为中心的模式下的 postScript 的打印机驱动程序不支持此转义。</p>
<p>有关此转义的详细信息，请参阅 Windows SDK 文档中的传递。</p></td>
</tr>
<tr class="odd">
<td><p>POSTSCRIPT_DATA</p></td>
<td><p>数据将直接发送到打印机驱动程序。 此转义是传递转义到相同的但 PostScript 的打印机驱动程序在 Windows NT 4.0 兼容性模式下支持此转义。</p>
<p>有关此转义的详细信息，请参阅 Windows SDK 文档中的 POSTSCRIPT_DATA。</p></td>
</tr>
<tr class="even">
<td><p>POSTSCRIPT_IDENTIFY</p></td>
<td><p>设置为 GDI 为中心或 PostScript 为中心模式的 PostScript 打印机驱动程序。</p>
<p>有关此转义的详细信息，请参阅 Windows SDK 文档中的 POSTSCRIPT_IDENTIFY。</p></td>
</tr>
<tr class="odd">
<td><p>POSTSCRIPT_IGNORE</p></td>
<td><p>禁止显示输出。</p>
<p>仅 PostScript 打印机驱动程序在 Windows NT 4.0 兼容性模式下或在 GDI 为中心的模式下支持此转义。 在 PostScript 为中心的模式下的 postScript 的打印机驱动程序不支持此转义。</p></td>
</tr>
<tr class="even">
<td><p>POSTSCRIPT_INJECTION</p></td>
<td><p>PostScript 作业流中插入原始数据的块。</p>
<p>有关此转义的详细信息，请参阅 Windows SDK 文档中的 POSTSCRIPT_INJECTION。</p></td>
</tr>
<tr class="odd">
<td><p>POSTSCRIPT_PASSTHROUGH</p></td>
<td><p>数据将直接发送到在 Windows NT 4.0 兼容性模式或 PostScript 为中心模式的 PostScript 打印机驱动程序。 在 GDI 为中心的模式下的 postScript 的打印机驱动程序不支持此转义。</p>
<p>有关此转义的详细信息，请参阅 Windows SDK 文档中的 POSTSCRIPT_PASSTHROUGH。</p></td>
</tr>
<tr class="even">
<td><p>QUERYESCSUPPORT</p></td>
<td><p>确定设备驱动程序是否实现特定的转义。</p>
<p>有关此转义的详细信息，请参阅 Windows SDK 文档中的 QUERYESCSUPPORT。</p></td>
</tr>
<tr class="odd">
<td><p>SETCOPYCOUNT</p></td>
<td><p>设置要打印的份数。</p>
<p>已被取代此转义<strong>DocumentProperties</strong>并<strong>PrinterProperties</strong> Windows SDK 文档中所述的函数。</p>
<p>有关此转义的详细信息，请参阅 Windows SDK 文档中的 SETCOPYCOUNT。</p></td>
</tr>
<tr class="even">
<td><p>SPCLPASSTHROUGH2</p></td>
<td><p>使应用程序包括专用的过程和其他资源在文档级别保存上下文。</p>
<p>有关此转义的详细信息，请参阅 Windows SDK 文档中的 SPCLPASSTHROUGH2。</p></td>
</tr>
</tbody>
</table>

 

以下转义符在 Windows NT 4.0 中新增但不再受支持：

-   ADDMSTT

-   IGNORESTARTPAGE

-   NOFIRSTSAVE

以下转义符是已过时，仅用于 16 位版本的 Windows 操作系统兼容性提供。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>退出</th>
<th>备注</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ABORTDOC</p></td>
<td><p>已被取代此转义<strong>AbortDoc</strong>函数，Windows SDK 文档中所述。</p></td>
</tr>
<tr class="even">
<td><p>ENDDOC</p></td>
<td><p>已被取代此转义<strong>EndDoc</strong>函数，Windows SDK 文档中所述。</p></td>
</tr>
<tr class="odd">
<td><p>GETPHYSPAGESIZE</p></td>
<td><p>中的 PHYSICALWIDTH 和 PHYSICALHEIGHT 值已被此转义<strong>GetDeviceCaps</strong>函数，Windows SDK 文档中所述。</p></td>
</tr>
<tr class="even">
<td><p>GETPRINTINGOFFSET</p></td>
<td><p>中的 PHYSICALOFFSETX 和 PHYSICALOFFSETY 值已被此转义<strong>GetDeviceCaps</strong>函数，Windows SDK 文档中所述。</p></td>
</tr>
<tr class="odd">
<td><p>GETSCALINGFACTOR</p></td>
<td><p>中的 SCALINGFACTORX 和 SCALINGFACTORY 值已被此转义<strong>GetDeviceCaps</strong>函数，Windows SDK 文档中所述。</p></td>
</tr>
<tr class="even">
<td><p>NEWFRAME</p></td>
<td><p>已被取代此转义<strong>EndPage</strong>函数，这将结束页。 与 NEWFRAME，不同<strong>EndPage</strong>打印一个页面之后，将始终调用。 <strong>EndPage</strong> Windows SDK 文档中所述。</p></td>
</tr>
<tr class="odd">
<td><p>NEXTBAND</p></td>
<td><p>不再使用带区信息。</p></td>
</tr>
<tr class="even">
<td><p>SETABORTPROC</p></td>
<td><p>已被取代此转义<strong>SetAbortProc</strong>函数，Windows SDK 文档中所述。</p></td>
</tr>
<tr class="odd">
<td><p>SETCOPYCOUNT</p></td>
<td><p>已被取代此转义<strong>DocumentProperties</strong>并<strong>PrinterProperties</strong> Windows SDK 文档中所述的函数。</p></td>
</tr>
<tr class="even">
<td><p>STARTDOC</p></td>
<td><p>已被取代此转义<strong>StartDoc</strong>函数，Windows SDK 文档中所述。</p></td>
</tr>
</tbody>
</table>

 

 

 





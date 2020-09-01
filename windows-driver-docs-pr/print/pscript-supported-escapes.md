---
title: Pscript 支持的转义符
description: Pscript 支持的转义符
ms.assetid: c0133355-fa3b-4117-bd38-b6a8b3898f94
keywords:
- PostScript 打印机驱动程序 WDK 打印，转义
- Pscript WDK 打印，转义
- 转义 WDK Pscript
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a17eb450b5dae3dd0edc371e9a1ff363d1106b3
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216332"
---
# <a name="pscript-supported-escapes"></a>Pscript 支持的转义符





Pscript5 打印机驱动程序支持以下转义。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Escape</th>
<th>含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>BEGIN_PATH</p></td>
<td><p>打开路径。</p></td>
</tr>
<tr class="even">
<td><p>CHECKJPEGFORMAT</p></td>
<td><p>确定打印机是否可以处理 JPEG 图像。 有关此转义的详细信息，请参阅 Microsoft Windows SDK 文档中的 CHECKJPEGFORMAT。</p>
<p>此转义将生成对 <a href="https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvquerydevicesupport" data-raw-source="[&lt;strong&gt;DrvQueryDeviceSupport&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvquerydevicesupport)"><strong>DrvQueryDeviceSupport</strong></a> 函数的调用。</p></td>
</tr>
<tr class="odd">
<td><p>CHECKPNGFORMAT</p></td>
<td><p>确定打印机是否可以处理 PNG 图像。 有关此转义的详细信息，请参阅 Windows SDK 文档中的 CHECKPNGFORMAT。</p>
<p>此转义将生成对 <a href="https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvquerydevicesupport" data-raw-source="[&lt;strong&gt;DrvQueryDeviceSupport&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvquerydevicesupport)"><strong>DrvQueryDeviceSupport</strong></a> 函数的调用。</p></td>
</tr>
<tr class="even">
<td><p>CLIP_TO_PATH</p></td>
<td><p>定义按路径绑定的剪辑区域。</p></td>
</tr>
<tr class="odd">
<td><p>DOWNLOADHEADER</p></td>
<td><p>下载所有 procsets (，即 PostScript 过程) 集。</p></td>
</tr>
<tr class="even">
<td><p>DRAWPATTERNRECT</p></td>
<td><p>通过使用页面控件语言的模式和规则功能 (PCL) 在 Hewlett Packard LaserJet 或 LaserJet 兼容的打印机上，创建一个白色、灰度或实心黑色矩形。 灰度是一种灰色模式，其中包含黑色和白色像素的特定混合。 有关此转义的详细信息，请参阅 Windows SDK 文档中的 DRAWPATTERNRECT。</p>
<p>此 escape 与驱动程序的 <a href="https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvescape" data-raw-source="[&lt;strong&gt;DrvEscape&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvescape)"><strong>DrvEscape</strong></a> 函数相关联。</p></td>
</tr>
<tr class="odd">
<td><p>ENCAPSULATED_POSTSCRIPT</p></td>
<td><p>将封装的 PostScript (EPS) 数据发送到打印机。</p>
<p>Microsoft Windows NT 4.0 打印机驱动程序不支持此转义。</p>
<p>此 escape 与驱动程序的 <a href="https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvdrawescape" data-raw-source="[&lt;strong&gt;DrvDrawEscape&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvdrawescape)"><strong>DrvDrawEscape</strong></a> 函数相关联。</p></td>
</tr>
<tr class="even">
<td><p>END_PATH</p></td>
<td><p>结束路径。</p></td>
</tr>
<tr class="odd">
<td><p>EPSPRINTING</p></td>
<td><p>指示 EPS 打印的开始或结束。</p>
<p>图形设备接口 (GDI) 会截获此转义，并将其转换为非 DrvEscape 的 DDI 调用。 打印机驱动程序未收到此转义符。</p></td>
</tr>
<tr class="even">
<td><p>GET_PS_FEATURESETTING</p></td>
<td><p>获取有关 PostScript 驱动程序的指定功能设置的信息。</p>
<p>有关此转义的详细信息，请参阅 Windows SDK 文档中的 GET_PS_FEATURESETTING。</p></td>
</tr>
<tr class="odd">
<td><p>GETTECHNOLOGY</p></td>
<td><p>获取打印机的常规技术类型。 Windows 3.0 之后为 Windows 操作系统版本编写的打印机驱动程序可能不支持此转义。</p></td>
</tr>
<tr class="even">
<td><p>直通</p></td>
<td><p>将数据直接发送到兼容模式或以 GDI 为中心的模式下的 PostScript 打印机驱动程序。 Postscript 模式下的 PostScript 打印机驱动程序不支持此转义。</p>
<p>有关此转义的详细信息，请参阅 Windows SDK 文档中的直通。</p></td>
</tr>
<tr class="odd">
<td><p>POSTSCRIPT_DATA</p></td>
<td><p>直接将数据发送到打印机驱动程序。 此转义与传递转义完全相同，只是 PostScript 打印机驱动程序仅支持 Windows NT 4.0 兼容模式下的此转义。</p>
<p>有关此转义的详细信息，请参阅 Windows SDK 文档中的 POSTSCRIPT_DATA。</p></td>
</tr>
<tr class="even">
<td><p>POSTSCRIPT_IDENTIFY</p></td>
<td><p>将 PostScript 打印机驱动程序设置为以 GDI 为中心或以 PostScript 模式。</p>
<p>有关此转义的详细信息，请参阅 Windows SDK 文档中的 POSTSCRIPT_IDENTIFY。</p></td>
</tr>
<tr class="odd">
<td><p>POSTSCRIPT_IGNORE</p></td>
<td><p>取消输出。</p>
<p>只有 Windows NT 4.0 兼容模式或以 GDI 为中心的模式中的 PostScript 打印机驱动程序支持此转义。 Postscript 模式下的 PostScript 打印机驱动程序不支持此转义。</p></td>
</tr>
<tr class="even">
<td><p>POSTSCRIPT_INJECTION</p></td>
<td><p>在 PostScript 作业流中插入原始数据块。</p>
<p>有关此转义的详细信息，请参阅 Windows SDK 文档中的 POSTSCRIPT_INJECTION。</p></td>
</tr>
<tr class="odd">
<td><p>POSTSCRIPT_PASSTHROUGH</p></td>
<td><p>在 Windows NT 4.0 兼容性模式或以 PostScript 模式模式下直接将数据发送到 PostScript 打印机驱动程序。 以 GDI 为中心的模式中的 PostScript 打印机驱动程序不支持此转义。</p>
<p>有关此转义的详细信息，请参阅 Windows SDK 文档中的 POSTSCRIPT_PASSTHROUGH。</p></td>
</tr>
<tr class="even">
<td><p>QUERYESCSUPPORT</p></td>
<td><p>确定设备驱动程序是否实现了特定的转义。</p>
<p>有关此转义的详细信息，请参阅 Windows SDK 文档中的 QUERYESCSUPPORT。</p></td>
</tr>
<tr class="odd">
<td><p>SETCOPYCOUNT</p></td>
<td><p>设置要打印的份数。</p>
<p>此转义已由 Windows SDK 文档中所述的 <strong>DocumentProperties</strong> 和 <strong>PrinterProperties</strong> 函数所取代。</p>
<p>有关此转义的详细信息，请参阅 Windows SDK 文档中的 SETCOPYCOUNT。</p></td>
</tr>
<tr class="even">
<td><p>SPCLPASSTHROUGH2</p></td>
<td><p>使应用程序能够将私有过程和其他资源包含在文档级别-保存上下文中。</p>
<p>有关此转义的详细信息，请参阅 Windows SDK 文档中的 SPCLPASSTHROUGH2。</p></td>
</tr>
</tbody>
</table>

 

以下转义是在 Windows NT 4.0 中添加的，但不再受支持：

-   ADDMSTT

-   IGNORESTARTPAGE

-   NOFIRSTSAVE

以下转义已过时，仅提供与16位版本的 Windows 操作系统的兼容性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Escape</th>
<th>注释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ABORTDOC</p></td>
<td><p>此转义已被 <strong>AbortDoc</strong> 函数取代，该函数在 Windows SDK 文档中进行了介绍。</p></td>
</tr>
<tr class="even">
<td><p>ENDDOC</p></td>
<td><p>此转义已被 <strong>EndDoc</strong> 函数取代，该函数在 Windows SDK 文档中进行了介绍。</p></td>
</tr>
<tr class="odd">
<td><p>GETPHYSPAGESIZE</p></td>
<td><p>在 Windows SDK 文档中介绍了 <strong>GetDeviceCaps</strong> 函数中的 PHYSICALWIDTH 和 PHYSICALHEIGHT 值。</p></td>
</tr>
<tr class="even">
<td><p>GETPRINTINGOFFSET</p></td>
<td><p>在 Windows SDK 文档中介绍了 <strong>GetDeviceCaps</strong> 函数中的 PHYSICALOFFSETX 和 PHYSICALOFFSETY 值。</p></td>
</tr>
<tr class="odd">
<td><p>GETSCALINGFACTOR</p></td>
<td><p>在 Windows SDK 文档中介绍了 <strong>GetDeviceCaps</strong> 函数中的 SCALINGFACTORX 和 SCALINGFACTORY 值。</p></td>
</tr>
<tr class="even">
<td><p>NEWFRAME</p></td>
<td><p>此 escape 已被 <strong>EndPage</strong> 函数取代，后者将结束页面。 与 NEWFRAME 不同，打印页面后始终会调用 <strong>EndPage</strong> 。 Windows SDK 文档中介绍了<strong>EndPage</strong> 。</p></td>
</tr>
<tr class="odd">
<td><p>NEXTBAND</p></td>
<td><p>不再使用带区信息。</p></td>
</tr>
<tr class="even">
<td><p>SETABORTPROC</p></td>
<td><p>此转义已被 <strong>SetAbortProc</strong> 函数取代，该函数在 Windows SDK 文档中进行了介绍。</p></td>
</tr>
<tr class="odd">
<td><p>SETCOPYCOUNT</p></td>
<td><p>此转义已由 Windows SDK 文档中所述的 <strong>DocumentProperties</strong> 和 <strong>PrinterProperties</strong> 函数所取代。</p></td>
</tr>
<tr class="even">
<td><p>STARTDOC</p></td>
<td><p>此转义已被 <strong>StartDoc</strong> 函数取代，该函数在 Windows SDK 文档中进行了介绍。</p></td>
</tr>
</tbody>
</table>

 

 


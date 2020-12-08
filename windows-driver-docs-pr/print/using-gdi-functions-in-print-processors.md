---
title: 使用打印处理器中的 GDI 函数
description: 使用打印处理器中的 GDI 函数
keywords:
- EMF 记录播放 WDK 打印处理器
- GDI 函数 WDK 打印处理器
- NT EMF WDK 打印处理器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 61f9df57e346852b35a5dd11704bc9bccc6efa3b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785993"
---
# <a name="using-gdi-functions-in-print-processors"></a>使用打印处理器中的 GDI 函数





一组用户模式 GDI 函数由 Gdi32.dll 导出，供处理基于 NT 的操作系统 EMF 作为输入格式的打印处理器使用。 下表列出了提供的函数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>函数名称</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/winppi/nf-winppi-gdideletespoolfilehandle" data-raw-source="[&lt;strong&gt;GdiDeleteSpoolFileHandle&lt;/strong&gt;](/windows-hardware/drivers/ddi/winppi/nf-winppi-gdideletespoolfilehandle)"><strong>GdiDeleteSpoolFileHandle</strong></a></p></td>
<td><p>释放假脱机文件句柄。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/winppi/nf-winppi-gdienddocemf" data-raw-source="[&lt;strong&gt;GdiEndDocEMF&lt;/strong&gt;](/windows-hardware/drivers/ddi/winppi/nf-winppi-gdienddocemf)"><strong>GdiEndDocEMF</strong></a></p></td>
<td><p>完成打印作业文档的 EMF 播放操作。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/winppi/nf-winppi-gdiendpageemf" data-raw-source="[&lt;strong&gt;GdiEndPageEMF&lt;/strong&gt;](/windows-hardware/drivers/ddi/winppi/nf-winppi-gdiendpageemf)"><strong>GdiEndPageEMF</strong></a></p></td>
<td><p>为物理页面完成 EMF 播放操作，并从打印机中弹出页面。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/winppi/nf-winppi-gdigetdc" data-raw-source="[&lt;strong&gt;GdiGetDC&lt;/strong&gt;](/windows-hardware/drivers/ddi/winppi/nf-winppi-gdigetdc)"><strong>GdiGetDC</strong></a></p></td>
<td><p>返回打印机设备上下文的句柄。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/winppi/nf-winppi-gdigetdevmodeforpage" data-raw-source="[&lt;strong&gt;GdiGetDevmodeForPage&lt;/strong&gt;](/windows-hardware/drivers/ddi/winppi/nf-winppi-gdigetdevmodeforpage)"><strong>GdiGetDevmodeForPage</strong></a></p></td>
<td><p>返回文档页的 <a href="/windows/win32/api/wingdi/ns-wingdi-devmodew" data-raw-source="[&lt;strong&gt;DEVMODEW&lt;/strong&gt;](/windows/win32/api/wingdi/ns-wingdi-devmodew)"><strong>DEVMODEW</strong></a> 结构。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/winppi/nf-winppi-gdigetpagecount" data-raw-source="[&lt;strong&gt;GdiGetPageCount&lt;/strong&gt;](/windows-hardware/drivers/ddi/winppi/nf-winppi-gdigetpagecount)"><strong>GdiGetPageCount</strong></a></p></td>
<td><p>返回文档页的数目。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/winppi/nf-winppi-gdigetpagehandle" data-raw-source="[&lt;strong&gt;GdiGetPageHandle&lt;/strong&gt;](/windows-hardware/drivers/ddi/winppi/nf-winppi-gdigetpagehandle)"><strong>GdiGetPageHandle</strong></a></p></td>
<td><p>返回文档页的句柄。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/winppi/nf-winppi-gdigetspoolfilehandle" data-raw-source="[&lt;strong&gt;GdiGetSpoolFileHandle&lt;/strong&gt;](/windows-hardware/drivers/ddi/winppi/nf-winppi-gdigetspoolfilehandle)"><strong>GdiGetSpoolFileHandle</strong></a></p></td>
<td><p>返回假脱机文件句柄，作为其他 GDI 函数的输入需要。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/winppi/nf-winppi-gdiplaypageemf" data-raw-source="[&lt;strong&gt;GdiPlayPageEMF&lt;/strong&gt;](/windows-hardware/drivers/ddi/winppi/nf-winppi-gdiplaypageemf)"><strong>GdiPlayPageEMF</strong></a></p></td>
<td><p>播放与文档页关联的 EMF 记录。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/winppi/nf-winppi-gdiresetdcemf" data-raw-source="[&lt;strong&gt;GdiResetDCEMF&lt;/strong&gt;](/windows-hardware/drivers/ddi/winppi/nf-winppi-gdiresetdcemf)"><strong>GdiResetDCEMF</strong></a></p></td>
<td><p>重置打印机的设备上下文。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/winppi/nf-winppi-gdistartdocemf" data-raw-source="[&lt;strong&gt;GdiStartDocEMF&lt;/strong&gt;](/windows-hardware/drivers/ddi/winppi/nf-winppi-gdistartdocemf)"><strong>GdiStartDocEMF</strong></a></p></td>
<td><p>执行打印作业文档的初始化操作。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/winppi/nf-winppi-gdistartpageemf" data-raw-source="[&lt;strong&gt;GdiStartPageEMF&lt;/strong&gt;](/windows-hardware/drivers/ddi/winppi/nf-winppi-gdistartpageemf)"><strong>GdiStartPageEMF</strong></a></p></td>
<td><p>为物理页执行初始化操作。</p></td>
</tr>
</tbody>
</table>

 

EMF 打印处理器的 [**PrintDocumentOnPrintProcessor**](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-printdocumentonprintprocessor) 应调用 [**GdiGetSpoolFileHandle**](/windows-hardware/drivers/ddi/winppi/nf-winppi-gdigetspoolfilehandle) 来获取假脱机文件句柄，并使用 [**GdiGetDC**](/windows-hardware/drivers/ddi/winppi/nf-winppi-gdigetdc) 获取打印机的设备上下文句柄。 然后，它可以执行以下步骤：

-   对于每个打印作业文档，必须先调用 [**GdiStartDocEMF**](/windows-hardware/drivers/ddi/winppi/nf-winppi-gdistartdocemf) ，然后才能播放任何 emf 记录，并且在播放完最后一个 emf 记录后必须调用 [**GdiEndDocEMF**](/windows-hardware/drivers/ddi/winppi/nf-winppi-gdienddocemf) 。

-   对于要打印的每个物理页，必须先调用 [**GdiStartPageEMF**](/windows-hardware/drivers/ddi/winppi/nf-winppi-gdistartpageemf) ，然后才能在页面上绘制任何文档页，并在物理页上绘制最后一个文档页后，必须调用 [**GdiEndPageEMF**](/windows-hardware/drivers/ddi/winppi/nf-winppi-gdiendpageemf) 。

-   对于要在物理页面上绘制的每个文档页，必须调用 [**GdiGetDevmodeForPage**](/windows-hardware/drivers/ddi/winppi/nf-winppi-gdigetdevmodeforpage) 来确定是否在绘制上一个文档页面后，DEVMODE 结构内容已发生更改。 如果 DEVMODE 发生了更改，则必须通过调用 [**GdiEndPageEMF**](/windows-hardware/drivers/ddi/winppi/nf-winppi-gdiendpageemf) 和 [**GdiStartPageEMF**](/windows-hardware/drivers/ddi/winppi/nf-winppi-gdistartpageemf))  (启动新的物理页面，并且必须通过调用 [**GdiResetDCEMF**](/windows-hardware/drivers/ddi/winppi/nf-winppi-gdiresetdcemf)来更新打印机的设备上下文。 通过首先调用 [**GdiGetPageHandle**](/windows-hardware/drivers/ddi/winppi/nf-winppi-gdigetpagehandle) 以获取文档页句柄，然后调用 [**GdiPlayPageEMF**](/windows-hardware/drivers/ddi/winppi/nf-winppi-gdiplaypageemf) 来绘制页面，可以在物理页面上绘制文档页。

完全绘制作业后，打印处理器必须调用 [**GdiDeleteSpoolFileHandle**](/windows-hardware/drivers/ddi/winppi/nf-winppi-gdideletespoolfilehandle)。

如果打印处理器需要总计页面计数，才能开始打印页面 (如为了按相反的顺序打印页面) 可以调用 [**GdiGetPageCount**](/windows-hardware/drivers/ddi/winppi/nf-winppi-gdigetpagecount)，但此函数不会返回，直到后台打印结束，因而禁用后台打印功能。

如果打印处理器使用这些 GDI 函数，则其 [**EnumPrintProcessorDatatypes**](/windows-hardware/drivers/ddi/winspool/nf-winspool-enumprintprocessordatatypesa) 函数必须以支持的数据类型（表示泛型 Windows 2000 和更高版本 EMF 格式）返回 "NT EMF"。 打印处理器不得修改 EMF 记录。


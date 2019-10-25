---
title: 使用打印处理器中的 GDI 函数
description: 使用打印处理器中的 GDI 函数
ms.assetid: 2ad62308-ab42-4475-ac42-f753d5091251
keywords:
- EMF 记录播放 WDK 打印处理器
- GDI 函数 WDK 打印处理器
- NT EMF WDK 打印处理器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2992d80e77bf58cc57a76d4678e6e049a9dde1c5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844197"
---
# <a name="using-gdi-functions-in-print-processors"></a>使用打印处理器中的 GDI 函数





一组用户模式 GDI 函数由 Gdi32 导出，供处理基于 NT 的操作系统 EMF 作为输入格式的打印处理器使用。 下表列出了提供的函数。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdideletespoolfilehandle" data-raw-source="[&lt;strong&gt;GdiDeleteSpoolFileHandle&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdideletespoolfilehandle)"><strong>GdiDeleteSpoolFileHandle</strong></a></p></td>
<td><p>释放假脱机文件句柄。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdienddocemf" data-raw-source="[&lt;strong&gt;GdiEndDocEMF&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdienddocemf)"><strong>GdiEndDocEMF</strong></a></p></td>
<td><p>完成打印作业文档的 EMF 播放操作。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdiendpageemf" data-raw-source="[&lt;strong&gt;GdiEndPageEMF&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdiendpageemf)"><strong>GdiEndPageEMF</strong></a></p></td>
<td><p>为物理页面完成 EMF 播放操作，并从打印机中弹出页面。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdigetdc" data-raw-source="[&lt;strong&gt;GdiGetDC&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdigetdc)"><strong>GdiGetDC</strong></a></p></td>
<td><p>返回打印机设备上下文的句柄。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdigetdevmodeforpage" data-raw-source="[&lt;strong&gt;GdiGetDevmodeForPage&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdigetdevmodeforpage)"><strong>GdiGetDevmodeForPage</strong></a></p></td>
<td><p>返回文档页的<a href="https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew" data-raw-source="[&lt;strong&gt;DEVMODEW&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)"><strong>DEVMODEW</strong></a>结构。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdigetpagecount" data-raw-source="[&lt;strong&gt;GdiGetPageCount&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdigetpagecount)"><strong>GdiGetPageCount</strong></a></p></td>
<td><p>返回文档页的数目。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdigetpagehandle" data-raw-source="[&lt;strong&gt;GdiGetPageHandle&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdigetpagehandle)"><strong>GdiGetPageHandle</strong></a></p></td>
<td><p>返回文档页的句柄。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdigetspoolfilehandle" data-raw-source="[&lt;strong&gt;GdiGetSpoolFileHandle&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdigetspoolfilehandle)"><strong>GdiGetSpoolFileHandle</strong></a></p></td>
<td><p>返回假脱机文件句柄，作为其他 GDI 函数的输入需要。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdiplaypageemf" data-raw-source="[&lt;strong&gt;GdiPlayPageEMF&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdiplaypageemf)"><strong>GdiPlayPageEMF</strong></a></p></td>
<td><p>播放与文档页关联的 EMF 记录。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdiresetdcemf" data-raw-source="[&lt;strong&gt;GdiResetDCEMF&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdiresetdcemf)"><strong>GdiResetDCEMF</strong></a></p></td>
<td><p>重置打印机的设备上下文。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdistartdocemf" data-raw-source="[&lt;strong&gt;GdiStartDocEMF&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdistartdocemf)"><strong>GdiStartDocEMF</strong></a></p></td>
<td><p>执行打印作业文档的初始化操作。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdistartpageemf" data-raw-source="[&lt;strong&gt;GdiStartPageEMF&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdistartpageemf)"><strong>GdiStartPageEMF</strong></a></p></td>
<td><p>为物理页执行初始化操作。</p></td>
</tr>
</tbody>
</table>

 

EMF 打印处理器的[**PrintDocumentOnPrintProcessor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-printdocumentonprintprocessor)应调用[**GdiGetSpoolFileHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdigetspoolfilehandle)来获取假脱机文件句柄，并使用[**GdiGetDC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdigetdc)获取打印机的设备上下文句柄。 然后，它可以执行以下步骤：

-   对于每个打印作业文档，必须先调用[**GdiStartDocEMF**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdistartdocemf) ，然后才能播放任何 emf 记录，并且在播放完最后一个 emf 记录后必须调用[**GdiEndDocEMF**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdienddocemf) 。

-   对于要打印的每个物理页，必须先调用[**GdiStartPageEMF**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdistartpageemf) ，然后才能在页面上绘制任何文档页，并在物理页上绘制最后一个文档页后，必须调用[**GdiEndPageEMF**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdiendpageemf) 。

-   对于要在物理页面上绘制的每个文档页，必须调用[**GdiGetDevmodeForPage**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdigetdevmodeforpage)来确定是否在绘制上一个文档页面后，DEVMODE 结构内容已发生更改。 如果 DEVMODE 已更改，则必须通过调用[**GdiEndPageEMF**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdiendpageemf)和[**GdiStartPageEMF**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdistartpageemf)来启动一个新的物理页面，并且必须通过调用[**GdiResetDCEMF**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdiresetdcemf)更新打印机的设备上下文。 通过首先调用[**GdiGetPageHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdigetpagehandle)以获取文档页句柄，然后调用[**GdiPlayPageEMF**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdiplaypageemf)来绘制页面，可以在物理页面上绘制文档页。

完全绘制作业后，打印处理器必须调用[**GdiDeleteSpoolFileHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdideletespoolfilehandle)。

如果打印处理器需要总计页面计数，然后才能开始打印页面（例如，按逆序打印页面），则它可以调用[**GdiGetPageCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdigetpagecount)，但此函数不会返回，直到后台打印结束，因而禁用打印功能后台处理.

如果打印处理器使用这些 GDI 函数，则其[**EnumPrintProcessorDatatypes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winspool/nf-winspool-enumprintprocessordatatypesa)函数必须以支持的数据类型（表示泛型 Windows 2000 和更高版本 EMF 格式）返回 "NT EMF"。 打印处理器不得修改 EMF 记录。

 

 





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
ms.openlocfilehash: d9d512cd7f12f6e3929f1994f00bb5a945c551b5
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349418"
---
# <a name="using-gdi-functions-in-print-processors"></a>使用打印处理器中的 GDI 函数





一组用户模式下 GDI 函数 Gdi32.dll 导出以供处理 NT 基于操作系统系统作为输入格式的 EMF 打印处理器。 下表列出了提供的函数。

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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549449" data-raw-source="[&lt;strong&gt;GdiDeleteSpoolFileHandle&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549449)"><strong>GdiDeleteSpoolFileHandle</strong></a></p></td>
<td><p>释放后台打印文件句柄。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549463" data-raw-source="[&lt;strong&gt;GdiEndDocEMF&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549463)"><strong>GdiEndDocEMF</strong></a></p></td>
<td><p>完成打印作业文档的 EMF 播放操作。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549468" data-raw-source="[&lt;strong&gt;GdiEndPageEMF&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549468)"><strong>GdiEndPageEMF</strong></a></p></td>
<td><p>完成一个物理页的 EMF 播放操作并弹出从打印机页。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549470" data-raw-source="[&lt;strong&gt;GdiGetDC&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549470)"><strong>GdiGetDC</strong></a></p></td>
<td><p>返回的句柄的打印机设备上下文。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549478" data-raw-source="[&lt;strong&gt;GdiGetDevmodeForPage&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549478)"><strong>GdiGetDevmodeForPage</strong></a></p></td>
<td><p>返回的文档页面<a href="https://msdn.microsoft.com/library/windows/hardware/ff552837" data-raw-source="[&lt;strong&gt;DEVMODEW&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552837)"> <strong>DEVMODEW</strong> </a>结构。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549492" data-raw-source="[&lt;strong&gt;GdiGetPageCount&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549492)"><strong>GdiGetPageCount</strong></a></p></td>
<td><p>返回文档页面的数量。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549505" data-raw-source="[&lt;strong&gt;GdiGetPageHandle&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549505)"><strong>GdiGetPageHandle</strong></a></p></td>
<td><p>返回的句柄的文档页。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549517" data-raw-source="[&lt;strong&gt;GdiGetSpoolFileHandle&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549517)"><strong>GdiGetSpoolFileHandle</strong></a></p></td>
<td><p>返回作为其他 GDI 函数的输入所需的假脱机文件句柄。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549524" data-raw-source="[&lt;strong&gt;GdiPlayPageEMF&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549524)"><strong>GdiPlayPageEMF</strong></a></p></td>
<td><p>播放与文档页关联的 EMF 记录。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549529" data-raw-source="[&lt;strong&gt;GdiResetDCEMF&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549529)"><strong>GdiResetDCEMF</strong></a></p></td>
<td><p>重置打印机设备上下文。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549534" data-raw-source="[&lt;strong&gt;GdiStartDocEMF&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549534)"><strong>GdiStartDocEMF</strong></a></p></td>
<td><p>执行打印作业文档的初始化操作。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549543" data-raw-source="[&lt;strong&gt;GdiStartPageEMF&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549543)"><strong>GdiStartPageEMF</strong></a></p></td>
<td><p>执行物理页的初始化操作。</p></td>
</tr>
</tbody>
</table>

 

EMF 打印处理器的[ **PrintDocumentOnPrintProcessor** ](https://msdn.microsoft.com/library/windows/hardware/ff560724)应调用[ **GdiGetSpoolFileHandle** ](https://msdn.microsoft.com/library/windows/hardware/ff549517)获取假脱机文件处理和[ **GdiGetDC** ](https://msdn.microsoft.com/library/windows/hardware/ff549470)以获得打印机的设备上下文句柄。 然后，它可以执行以下步骤：

-   对于每个打印作业的文档， [ **GdiStartDocEMF** ](https://msdn.microsoft.com/library/windows/hardware/ff549534)播放任何 EMF 记录之前，必须调用并[ **GdiEndDocEMF** ](https://msdn.microsoft.com/library/windows/hardware/ff549463)必须是已播放的最后一个的 EMF 记录后调用。

-   为要打印每个物理页[ **GdiStartPageEMF** ](https://msdn.microsoft.com/library/windows/hardware/ff549543)页上，绘制任何文档页之前，必须调用并[ **GdiEndPageEMF** ](https://msdn.microsoft.com/library/windows/hardware/ff549468)必须在调用之后物理页上绘制完最后一个文档页。

-   对于每个文档页后，可以在物理页上，绘制[ **GdiGetDevmodeForPage** ](https://msdn.microsoft.com/library/windows/hardware/ff549478)必须调用以确定是否已更改的 DEVMODE 结构内容，因为绘制的最后一文档页。 如果 DEVMODE 已更改，必须启动新的物理页 (通过调用[ **GdiEndPageEMF** ](https://msdn.microsoft.com/library/windows/hardware/ff549468)并[ **GdiStartPageEMF**](https://msdn.microsoft.com/library/windows/hardware/ff549543))，并必须通过调用更新打印机的设备上下文[ **GdiResetDCEMF**](https://msdn.microsoft.com/library/windows/hardware/ff549529)。 物理页上通过首先调用绘制文档页面[ **GdiGetPageHandle** ](https://msdn.microsoft.com/library/windows/hardware/ff549505)以获取文档页句柄，并调用[ **GdiPlayPageEMF**](https://msdn.microsoft.com/library/windows/hardware/ff549524)绘制页面。

打印处理器完全绘制作业之后，必须调用[ **GdiDeleteSpoolFileHandle**](https://msdn.microsoft.com/library/windows/hardware/ff549449)。

如果打印处理器需要的总页计数，才能开始打印页面 （例如按相反的顺序打印页面） 它可以调用[ **GdiGetPageCount**](https://msdn.microsoft.com/library/windows/hardware/ff549492)，但此函数不会返回之前后台处理结束，并因此禁用打印后台处理时的功能。

如果打印处理器将使用这些 GDI 函数，其[ **EnumPrintProcessorDatatypes** ](https://msdn.microsoft.com/library/windows/hardware/ff548757)函数必须返回表示泛型 Windows 2000 和更高版本的 EMF 格式受支持的数据类型为"NT EMF"。 打印处理器不能修改 EMF 记录。

 

 





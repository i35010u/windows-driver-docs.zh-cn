---
title: 打印机图形 DLL 定义的函数
description: 打印机图形 DLL 定义的函数
ms.assetid: b0c9ce45-76c4-4058-af3f-7b9d230bcf94
keywords:
- 打印机图形 DLL WDK，函数
- 函数 WDK 打印机图形 DLL
- 图形 DLL WDK 打印机，函数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f268696c4a06f4ec36e04f9da6416e5ef4de5bff
ms.sourcegitcommit: 17c1bbc5ea0bef3bbc87794b030a073f905dc942
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88802763"
---
# <a name="functions-defined-by-printer-graphics-dlls"></a>打印机图形 DLL 定义的函数





与所有图形驱动程序一样，打印机图形 Dll 负责定义以下图形 DDI 函数。 按照 [**DrvEnableDriver**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvenabledriver)，初始驱动程序入口点，其余函数按字母顺序列出。 请注意，因为 GDI 按名称调用 **DrvEnableDriver** ，所以其名称以粗体显示。 GDI 通过 **DrvEnableDriver** 返回的函数指针数组调用所有其他显示驱动程序函数。

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
<td><p><a href="https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvenabledriver" data-raw-source="[&lt;strong&gt;DrvEnableDriver&lt;/strong&gt;](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvenabledriver)"><strong>DrvEnableDriver</strong></a></p></td>
<td><p>允许驱动程序自行初始化并返回指向支持的图形 DDI 函数的指针。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvcompletepdev" data-raw-source="[&lt;strong&gt;DrvCompletePDEV&lt;/strong&gt;](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvcompletepdev)"><strong>DrvCompletePDEV</strong></a></p></td>
<td><p>向设备实例提供具有 GDI 句柄的驱动程序。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvdisabledriver" data-raw-source="[&lt;strong&gt;DrvDisableDriver&lt;/strong&gt;](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvdisabledriver)"><strong>DrvDisableDriver</strong></a></p></td>
<td><p> (可选的) 允许驱动程序在卸载之前执行清理操作。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvdisablepdev" data-raw-source="[&lt;strong&gt;DrvDisablePDEV&lt;/strong&gt;](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvdisablepdev)"><strong>DrvDisablePDEV</strong></a></p></td>
<td><p>允许驱动程序删除特定于设备实例的信息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvdisablesurface" data-raw-source="[&lt;strong&gt;DrvDisableSurface&lt;/strong&gt;](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvdisablesurface)"><strong>DrvDisableSurface</strong></a></p></td>
<td><p>允许驱动程序删除绘图图面。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvenablepdev" data-raw-source="[&lt;strong&gt;DrvEnablePDEV&lt;/strong&gt;](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvenablepdev)"><strong>DrvEnablePDEV</strong></a></p></td>
<td><p>允许驱动程序提供具有物理设备特征的 GDI，并初始化特定于设备实例的信息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvenablesurface" data-raw-source="[&lt;strong&gt;DrvEnableSurface&lt;/strong&gt;](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvenablesurface)"><strong>DrvEnableSurface</strong></a></p></td>
<td><p>允许驱动程序创建绘图图面。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvquerydevicesupport" data-raw-source="[&lt;strong&gt;DrvQueryDeviceSupport&lt;/strong&gt;](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvquerydevicesupport)"><strong>DrvQueryDeviceSupport</strong></a></p></td>
<td><p> (可选) 返回请求的特定于设备的信息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvquerydriverinfo" data-raw-source="[&lt;strong&gt;DrvQueryDriverInfo&lt;/strong&gt;](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvquerydriverinfo)"><strong>DrvQueryDriverInfo</strong></a></p></td>
<td><p> (可选) 返回请求的特定于驱动程序的信息。</p></td>
</tr>
</tbody>
</table>

 

打印机图形 Dll 还负责定义下列打印特定图形 DDI 函数，这些函数在呈现打印作业的过程中的特定点调用。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>函数</th>
<th>调用时</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvenddoc" data-raw-source="[&lt;strong&gt;DrvEndDoc&lt;/strong&gt;](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvenddoc)"><strong>DrvEndDoc</strong></a></p></td>
<td><p>当 GDI 完成将文档发送到要呈现的驱动程序时。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvnextband" data-raw-source="[&lt;strong&gt;DrvNextBand&lt;/strong&gt;](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvnextband)"><strong>DrvNextBand</strong></a></p></td>
<td><p>当 GDI 完成为物理页面绘制带区时， (可选) ，以便驱动程序可以将带区发送到打印机。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvqueryperbandinfo" data-raw-source="[&lt;em&gt;DrvQueryPerBandInfo&lt;/em&gt;](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvqueryperbandinfo)"><em>DrvQueryPerBandInfo</em></a></p></td>
<td><p>在 GDI 开始为物理页面绘制带区之前， (可选) ，因此驱动程序可以向 GDI 提供特定于波段的信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvsendpage" data-raw-source="[&lt;em&gt;DrvSendPage&lt;/em&gt;](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvsendpage)"><em>DrvSendPage</em></a></p></td>
<td><p>当 GDI 完成了物理页的绘制时，因此驱动程序可以将页发送到打印机。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvstartbanding" data-raw-source="[&lt;strong&gt;DrvStartBanding&lt;/strong&gt;](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvstartbanding)"><strong>DrvStartBanding</strong></a></p></td>
<td><p>当 GDI 准备好开始向要呈现的驱动程序中发送物理页面带区时， (可选) 。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvstartdoc" data-raw-source="[&lt;strong&gt;DrvStartDoc&lt;/strong&gt;](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvstartdoc)"><strong>DrvStartDoc</strong></a></p></td>
<td><p>当 GDI 准备好开始向驱动程序发送文档以供呈现时使用。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvstartpage" data-raw-source="[&lt;strong&gt;DrvStartPage&lt;/strong&gt;](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvstartpage)"><strong>DrvStartPage</strong></a></p></td>
<td><p>当 GDI 准备好开始向要呈现的驱动程序发送文档页面时。</p></td>
</tr>
</tbody>
</table>

 

通常，打印机图形 DLL 还会定义完成打印作业呈现所需的任何其他图形 DDI 函数。 定义的函数的数量和类型取决于：

-   驱动程序是否支持使用 GDI 托管或设备托管的绘图图面的 (或二者) 。 有关详细信息，请参阅 [表面类型](https://docs.microsoft.com/windows-hardware/drivers/display/surface-types)。

-   GDI 操作可由 GDI 处理的范围，而不是由驱动程序本身来执行。 有关详细信息，请参阅 [使用图形 DDI](https://docs.microsoft.com/windows-hardware/drivers/display/using-the-graphics-ddi)。

打印机图形 Dll 定义的所有函数都是通过 GDI 的内核模式图形呈现引擎（ (GRE) ）调用的。

[**DrvEnableDriver**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvenabledriver)和[**DrvQueryDriverInfo**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvquerydriverinfo)函数由图形 DLL 导出。 所有其他受支持的图形 DDI 函数的地址都放置在 **DrvEnableDriver** 函数返回的表中。

 

 





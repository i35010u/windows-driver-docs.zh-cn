---
title: 打印机图形 DLL 定义的函数
description: 打印机图形 DLL 定义的函数
ms.assetid: b0c9ce45-76c4-4058-af3f-7b9d230bcf94
keywords:
- 打印机图形 DLL WDK，函数
- WDK 打印机图形 DLL 函数
- 图形 DLL WDK 打印机，函数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 868eb414a0b48802aa0bce31d7ede17fdec3087f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364018"
---
# <a name="functions-defined-by-printer-graphics-dlls"></a>打印机图形 DLL 定义的函数





所有图形驱动程序，如打印机图形 Dll 负责定义以下图形 DDI 函数。 遵循[ **DrvEnableDriver**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenabledriver)，初始驱动程序入口点，其余函数按字母顺序列出。 请注意，由于调用 GDI **DrvEnableDriver**按名称，其名称将显示为粗体。 GDI 调用通过函数指针的数组的所有其他显示器驱动程序函数**DrvEnableDriver**返回。

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
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenabledriver" data-raw-source="[&lt;strong&gt;DrvEnableDriver&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenabledriver)"><strong>DrvEnableDriver</strong></a></p></td>
<td><p>使驱动程序初始化自身并返回到受支持的图形 DDI 函数的指针。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvcompletepdev" data-raw-source="[&lt;strong&gt;DrvCompletePDEV&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvcompletepdev)"><strong>DrvCompletePDEV</strong></a></p></td>
<td><p>该驱动程序提供的 GDI 句柄的设备实例。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisabledriver" data-raw-source="[&lt;strong&gt;DrvDisableDriver&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisabledriver)"><strong>DrvDisableDriver</strong></a></p></td>
<td><p>（可选）使驱动程序在卸载之前执行清理操作。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisablepdev" data-raw-source="[&lt;strong&gt;DrvDisablePDEV&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisablepdev)"><strong>DrvDisablePDEV</strong></a></p></td>
<td><p>使驱动程序删除设备特定于实例的信息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisablesurface" data-raw-source="[&lt;strong&gt;DrvDisableSurface&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisablesurface)"><strong>DrvDisableSurface</strong></a></p></td>
<td><p>使驱动程序删除绘图图面。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablepdev" data-raw-source="[&lt;strong&gt;DrvEnablePDEV&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablepdev)"><strong>DrvEnablePDEV</strong></a></p></td>
<td><p>使驱动程序与物理设备特性提供 GDI 并初始化设备特定于实例的信息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablesurface" data-raw-source="[&lt;strong&gt;DrvEnableSurface&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablesurface)"><strong>DrvEnableSurface</strong></a></p></td>
<td><p>使驱动程序来创建绘图图面。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvquerydevicesupport" data-raw-source="[&lt;strong&gt;DrvQueryDeviceSupport&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvquerydevicesupport)"><strong>DrvQueryDeviceSupport</strong></a></p></td>
<td><p>（可选）返回请求的特定于设备的信息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvquerydriverinfo" data-raw-source="[&lt;strong&gt;DrvQueryDriverInfo&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvquerydriverinfo)"><strong>DrvQueryDriverInfo</strong></a></p></td>
<td><p>（可选）返回请求的特定于驱动程序的信息。</p></td>
</tr>
</tbody>
</table>

 

打印机图形 Dll 也要负责定义以下特定于打印的图形 DDI 函数，在打印作业的呈现期间调用的特定点上。

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
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenddoc" data-raw-source="[&lt;strong&gt;DrvEndDoc&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenddoc)"><strong>DrvEndDoc</strong></a></p></td>
<td><p>GDI 结束时将文档发送到呈现的驱动程序。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvnextband" data-raw-source="[&lt;strong&gt;DrvNextBand&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvnextband)"><strong>DrvNextBand</strong></a></p></td>
<td><p>（可选）GDI 结束时绘制一个物理页的带，因此驱动程序可以向外发送到打印机。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvqueryperbandinfo" data-raw-source="[&lt;em&gt;DrvQueryPerBandInfo&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvqueryperbandinfo)"><em>DrvQueryPerBandInfo</em></a></p></td>
<td><p>（可选）GDI 开始绘制带区的物理页之前，因此驱动程序能够为 GDI 提供特定于外的信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsendpage" data-raw-source="[&lt;em&gt;DrvSendPage&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsendpage)"><em>DrvSendPage</em></a></p></td>
<td><p>GDI 结束时绘制一个物理页，因此驱动程序可以将页发送到打印机。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstartbanding" data-raw-source="[&lt;strong&gt;DrvStartBanding&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstartbanding)"><strong>DrvStartBanding</strong></a></p></td>
<td><p>（可选）当 GDI 已准备好开始将物理页的带区发送到呈现的驱动程序。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstartdoc" data-raw-source="[&lt;strong&gt;DrvStartDoc&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstartdoc)"><strong>DrvStartDoc</strong></a></p></td>
<td><p>当 GDI 已准备好开始将文档发送到呈现的驱动程序。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstartpage" data-raw-source="[&lt;strong&gt;DrvStartPage&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstartpage)"><strong>DrvStartPage</strong></a></p></td>
<td><p>当 GDI 已准备好开始向呈现的驱动程序发送的文档页。</p></td>
</tr>
</tbody>
</table>

 

通常情况下，打印机图形 DLL 还定义了任何其他图形 DDI 函数所需完成打印作业呈现。 数量和类型定义的函数取决于：

-   是否驱动程序支持使用 GDI 管理或由设备管理的绘图图面 （或两者）。 有关详细信息，请参阅[图面类型](https://docs.microsoft.com/windows-hardware/drivers/display/surface-types)。

-   向其绘制操作可以处理通过 GDI 而不是执行驱动程序本身的范围。 有关详细信息，请参阅[使用图形 DDI](https://docs.microsoft.com/windows-hardware/drivers/display/using-the-graphics-ddi)。

所有函数定义的打印机图形 GDI 的内核模式图形呈现引擎 (GRE) 都调用的 Dll。

[ **DrvEnableDriver** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenabledriver)并[ **DrvQueryDriverInfo** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvquerydriverinfo)通过图形 DLL 导出函数。 所有其他受支持的图形 DDI 函数的地址返回的表中放置**DrvEnableDriver**函数。

 

 





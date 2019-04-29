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
ms.openlocfilehash: b4811b065aa86d603bf9f649cb69222bc5a4bcd3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363346"
---
# <a name="functions-defined-by-printer-graphics-dlls"></a>打印机图形 DLL 定义的函数





所有图形驱动程序，如打印机图形 Dll 负责定义以下图形 DDI 函数。 遵循[ **DrvEnableDriver**](https://msdn.microsoft.com/library/windows/hardware/ff556210)，初始驱动程序入口点，其余函数按字母顺序列出。 请注意，由于调用 GDI **DrvEnableDriver**按名称，其名称将显示为粗体。 GDI 调用通过函数指针的数组的所有其他显示器驱动程序函数**DrvEnableDriver**返回。

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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556210" data-raw-source="[&lt;strong&gt;DrvEnableDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556210)"><strong>DrvEnableDriver</strong></a></p></td>
<td><p>使驱动程序初始化自身并返回到受支持的图形 DDI 函数的指针。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556181" data-raw-source="[&lt;strong&gt;DrvCompletePDEV&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556181)"><strong>DrvCompletePDEV</strong></a></p></td>
<td><p>该驱动程序提供的 GDI 句柄的设备实例。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556196" data-raw-source="[&lt;strong&gt;DrvDisableDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556196)"><strong>DrvDisableDriver</strong></a></p></td>
<td><p>（可选）使驱动程序在卸载之前执行清理操作。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556198" data-raw-source="[&lt;strong&gt;DrvDisablePDEV&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556198)"><strong>DrvDisablePDEV</strong></a></p></td>
<td><p>使驱动程序删除设备特定于实例的信息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556200" data-raw-source="[&lt;strong&gt;DrvDisableSurface&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556200)"><strong>DrvDisableSurface</strong></a></p></td>
<td><p>使驱动程序删除绘图图面。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556211" data-raw-source="[&lt;strong&gt;DrvEnablePDEV&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556211)"><strong>DrvEnablePDEV</strong></a></p></td>
<td><p>使驱动程序与物理设备特性提供 GDI 并初始化设备特定于实例的信息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556214" data-raw-source="[&lt;strong&gt;DrvEnableSurface&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556214)"><strong>DrvEnableSurface</strong></a></p></td>
<td><p>使驱动程序来创建绘图图面。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556260" data-raw-source="[&lt;strong&gt;DrvQueryDeviceSupport&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556260)"><strong>DrvQueryDeviceSupport</strong></a></p></td>
<td><p>（可选）返回请求的特定于设备的信息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556261" data-raw-source="[&lt;strong&gt;DrvQueryDriverInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556261)"><strong>DrvQueryDriverInfo</strong></a></p></td>
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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556215" data-raw-source="[&lt;strong&gt;DrvEndDoc&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556215)"><strong>DrvEndDoc</strong></a></p></td>
<td><p>GDI 结束时将文档发送到呈现的驱动程序。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556250" data-raw-source="[&lt;strong&gt;DrvNextBand&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556250)"><strong>DrvNextBand</strong></a></p></td>
<td><p>（可选）GDI 结束时绘制一个物理页的带，因此驱动程序可以向外发送到打印机。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556268" data-raw-source="[&lt;em&gt;DrvQueryPerBandInfo&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556268)"><em>DrvQueryPerBandInfo</em></a></p></td>
<td><p>（可选）GDI 开始绘制带区的物理页之前，因此驱动程序能够为 GDI 提供特定于外的信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556281" data-raw-source="[&lt;em&gt;DrvSendPage&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556281)"><em>DrvSendPage</em></a></p></td>
<td><p>GDI 结束时绘制一个物理页，因此驱动程序可以将页发送到打印机。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556292" data-raw-source="[&lt;strong&gt;DrvStartBanding&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556292)"><strong>DrvStartBanding</strong></a></p></td>
<td><p>（可选）当 GDI 已准备好开始将物理页的带区发送到呈现的驱动程序。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556296" data-raw-source="[&lt;strong&gt;DrvStartDoc&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556296)"><strong>DrvStartDoc</strong></a></p></td>
<td><p>当 GDI 已准备好开始将文档发送到呈现的驱动程序。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556298" data-raw-source="[&lt;strong&gt;DrvStartPage&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556298)"><strong>DrvStartPage</strong></a></p></td>
<td><p>当 GDI 已准备好开始向呈现的驱动程序发送的文档页。</p></td>
</tr>
</tbody>
</table>

 

通常情况下，打印机图形 DLL 还定义了任何其他图形 DDI 函数所需完成打印作业呈现。 数量和类型定义的函数取决于：

-   是否驱动程序支持使用 GDI 管理或由设备管理的绘图图面 （或两者）。 有关详细信息，请参阅[图面类型](https://msdn.microsoft.com/library/windows/hardware/ff569900)。

-   向其绘制操作可以处理通过 GDI 而不是执行驱动程序本身的范围。 有关详细信息，请参阅[使用图形 DDI](https://msdn.microsoft.com/library/windows/hardware/ff570139)。

所有函数定义的打印机图形 GDI 的内核模式图形呈现引擎 (GRE) 都调用的 Dll。

[ **DrvEnableDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff556210)并[ **DrvQueryDriverInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff556261)通过图形 DLL 导出函数。 所有其他受支持的图形 DDI 函数的地址返回的表中放置**DrvEnableDriver**函数。

 

 





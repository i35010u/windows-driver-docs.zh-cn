---
title: 按打印机接口 DLL 定义的函数
description: 按打印机接口 DLL 定义的函数
ms.assetid: 8b0ae796-67cf-4619-a0a7-6cb6aab8c2e4
keywords:
- 打印机接口 DLL WDK，函数
- 功能 WDK 打印机接口 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ee41cfa13dd961d3b93496fb70702e2cc64466c
ms.sourcegitcommit: 17c1bbc5ea0bef3bbc87794b030a073f905dc942
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88802761"
---
# <a name="functions-defined-by-printer-interface-dlls"></a>按打印机接口 DLL 定义的函数





打印机接口 Dll 导出下表中列出的函数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>函数</th>
<th>用途</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>DllEntryPoint</strong></p></td>
<td><p>初始 DLL 入口点通常称为 DLLMain (Microsoft Windows SDK 文档) 中所述。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvconvertdevmode" data-raw-source="[&lt;strong&gt;DrvConvertDevMode&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvconvertdevmode)"><strong>DrvConvertDevMode</strong></a></p></td>
<td><p>将指定的 <a href="https://docs.microsoft.com/windows/win32/api/wingdi/ns-wingdi-devmodew" data-raw-source="[&lt;strong&gt;DEVMODEW&lt;/strong&gt;](https://docs.microsoft.com/windows/win32/api/wingdi/ns-wingdi-devmodew)"><strong>DEVMODEW</strong></a> 结构从一个版本转换到另一个版本。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdevicecapabilities" data-raw-source="[&lt;strong&gt;DrvDeviceCapabilities&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdevicecapabilities)"><strong>DrvDeviceCapabilities</strong></a></p></td>
<td><p>返回有关打印机功能的请求信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdevicepropertysheets" data-raw-source="[&lt;strong&gt;DrvDevicePropertySheets&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdevicepropertysheets)"><strong>DrvDevicePropertySheets</strong></a></p></td>
<td><p>调用 <a href="common-property-sheet-user-interface.md" data-raw-source="[CPSUI](common-property-sheet-user-interface.md)">CPSUI</a> 创建描述打印机属性的属性表页。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdocumentevent" data-raw-source="[&lt;strong&gt;DrvDocumentEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdocumentevent)"><strong>DrvDocumentEvent</strong></a></p></td>
<td><p> (可选) 允许打印机接口 DLL 指定与打印文档将处理的文档相关联的事件。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdriverevent" data-raw-source="[&lt;strong&gt;DrvDriverEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdriverevent)"><strong>DrvDriverEvent</strong></a></p></td>
<td><p> (可选) 允许打印机接口 DLL 响应来自特定于特定驱动程序事件的后台处理程序的通知。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdocumentpropertysheets" data-raw-source="[&lt;strong&gt;DrvDocumentPropertySheets&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdocumentpropertysheets)"><strong>DrvDocumentPropertySheets</strong></a></p></td>
<td><p>调用 CPSUI 创建描述打印文档属性的属性表页。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvprinterevent" data-raw-source="[&lt;strong&gt;DrvPrinterEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvprinterevent)"><strong>DrvPrinterEvent</strong></a></p></td>
<td><p>允许打印机接口 DLL 响应来自特定于打印机的事件已发生的后台处理程序的通知。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvquerycolorprofile" data-raw-source="[&lt;strong&gt;DrvQueryColorProfile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvquerycolorprofile)"><strong>DrvQueryColorProfile</strong></a></p></td>
<td><p> (可选) 允许打印机接口 DLL 指定用于颜色管理的 ICC 配置文件。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvqueryjobattributes" data-raw-source="[&lt;strong&gt;DrvQueryJobAttributes&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvqueryjobattributes)"><strong>DrvQueryJobAttributes</strong></a></p></td>
<td><p> (可选) 使打印机接口 DLL 能够指定支持在物理页面上打印多个文档页面的功能， ( "N 向上" 打印) ，打印每个页面的多个副本，以及对页面进行分页。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-devqueryprintex" data-raw-source="[&lt;strong&gt;DevQueryPrintEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-devqueryprintex)"><strong>DevQueryPrintEx</strong></a></p></td>
<td><p>确定是否可以使用打印机的当前配置打印打印作业。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvspldevicecaps" data-raw-source="[&lt;strong&gt;DrvSplDeviceCaps&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvspldevicecaps)"><strong>DrvSplDeviceCaps</strong></a></p></td>
<td><p>返回有关打印机功能的请求信息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvupgradeprinter" data-raw-source="[&lt;strong&gt;DrvUpgradePrinter&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvupgradeprinter)"><strong>DrvUpgradePrinter</strong></a></p></td>
<td><p> (可选) 在将新版本的驱动程序添加到系统时更新打印机的注册表设置。</p></td>
</tr>
</tbody>
</table>

 

 

 





---
title: 按打印机接口 DLL 定义的函数
description: 按打印机接口 DLL 定义的函数
ms.assetid: 8b0ae796-67cf-4619-a0a7-6cb6aab8c2e4
keywords:
- 打印机接口 DLL WDK，函数
- 函数 WDK 打印机接口 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9daf71e6c2529c1eecc6a3b0fc6c7b193155ab98
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363207"
---
# <a name="functions-defined-by-printer-interface-dlls"></a>按打印机接口 DLL 定义的函数





打印机接口 Dll 将导出下表中列出的函数。

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
<td><p>初始 DLL 入口点，通常称为 DLLMain （Microsoft Windows SDK 文档中所述）。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548532" data-raw-source="[&lt;strong&gt;DrvConvertDevMode&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548532)"><strong>DrvConvertDevMode</strong></a></p></td>
<td><p>将指定<a href="https://msdn.microsoft.com/library/windows/hardware/ff552837" data-raw-source="[&lt;strong&gt;DEVMODEW&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552837)"> <strong>DEVMODEW</strong> </a>结构从一个版本到另一个。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548539" data-raw-source="[&lt;strong&gt;DrvDeviceCapabilities&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548539)"><strong>DrvDeviceCapabilities</strong></a></p></td>
<td><p>返回请求的有关打印机的功能的信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548542" data-raw-source="[&lt;strong&gt;DrvDevicePropertySheets&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548542)"><strong>DrvDevicePropertySheets</strong></a></p></td>
<td><p>调用<a href="common-property-sheet-user-interface.md" data-raw-source="[CPSUI](common-property-sheet-user-interface.md)">CPSUI</a>创建描述打印机的属性的属性表页。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548544" data-raw-source="[&lt;strong&gt;DrvDocumentEvent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548544)"><strong>DrvDocumentEvent</strong></a></p></td>
<td><p>（可选）允许打印机接口 DLL 以指定将处理与打印文档相关联的事件。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548551" data-raw-source="[&lt;strong&gt;DrvDriverEvent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548551)"><strong>DrvDriverEvent</strong></a></p></td>
<td><p>（可选）允许打印机接口 DLL 以响应来自特定驱动程序特定事件已发生后台处理程序的通知。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548548" data-raw-source="[&lt;strong&gt;DrvDocumentPropertySheets&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548548)"><strong>DrvDocumentPropertySheets</strong></a></p></td>
<td><p>调用 CPSUI 创建描述打印文档的属性的属性表页。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548564" data-raw-source="[&lt;strong&gt;DrvPrinterEvent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548564)"><strong>DrvPrinterEvent</strong></a></p></td>
<td><p>允许打印机接口 DLL 以响应来自某些特定于打印机的事件发生的后台处理程序的通知。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548573" data-raw-source="[&lt;strong&gt;DrvQueryColorProfile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548573)"><strong>DrvQueryColorProfile</strong></a></p></td>
<td><p>（可选）允许打印机接口来指定要使用的颜色管理的 ICC 配置文件的 DLL。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548581" data-raw-source="[&lt;strong&gt;DrvQueryJobAttributes&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548581)"><strong>DrvQueryJobAttributes</strong></a></p></td>
<td><p>（可选）允许打印机接口 DLL 指定为物理页 （"每张"打印） 上打印多个文档页面对此类功能的支持、 打印的每个页上，多个副本和对页进行排序。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff547576" data-raw-source="[&lt;strong&gt;DevQueryPrintEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547576)"><strong>DevQueryPrintEx</strong></a></p></td>
<td><p>确定是否可以使用打印机的当前配置显示打印作业。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548600" data-raw-source="[&lt;strong&gt;DrvSplDeviceCaps&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548600)"><strong>DrvSplDeviceCaps</strong></a></p></td>
<td><p>返回请求的有关打印机的功能的信息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548648" data-raw-source="[&lt;strong&gt;DrvUpgradePrinter&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548648)"><strong>DrvUpgradePrinter</strong></a></p></td>
<td><p>（可选）新版本的驱动程序添加到系统时，请更新打印机的注册表设置。</p></td>
</tr>
</tbody>
</table>

 

 

 





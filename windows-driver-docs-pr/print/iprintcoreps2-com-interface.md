---
title: IPrintCorePS2 COM 接口
description: IPrintCorePS2 COM 接口
ms.assetid: d5eb6962-2201-405f-9a22-2b11fb6d0360
keywords:
- IPrintCorePS2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ffdaddd7512087c532e2b98568144fd8325bdc3
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57348912"
---
# <a name="iprintcoreps2-com-interface"></a>IPrintCorePS2 COM 接口





`IPrintCorePS2` Pscript5 呈现插件 COM 接口提供一组帮助程序方法。下表列出并描述所有定义的方法`IPrintCorePS2`接口。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>方法</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552978" data-raw-source="[&lt;strong&gt;IPrintCorePS2::DrvWriteSpoolBuf&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552978)"><strong>IPrintCorePS2::DrvWriteSpoolBuf</strong></a></p></td>
<td><p>Pscript5 驱动程序提供，以便<a href="rendering-plug-ins.md" data-raw-source="[rendering plug-ins](rendering-plug-ins.md)">呈现插件</a>可以将打印机数据发送到后台处理程序。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552990" data-raw-source="[&lt;strong&gt;IPrintCorePS2::EnumFeatures&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552990)"><strong>IPrintCorePS2::EnumFeatures</strong></a></p></td>
<td><p>枚举打印机的可用功能。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552996" data-raw-source="[&lt;strong&gt;IPrintCorePS2::EnumOptions&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552996)"><strong>IPrintCorePS2::EnumOptions</strong></a></p></td>
<td><p>枚举特定功能的可用选项。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553006" data-raw-source="[&lt;strong&gt;IPrintCorePS2::GetFeatureAttribute&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553006)"><strong>IPrintCorePS2::GetFeatureAttribute</strong></a></p></td>
<td><p>检索功能特性列表或特定的功能属性的值。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553009" data-raw-source="[&lt;strong&gt;IPrintCorePS2::GetGlobalAttribute&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553009)"><strong>IPrintCorePS2::GetGlobalAttribute</strong></a></p></td>
<td><p>检索的全局属性列表或特定的全局属性的值。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553013" data-raw-source="[&lt;strong&gt;IPrintCorePS2::GetOptionAttribute&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553013)"><strong>IPrintCorePS2::GetOptionAttribute</strong></a></p></td>
<td><p>检索选项属性列表或特定的选项属性的值。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553019" data-raw-source="[&lt;strong&gt;IPrintCorePS2::GetOptions&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553019)"><strong>IPrintCorePS2::GetOptions</strong></a></p></td>
<td><p>检索驱动程序的当前功能设置中的功能/选项关键字对列表的格式。</p></td>
</tr>
</tbody>
</table>

 

有关详细信息，请参阅[实现打印机驱动程序 COM 接口](implementing-printer-driver-com-interfaces.md)。

 

 





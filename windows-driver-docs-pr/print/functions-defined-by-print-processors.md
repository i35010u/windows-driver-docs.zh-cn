---
title: 打印处理器所定义的函数
description: 打印处理器所定义的函数
ms.assetid: ada376f0-515e-4995-b612-4da9523b6fcf
keywords:
- 打印处理器 WDK，函数
- 函数 WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17c27218af95da7714b9e9d99ce18ab0a97d3f13
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526021"
---
# <a name="functions-defined-by-print-processors"></a>打印处理器所定义的函数





打印处理器必须将导出下表中列出的函数。

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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff545976" data-raw-source="[&lt;strong&gt;ClosePrintProcessor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545976)"><strong>ClosePrintProcessor</strong></a></p></td>
<td><p>关闭打印处理器。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546352" data-raw-source="[&lt;strong&gt;ControlPrintProcessor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546352)"><strong>ControlPrintProcessor</strong></a></p></td>
<td><p>提供对打印文档的控制。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548757" data-raw-source="[&lt;strong&gt;EnumPrintProcessorDatatypes&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548757)"><strong>EnumPrintProcessorDatatypes</strong></a></p></td>
<td><p>枚举打印处理器支持的数据类型。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550522" data-raw-source="[&lt;strong&gt;GetPrintProcessorCapabilities&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550522)"><strong>GetPrintProcessorCapabilities</strong></a></p></td>
<td><p>返回打印指定的输入的数据类型的处理器功能。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559604" data-raw-source="[&lt;strong&gt;OpenPrintProcessor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559604)"><strong>OpenPrintProcessor</strong></a></p></td>
<td><p>此时会打开用于打印的打印处理器。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff560724" data-raw-source="[&lt;strong&gt;PrintDocumentOnPrintProcessor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560724)"><strong>PrintDocumentOnPrintProcessor</strong></a></p></td>
<td><p>打印处理器上打印文档。</p></td>
</tr>
</tbody>
</table>

 

 

 





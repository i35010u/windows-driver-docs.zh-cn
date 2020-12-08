---
title: 打印处理器定义的函数
description: 打印处理器定义的函数
keywords:
- 打印处理器 WDK，函数
- 函数 WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2e9c2c70b4315a4c5e40365d6d1b9c27537ff9d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797065"
---
# <a name="functions-defined-by-print-processors"></a>打印处理器定义的函数





打印处理器必须导出下表中列出的函数。

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
<td><p><a href="/windows-hardware/drivers/ddi/winsplp/nf-winsplp-closeprintprocessor" data-raw-source="[&lt;strong&gt;ClosePrintProcessor&lt;/strong&gt;](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-closeprintprocessor)"><strong>ClosePrintProcessor</strong></a></p></td>
<td><p>关闭打印处理器。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/winsplp/nf-winsplp-controlprintprocessor" data-raw-source="[&lt;strong&gt;ControlPrintProcessor&lt;/strong&gt;](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-controlprintprocessor)"><strong>ControlPrintProcessor</strong></a></p></td>
<td><p>提供对打印文档的控制。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/winspool/nf-winspool-enumprintprocessordatatypesa" data-raw-source="[&lt;strong&gt;EnumPrintProcessorDatatypes&lt;/strong&gt;](/windows-hardware/drivers/ddi/winspool/nf-winspool-enumprintprocessordatatypesa)"><strong>EnumPrintProcessorDatatypes</strong></a></p></td>
<td><p>枚举打印处理器支持的数据类型。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/winsplp/nf-winsplp-getprintprocessorcapabilities" data-raw-source="[&lt;strong&gt;GetPrintProcessorCapabilities&lt;/strong&gt;](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-getprintprocessorcapabilities)"><strong>GetPrintProcessorCapabilities</strong></a></p></td>
<td><p>返回指定输入数据类型的打印处理器功能。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/winsplp/nf-winsplp-openprintprocessor" data-raw-source="[&lt;strong&gt;OpenPrintProcessor&lt;/strong&gt;](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-openprintprocessor)"><strong>OpenPrintProcessor</strong></a></p></td>
<td><p>打开打印处理器以进行打印。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/winsplp/nf-winsplp-printdocumentonprintprocessor" data-raw-source="[&lt;strong&gt;PrintDocumentOnPrintProcessor&lt;/strong&gt;](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-printdocumentonprintprocessor)"><strong>PrintDocumentOnPrintProcessor</strong></a></p></td>
<td><p>打印打印处理器上的文档。</p></td>
</tr>
</tbody>
</table>

 


---
title: 打印处理器定义的函数
description: 打印处理器定义的函数
ms.assetid: ada376f0-515e-4995-b612-4da9523b6fcf
keywords:
- 打印处理器 WDK，函数
- 函数 WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 36509dbf28a0d85e024a43a22390b9663a91b625
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383155"
---
# <a name="functions-defined-by-print-processors"></a>打印处理器定义的函数





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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-closeprintprocessor" data-raw-source="[&lt;strong&gt;ClosePrintProcessor&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-closeprintprocessor)"><strong>ClosePrintProcessor</strong></a></p></td>
<td><p>关闭打印处理器。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-controlprintprocessor" data-raw-source="[&lt;strong&gt;ControlPrintProcessor&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-controlprintprocessor)"><strong>ControlPrintProcessor</strong></a></p></td>
<td><p>提供对打印文档的控制。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winspool/nf-winspool-enumprintprocessordatatypesa" data-raw-source="[&lt;strong&gt;EnumPrintProcessorDatatypes&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winspool/nf-winspool-enumprintprocessordatatypesa)"><strong>EnumPrintProcessorDatatypes</strong></a></p></td>
<td><p>枚举打印处理器支持的数据类型。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-getprintprocessorcapabilities" data-raw-source="[&lt;strong&gt;GetPrintProcessorCapabilities&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-getprintprocessorcapabilities)"><strong>GetPrintProcessorCapabilities</strong></a></p></td>
<td><p>返回打印指定的输入的数据类型的处理器功能。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-openprintprocessor" data-raw-source="[&lt;strong&gt;OpenPrintProcessor&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-openprintprocessor)"><strong>OpenPrintProcessor</strong></a></p></td>
<td><p>此时会打开用于打印的打印处理器。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-printdocumentonprintprocessor" data-raw-source="[&lt;strong&gt;PrintDocumentOnPrintProcessor&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-printdocumentonprintprocessor)"><strong>PrintDocumentOnPrintProcessor</strong></a></p></td>
<td><p>打印处理器上打印文档。</p></td>
</tr>
</tbody>
</table>

 

 

 





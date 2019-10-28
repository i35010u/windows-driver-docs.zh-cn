---
title: 打印处理器定义的函数
description: 打印处理器定义的函数
ms.assetid: ada376f0-515e-4995-b612-4da9523b6fcf
keywords:
- 打印处理器 WDK，函数
- 函数 WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 682fb80a93afb9001f65af5c5dd80544fedf5e42
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842405"
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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-closeprintprocessor" data-raw-source="[&lt;strong&gt;ClosePrintProcessor&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-closeprintprocessor)"><strong>ClosePrintProcessor</strong></a></p></td>
<td><p>关闭打印处理器。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-controlprintprocessor" data-raw-source="[&lt;strong&gt;ControlPrintProcessor&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-controlprintprocessor)"><strong>ControlPrintProcessor</strong></a></p></td>
<td><p>提供对打印文档的控制。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winspool/nf-winspool-enumprintprocessordatatypesa" data-raw-source="[&lt;strong&gt;EnumPrintProcessorDatatypes&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winspool/nf-winspool-enumprintprocessordatatypesa)"><strong>EnumPrintProcessorDatatypes</strong></a></p></td>
<td><p>枚举打印处理器支持的数据类型。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-getprintprocessorcapabilities" data-raw-source="[&lt;strong&gt;GetPrintProcessorCapabilities&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-getprintprocessorcapabilities)"><strong>GetPrintProcessorCapabilities</strong></a></p></td>
<td><p>返回指定输入数据类型的打印处理器功能。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-openprintprocessor" data-raw-source="[&lt;strong&gt;OpenPrintProcessor&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-openprintprocessor)"><strong>OpenPrintProcessor</strong></a></p></td>
<td><p>打开打印处理器以进行打印。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-printdocumentonprintprocessor" data-raw-source="[&lt;strong&gt;PrintDocumentOnPrintProcessor&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-printdocumentonprintprocessor)"><strong>PrintDocumentOnPrintProcessor</strong></a></p></td>
<td><p>打印打印处理器上的文档。</p></td>
</tr>
</tbody>
</table>

 

 

 





---
title: IPrintOemUni2 COM 接口
description: IPrintOemUni2 COM 接口
ms.assetid: 7dabc133-a77c-43af-9171-1195fcaf3162
keywords:
- IPrintOemUni2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d54fe049589f5536eb9e9a36087be976cbaffe9
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209553"
---
# <a name="iprintoemuni2-com-interface"></a>IPrintOemUni2 COM 接口





`IPrintOemUni2`Com 接口包含的所有方法，并扩展了[IPrintOemUni COM 接口](iprintoemuni-com-interface.md)的功能。

下表列出并描述了接口提供的所有方法 `IPrintOemUni2` 。 呈现插件必须定义所有列出的方法。 如果方法不是必需的，则可以只返回 E \_ NOTIMPL。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>方法</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni2-writeprinter" data-raw-source="[&lt;strong&gt;IPrintOemUni2::WritePrinter&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni2-writeprinter)"><strong>IPrintOemUni2::WritePrinter</strong></a></p></td>
<td><p>允许插件捕获 Unidrv 驱动程序生成的所有输出数据。</p></td>
</tr>
</tbody>
</table>

 

有关详细信息，请参阅 [实现打印机驱动程序 COM 接口](implementing-printer-driver-com-interfaces.md)。

 


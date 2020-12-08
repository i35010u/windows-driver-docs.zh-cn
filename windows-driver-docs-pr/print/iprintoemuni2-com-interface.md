---
title: IPrintOemUni2 COM 接口
description: IPrintOemUni2 COM 接口
keywords:
- IPrintOemUni2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 82d3cfed68dd78f319a958e7fe8fdee28a2b0c06
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835519"
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
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni2-writeprinter" data-raw-source="[&lt;strong&gt;IPrintOemUni2::WritePrinter&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni2-writeprinter)"><strong>IPrintOemUni2::WritePrinter</strong></a></p></td>
<td><p>允许插件捕获 Unidrv 驱动程序生成的所有输出数据。</p></td>
</tr>
</tbody>
</table>

 

有关详细信息，请参阅 [实现打印机驱动程序 COM 接口](implementing-printer-driver-com-interfaces.md)。


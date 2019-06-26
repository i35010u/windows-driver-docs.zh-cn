---
title: IPrintOemUni2 COM 接口
description: IPrintOemUni2 COM 接口
ms.assetid: 7dabc133-a77c-43af-9171-1195fcaf3162
keywords:
- IPrintOemUni2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 052f9a04ccd610cbc7c9e5f18abf4a149597ba93
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386502"
---
# <a name="iprintoemuni2-com-interface"></a>IPrintOemUni2 COM 接口





`IPrintOemUni2` COM 接口包含的所有方法和扩展的功能[IPrintOemUni COM 接口](iprintoemuni-com-interface.md)。

下表列出并描述所有提供的方法`IPrintOemUni2`接口。 呈现插件必须定义所有列出的方法。 如果不需要一种方法，则可以只返回 E\_NOTIMPL。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuni2-writeprinter" data-raw-source="[&lt;strong&gt;IPrintOemUni2::WritePrinter&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuni2-writeprinter)"><strong>IPrintOemUni2::WritePrinter</strong></a></p></td>
<td><p>允许插件来捕获 Unidrv 驱动程序生成的所有输出数据。</p></td>
</tr>
</tbody>
</table>

 

有关详细信息，请参阅[实现打印机驱动程序 COM 接口](implementing-printer-driver-com-interfaces.md)。

 

 





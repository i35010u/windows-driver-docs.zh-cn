---
title: IPrintOemUni2 COM 接口
description: IPrintOemUni2 COM 接口
ms.assetid: 7dabc133-a77c-43af-9171-1195fcaf3162
keywords:
- IPrintOemUni2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd0e0ca712c93d1795042fa7f19d74ba9212083f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841769"
---
# <a name="iprintoemuni2-com-interface"></a>IPrintOemUni2 COM 接口





`IPrintOemUni2` COM 接口包含的所有方法，并扩展了[IPRINTOEMUNI COM 接口](iprintoemuni-com-interface.md)的功能。

下表列出并描述了 `IPrintOemUni2` 接口提供的所有方法。 呈现插件必须定义所有列出的方法。 如果不需要方法，它可以只返回 E\_NOTIMPL。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni2-writeprinter" data-raw-source="[&lt;strong&gt;IPrintOemUni2::WritePrinter&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni2-writeprinter)"><strong>IPrintOemUni2::WritePrinter</strong></a></p></td>
<td><p>允许插件捕获 Unidrv 驱动程序生成的所有输出数据。</p></td>
</tr>
</tbody>
</table>

 

有关详细信息，请参阅[实现打印机驱动程序 COM 接口](implementing-printer-driver-com-interfaces.md)。

 

 





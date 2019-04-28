---
title: IPrintOemPS2 COM 接口
description: IPrintOemPS2 COM 接口
ms.assetid: 6743d73e-243b-4a05-8e88-576c65b37a19
keywords:
- IPrintOemPS2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 673ff5fe1a0ea45c20fcfdb7a18466971e8ae436
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341328"
---
# <a name="iprintoemps2-com-interface"></a>IPrintOemPS2 COM 接口





`IPrintOemPS2` COM 接口包含的所有方法和扩展的功能[IPrintOemPS COM 接口](iprintoemps-com-interface.md)。 此接口仅限于 Pscript5 呈现的管理单元在 Windows XP 和更高版本的 Windows 操作系统运行。

下表列出并描述所有提供的方法`IPrintOemPS2`接口。 呈现插件必须定义所有列出的方法。 如果不需要一种方法，则可以只返回 E\_NOTIMPL。

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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553189" data-raw-source="[&lt;strong&gt;IPrintOemPS2::GetPDEVAdjustment&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553189)"><strong>IPrintOemPS2::GetPDEVAdjustment</strong></a></p></td>
<td><p>允许插件重写特定 PDEV 设置。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553196" data-raw-source="[&lt;strong&gt;IPrintOemPS2::WritePrinter&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553196)"><strong>IPrintOemPS2::WritePrinter</strong></a></p></td>
<td><p>允许插件来捕获生成的 Postscript 驱动程序的所有输出数据。</p></td>
</tr>
</tbody>
</table>

 

有关详细信息，请参阅[实现打印机驱动程序 COM 接口](implementing-printer-driver-com-interfaces.md)。

 

 





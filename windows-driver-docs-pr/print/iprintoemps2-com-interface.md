---
title: IPrintOemPS2 COM 接口
description: IPrintOemPS2 COM 接口
ms.assetid: 6743d73e-243b-4a05-8e88-576c65b37a19
keywords:
- IPrintOemPS2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd2b08c5878ec785db631ab50860dee9bdd6e3f7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837860"
---
# <a name="iprintoemps2-com-interface"></a>IPrintOemPS2 COM 接口





`IPrintOemPS2` COM 接口包含的所有方法，并扩展了[IPRINTOEMPS COM 接口](iprintoemps-com-interface.md)的功能。 此接口仅限于在 Windows XP 和更高版本的 Windows 操作系统上运行的 Pscript5 呈现插件。

下表列出并描述了 `IPrintOemPS2` 接口提供的所有方法。 呈现插件必须定义所有列出的方法。 如果不需要方法，它可以只返回 E\_NOTIMPL。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps2-getpdevadjustment" data-raw-source="[&lt;strong&gt;IPrintOemPS2::GetPDEVAdjustment&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps2-getpdevadjustment)"><strong>IPrintOemPS2::GetPDEVAdjustment</strong></a></p></td>
<td><p>使插件能够重写特定的 PDEV 设置。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps2-writeprinter" data-raw-source="[&lt;strong&gt;IPrintOemPS2::WritePrinter&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps2-writeprinter)"><strong>IPrintOemPS2::WritePrinter</strong></a></p></td>
<td><p>允许插件捕获由 Postscript 驱动程序生成的所有输出数据。</p></td>
</tr>
</tbody>
</table>

 

有关详细信息，请参阅[实现打印机驱动程序 COM 接口](implementing-printer-driver-com-interfaces.md)。

 

 





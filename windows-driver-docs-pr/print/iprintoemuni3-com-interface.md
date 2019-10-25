---
title: IPrintOemUni3 COM 接口
description: IPrintOemUni3 COM 接口
ms.assetid: 2b3a43fe-52f8-4cb2-993e-d8fcdc878e90
keywords:
- IPrintOemUni3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ccde661bc647be33a0c395cc0d3fa7639909a1a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841765"
---
# <a name="iprintoemuni3-com-interface"></a>IPrintOemUni3 COM 接口





`IPrintOemUni3` COM 接口包含的所有方法，并扩展了[IPRINTOEMUNI Com 接口](iprintoemuni-com-interface.md)和[IPrintOemUni2 com 接口](iprintoemuni2-com-interface.md)的功能。

下表列出并描述了 `IPrintOemUni3` 接口提供的所有方法。 呈现插件必须定义所有列出的方法。 如果不需要方法，它可以只返回 E\_NOTIMPL。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni3-downloadpattern" data-raw-source="[&lt;strong&gt;IPrintOemUni3::DownloadPattern&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni3-downloadpattern)"><strong>IPrintOemUni3：:D ownloadPattern</strong></a></p></td>
<td><p>允许插件将模式下载到打印机。</p></td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni3-getpdevadjustment" data-raw-source="[&lt;strong&gt;IPrintOemUni3::GetPDEVAdjustment&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni3-getpdevadjustment)"><strong>IPrintOemUni3::GetPDEVAdjustment</strong></a></td>
<td><p>使插件能够重写特定的<a href="https://docs.microsoft.com/windows-hardware/drivers/#wdkgloss-pdev" data-raw-source="&lt;em&gt;PDEV&lt;/em&gt;"><em>PDEV</em></a>设置。</p></td>
</tr>
<tr class="odd">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni3-setbandsize" data-raw-source="[&lt;strong&gt;IPrintOemUni3::SetBandSize&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni3-setbandsize)"><strong>IPrintOemUni3::SetBandSize</strong></a></td>
<td><p>允许插件在打印输出中指定所需的带区大小</p></td>
</tr>
</tbody>
</table>

 

有关详细信息，请参阅[实现打印机驱动程序 COM 接口](implementing-printer-driver-com-interfaces.md)。

 

 





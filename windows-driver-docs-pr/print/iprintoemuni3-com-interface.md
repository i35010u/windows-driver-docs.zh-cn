---
title: IPrintOemUni3 COM 接口
description: IPrintOemUni3 COM 接口
ms.assetid: 2b3a43fe-52f8-4cb2-993e-d8fcdc878e90
keywords:
- IPrintOemUni3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0469d43bcd211c56e56f55715b10a93fa1a1b0fc
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89218201"
---
# <a name="iprintoemuni3-com-interface"></a>IPrintOemUni3 COM 接口





`IPrintOemUni3`Com 接口包含的所有方法，并扩展了[IPrintOemUni com 接口](iprintoemuni-com-interface.md)和[IPrintOemUni2 com 接口](iprintoemuni2-com-interface.md)的功能。

下表列出并描述了接口提供的所有方法 `IPrintOemUni3` 。 呈现插件必须定义所有列出的方法。 如果方法不是必需的，则可以只返回 E \_ NOTIMPL。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni3-downloadpattern" data-raw-source="[&lt;strong&gt;IPrintOemUni3::DownloadPattern&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni3-downloadpattern)"><strong>IPrintOemUni3：:D ownloadPattern</strong></a></p></td>
<td><p>允许插件将模式下载到打印机。</p></td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni3-getpdevadjustment" data-raw-source="[&lt;strong&gt;IPrintOemUni3::GetPDEVAdjustment&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni3-getpdevadjustment)"><strong>IPrintOemUni3::GetPDEVAdjustment</strong></a></td>
<td><p>使插件能够重写特定的 <a href="https://docs.microsoft.com/windows-hardware/drivers/#wdkgloss-pdev" data-raw-source="&lt;em&gt;PDEV&lt;/em&gt;"><em>PDEV</em></a> 设置。</p></td>
</tr>
<tr class="odd">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni3-setbandsize" data-raw-source="[&lt;strong&gt;IPrintOemUni3::SetBandSize&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni3-setbandsize)"><strong>IPrintOemUni3::SetBandSize</strong></a></td>
<td><p>允许插件在打印输出中指定所需的带区大小</p></td>
</tr>
</tbody>
</table>

 

有关详细信息，请参阅 [实现打印机驱动程序 COM 接口](implementing-printer-driver-com-interfaces.md)。

 


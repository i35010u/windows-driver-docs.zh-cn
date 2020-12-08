---
title: IPrintOemUni3 COM 接口
description: IPrintOemUni3 COM 接口
keywords:
- IPrintOemUni3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e37c5d0d2ee26e7727666d2f247209f62bb742d3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796535"
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
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni3-downloadpattern" data-raw-source="[&lt;strong&gt;IPrintOemUni3::DownloadPattern&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni3-downloadpattern)"><strong>IPrintOemUni3：:D ownloadPattern</strong></a></p></td>
<td><p>允许插件将模式下载到打印机。</p></td>
</tr>
<tr class="even">
<td><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni3-getpdevadjustment" data-raw-source="[&lt;strong&gt;IPrintOemUni3::GetPDEVAdjustment&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni3-getpdevadjustment)"><strong>IPrintOemUni3::GetPDEVAdjustment</strong></a></td>
<td><p>使插件能够重写特定的 <a href="/windows-hardware/drivers/#wdkgloss-pdev" data-raw-source="&lt;em&gt;PDEV&lt;/em&gt;"><em>PDEV</em></a> 设置。</p></td>
</tr>
<tr class="odd">
<td><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni3-setbandsize" data-raw-source="[&lt;strong&gt;IPrintOemUni3::SetBandSize&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni3-setbandsize)"><strong>IPrintOemUni3::SetBandSize</strong></a></td>
<td><p>允许插件在打印输出中指定所需的带区大小</p></td>
</tr>
</tbody>
</table>

 

有关详细信息，请参阅 [实现打印机驱动程序 COM 接口](implementing-printer-driver-com-interfaces.md)。


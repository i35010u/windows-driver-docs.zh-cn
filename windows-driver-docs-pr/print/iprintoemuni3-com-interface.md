---
title: IPrintOemUni3 COM 接口
description: IPrintOemUni3 COM 接口
ms.assetid: 2b3a43fe-52f8-4cb2-993e-d8fcdc878e90
keywords:
- IPrintOemUni3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e28efbddce1f27e6dd20af41fdd6e1ff5c3ef2b6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384212"
---
# <a name="iprintoemuni3-com-interface"></a>IPrintOemUni3 COM 接口





`IPrintOemUni3` COM 接口包含的所有方法和扩展的功能[IPrintOemUni COM 接口](iprintoemuni-com-interface.md)并且[IPrintOemUni2 COM 接口](iprintoemuni2-com-interface.md)。

下表列出并描述所有提供的方法`IPrintOemUni3`接口。 呈现插件必须定义所有列出的方法。 如果不需要一种方法，则可以只返回 E\_NOTIMPL。

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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554201" data-raw-source="[&lt;strong&gt;IPrintOemUni3::DownloadPattern&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554201)"><strong>IPrintOemUni3::DownloadPattern</strong></a></p></td>
<td><p>允许插件以将其下载到打印机的一种模式。</p></td>
</tr>
<tr class="even">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/ff554205" data-raw-source="[&lt;strong&gt;IPrintOemUni3::GetPDEVAdjustment&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554205)"><strong>IPrintOemUni3::GetPDEVAdjustment</strong></a></td>
<td><p>允许插件以将其重写特定<a href="https://msdn.microsoft.com/library/windows/hardware/ff556325#wdkgloss-pdev" data-raw-source="&lt;em&gt;PDEV&lt;/em&gt;"> <em>PDEV</em> </a>设置。</p></td>
</tr>
<tr class="odd">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/ff554209" data-raw-source="[&lt;strong&gt;IPrintOemUni3::SetBandSize&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554209)"><strong>IPrintOemUni3::SetBandSize</strong></a></td>
<td><p>允许插件以将其指定所需的带区大小上打印输出</p></td>
</tr>
</tbody>
</table>

 

有关详细信息，请参阅[实现打印机驱动程序 COM 接口](implementing-printer-driver-com-interfaces.md)。

 

 





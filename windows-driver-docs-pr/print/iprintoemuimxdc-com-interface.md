---
title: IPrintOemUIMXDC COM 接口
description: IPrintOemUIMXDC COM 接口
ms.assetid: db6d575e-31d0-4a26-8cf9-5188935610e5
keywords:
- IPrintOemUIMXDC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aaa64d9f3fad9475f3aaf639168e6aa0c1933bb2
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90104018"
---
# <a name="iprintoemuimxdc-com-interface"></a>IPrintOemUIMXDC COM 接口


`IPrintOemUIMXDC`利用 COM 接口，XPS 筛选器管道驱动程序可以查看和修改打印机的打印机[接口 DLL](printer-interface-dll.md)所管理的信息。 XPS 驱动程序通过 [Unidrv 或 Pscript 插件](xpsdrv-driver-options.md)访问此 COM 接口。

下表列出并描述了该接口定义的所有方法 `IPrintOemUIMXDC` 。

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
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuimxdc-adjustimageablearea" data-raw-source="[&lt;strong&gt;IPrintOEMUIMXDC::AdjustImageableArea&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuimxdc-adjustimageablearea)"><strong>IPrintOEMUIMXDC::AdjustImageableArea</strong></a></p></td>
<td><p>使 XPS 筛选器管道驱动程序可以使用 UnidrvUI.dll 或 PS5UI.dll 来支持对可打印区域的配置，包括方向和旋转方向。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuimxdc-adjustimagecompression" data-raw-source="[&lt;strong&gt;IPrintOEMUIMXDC::AdjustImageCompression&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuimxdc-adjustimagecompression)"><strong>IPrintOEMUIMXDC::AdjustImageCompression</strong></a></p></td>
<td><p>使 XPS 筛选器管道驱动程序可以使用 UnidrvUI.dll 或 PS5UI.dll 来支持为 JPEG 图像的压缩级别配置。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuimxdc-adjustdpi" data-raw-source="[&lt;strong&gt;IPrintOEMUIMXDC::AdjustDPI&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuimxdc-adjustdpi)"><strong>IPrintOEMUIMXDC::AdjustDPI</strong></a></p></td>
<td><p>使 XPS 筛选器管道驱动程序可以使用 UnidrvUI.dll 或 PS5UI.dll 来支持配置图像解析。</p></td>
</tr>
</tbody>
</table>

 

有关详细信息，请参阅 [实现打印机驱动程序 COM 接口](implementing-printer-driver-com-interfaces.md)。


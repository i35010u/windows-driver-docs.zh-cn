---
title: IPrintOemUIMXDC COM 接口
description: IPrintOemUIMXDC COM 接口
ms.assetid: db6d575e-31d0-4a26-8cf9-5188935610e5
keywords:
- IPrintOemUIMXDC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6eb9ec92512289fa3bd2c05446ce5cb5ac95555d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371749"
---
# <a name="iprintoemuimxdc-com-interface"></a>IPrintOemUIMXDC COM 接口


`IPrintOemUIMXDC` COM 接口，可查看和修改信息的 XPS 筛选器管道驱动程序的[打印机接口 DLL](printer-interface-dll.md)为打印机配置管理。 XPS 驱动程序访问通过此 COM 接口[Unidrv 或 Pscript 插件](xpsdrv-driver-options.md)。

下表列出并描述所有方法`IPrintOemUIMXDC`接口定义。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuimxdc-adjustimageablearea" data-raw-source="[&lt;strong&gt;IPrintOEMUIMXDC::AdjustImageableArea&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuimxdc-adjustimageablearea)"><strong>IPrintOEMUIMXDC::AdjustImageableArea</strong></a></p></td>
<td><p>使 XPS 筛选器管道的驱动程序使用 UnidrvUI.dll 或 PS5UI.dll 来支持配置的可打印区域，包括方向和方向的旋转。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuimxdc-adjustimagecompression" data-raw-source="[&lt;strong&gt;IPrintOEMUIMXDC::AdjustImageCompression&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuimxdc-adjustimagecompression)"><strong>IPrintOEMUIMXDC::AdjustImageCompression</strong></a></p></td>
<td><p>使 XPS 筛选器管道的驱动程序使用 UnidrvUI.dll 或 PS5UI.dll 来支持 JPEG 图像的压缩级别的配置。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuimxdc-adjustdpi" data-raw-source="[&lt;strong&gt;IPrintOEMUIMXDC::AdjustDPI&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuimxdc-adjustdpi)"><strong>IPrintOEMUIMXDC::AdjustDPI</strong></a></p></td>
<td><p>使 XPS 筛选器管道的驱动程序使用 UnidrvUI.dll 或 PS5UI.dll 来支持配置的图像分辨率。</p></td>
</tr>
</tbody>
</table>

 

有关详细信息，请参阅[实现打印机驱动程序 COM 接口](implementing-printer-driver-com-interfaces.md)。

 

 





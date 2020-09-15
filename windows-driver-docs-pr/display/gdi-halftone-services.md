---
title: GDI 半色调服务
description: GDI 半色调服务
ms.assetid: 21112cfc-f7c4-4cce-a9bb-c68d918f5678
keywords:
- GDI WDK Windows 2000 显示，半色调
- 图形驱动程序 WDK Windows 2000 显示，半色调
- 绘制 WDK GDI，半色调
- 半色调 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3594aeaa773a20a5989282499632cbd23e5fe7e
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90107344"
---
# <a name="gdi-halftone-services"></a>GDI 半色调服务


## <span id="ddk_gdi_halftone_services_gg"></span><span id="DDK_GDI_HALFTONE_SERVICES_GG"></span>


GDI 半色调支持包括下表中列出的服务。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">函数</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-ht_computergbgammatable" data-raw-source="[&lt;strong&gt;HT_ComputeRGBGammaTable&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-ht_computergbgammatable)"><strong>HT_ComputeRGBGammaTable</strong></a></p></td>
<td align="left"><p>使 GDI 基于伽玛数字计算设备的红色、绿色和蓝色浓度。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-ht_get8bppformatpalette" data-raw-source="[&lt;strong&gt;HT_Get8BPPFormatPalette&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-ht_get8bppformatpalette)"><strong>HT_Get8BPPFormatPalette</strong></a></p></td>
<td align="left"><p>返回一个半色调调色板，用于每像素标准8位设备类型。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-ht_get8bppmaskpalette" data-raw-source="[&lt;strong&gt;HT_Get8BPPMaskPalette&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-ht_get8bppmaskpalette)"><strong>HT_Get8BPPMaskPalette</strong></a></p></td>
<td align="left"><p>返回8位/像素设备类型的掩码调色板。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-htui_devicecoloradjustment" data-raw-source="[&lt;strong&gt;HTUI_DeviceColorAdjustment&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-htui_devicecoloradjustment)"><strong>HTUI_DeviceColorAdjustment</strong></a></p></td>
<td align="left"><p>显示允许用户调整设备的半色调属性的对话框。</p></td>
</tr>
</tbody>
</table>

 


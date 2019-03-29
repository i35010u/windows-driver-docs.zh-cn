---
title: GDI 半色调服务
description: GDI 半色调服务
ms.assetid: 21112cfc-f7c4-4cce-a9bb-c68d918f5678
keywords:
- GDI WDK Windows 2000 显示、 半色调
- 图形驱动程序 WDK Windows 2000 显示、 半色调
- 绘制 WDK GDI、 半色调
- 半色调 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8832636c506c698e0576b0a8101915cad29f3c7f
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349540"
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
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567314" data-raw-source="[&lt;strong&gt;HT_ComputeRGBGammaTable&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567314)"><strong>HT_ComputeRGBGammaTable</strong></a></p></td>
<td align="left"><p>使 GDI 来计算基于伽玛号的设备红色、 绿色和蓝色强度。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567317" data-raw-source="[&lt;strong&gt;HT_Get8BPPFormatPalette&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567317)"><strong>HT_Get8BPPFormatPalette</strong></a></p></td>
<td align="left"><p>返回用于半色调调色板上的标准将 8 位 / 像素的设备类型。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567320" data-raw-source="[&lt;strong&gt;HT_Get8BPPMaskPalette&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567320)"><strong>HT_Get8BPPMaskPalette</strong></a></p></td>
<td align="left"><p>返回 8 位 / 像素设备类型的掩码调色板。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567308" data-raw-source="[&lt;strong&gt;HTUI_DeviceColorAdjustment&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567308)"><strong>HTUI_DeviceColorAdjustment</strong></a></p></td>
<td align="left"><p>显示一个对话框，允许用户调整设备的半色调属性。</p></td>
</tr>
</tbody>
</table>

 

 

 






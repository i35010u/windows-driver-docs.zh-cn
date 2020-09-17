---
title: 必需的图形驱动程序函数
description: 必需的图形驱动程序函数
ms.assetid: 3a7a7516-b758-4499-bd9d-216fef7b3c8c
keywords:
- GDI WDK Windows 2000 显示、功能、必需
- 图形驱动程序 WDK Windows 2000 显示、功能、必需
- 函数 WDK 图形，必需
- 绘制 WDK GDI，函数，必需
- GDI WDK Windows 2000 显示，DDI，必需的功能
- 图形驱动程序 WDK Windows 2000 显示器、DDI、必需的功能
- DDI WDK 图形，必需的功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b898a9af7db9382c33c5405899aab9c4f2dc7a40
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715134"
---
# <a name="required-graphics-driver-functions"></a>必需的图形驱动程序函数


## <span id="ddk_required_graphics_driver_functions_gg"></span><span id="DDK_REQUIRED_GRAPHICS_DRIVER_FUNCTIONS_GG"></span>


所有图形驱动程序都必须支持 GDI 调用以启用和禁用驱动程序、 *PDEV* 结构和与每个 PDEV 相关联的图面。 下表按通常调用的顺序列出了所需的函数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">入口点</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvenabledriver" data-raw-source="[&lt;strong&gt;DrvEnableDriver&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvenabledriver)"><strong>DrvEnableDriver</strong></a></p></td>
<td align="left"><p>作为初始驱动程序入口点，此函数为 GDI 提供了支持的可选函数的驱动程序版本号和入口点。 这也是 GDI 按名称调用的唯一驱动程序函数。 所有其他驱动程序函数都通过函数指针的表进行访问。 与 <strong>DrvEnableDriver</strong>不同，其他驱动程序函数的名称不是固定的。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvgetmodes" data-raw-source="[&lt;strong&gt;DrvGetModes&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvgetmodes)"><strong>DrvGetModes</strong></a></p></td>
<td align="left"><p>列出指定视频硬件设备支持的模式。  (仅显示驱动程序需要此函数。 ) </p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvenablepdev" data-raw-source="[&lt;strong&gt;DrvEnablePDEV&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvenablepdev)"><strong>DrvEnablePDEV</strong></a></p></td>
<td align="left"><p>启用 PDEV。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvcompletepdev" data-raw-source="[&lt;strong&gt;DrvCompletePDEV&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvcompletepdev)"><strong>DrvCompletePDEV</strong></a></p></td>
<td align="left"><p>设备安装完成后通知驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvenablesurface" data-raw-source="[&lt;strong&gt;DrvEnableSurface&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvenablesurface)"><strong>DrvEnableSurface</strong></a></p></td>
<td align="left"><p>创建指定硬件设备的图面。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvdisablesurface" data-raw-source="[&lt;strong&gt;DrvDisableSurface&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvdisablesurface)"><strong>DrvDisableSurface</strong></a></p></td>
<td align="left"><p>通知驱动程序不再需要为当前设备创建的图面。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvdisablepdev" data-raw-source="[&lt;strong&gt;DrvDisablePDEV&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvdisablepdev)"><strong>DrvDisablePDEV</strong></a></p></td>
<td align="left"><p>当不再需要硬件时，将释放设备使用的内存和资源以及创建的任何表面，但尚未删除。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvdisabledriver" data-raw-source="[&lt;strong&gt;DrvDisableDriver&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvdisabledriver)"><strong>DrvDisableDriver</strong></a></p></td>
<td align="left"><p>释放驱动程序的所有已分配资源，并将设备返回到它的初始状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvassertmode" data-raw-source="[&lt;strong&gt;DrvAssertMode&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvassertmode)"><strong>DrvAssertMode</strong></a></p></td>
<td align="left"><p>重置指定硬件设备的视频模式。  (仅显示驱动程序需要此函数。 ) </p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvresetdevice" data-raw-source="[&lt;strong&gt;DrvResetDevice&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvresetdevice)"><strong>DrvResetDevice</strong></a></p></td>
<td align="left"><p>当设备变为不可操作或无响应时重置设备。</p></td>
</tr>
</tbody>
</table>

 


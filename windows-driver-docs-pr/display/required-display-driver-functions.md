---
title: 必需的显示驱动程序函数
description: 必需的显示驱动程序函数
ms.assetid: 483aa13b-a14d-49f3-8265-013f7bb64d40
keywords:
- 图形 DDI 函数 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 097f80b4853c451fd3c63ecd3265d47bc647ffc0
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716000"
---
# <a name="required-display-driver-functions"></a>必需的显示驱动程序函数


## <span id="ddk_required_display_driver_functions_gg"></span><span id="DDK_REQUIRED_DISPLAY_DRIVER_FUNCTIONS_GG"></span>


每个显示驱动程序至少必须：

1.  启用和禁用图形硬件。

2.  为 GDI 提供有关硬件功能的信息。

3.  启用绘制图面。

下表列出了所有显示驱动程序都必须实现的函数。 按照 **DrvEnableDriver**，剩余的函数按字母顺序列出。 请注意， **DrvEnableDriver**（GDI 按名称调用，其他所有显示器驱动程序函数不具有固定名称）除外，并与 pseudonames 一起列出。

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
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvenabledriver" data-raw-source="[&lt;strong&gt;DrvEnableDriver&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvenabledriver)"><strong>DrvEnableDriver</strong></a></p></td>
<td align="left"><p>作为初始驱动程序入口点，提供 GDI，其中包含支持的可选函数的驱动程序版本号和入口点。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvassertmode" data-raw-source="[&lt;strong&gt;DrvAssertMode&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvassertmode)"><strong>DrvAssertMode</strong></a></p></td>
<td align="left"><p>重置指定视频硬件设备的视频模式。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvcompletepdev" data-raw-source="[&lt;strong&gt;DrvCompletePDEV&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvcompletepdev)"><strong>DrvCompletePDEV</strong></a></p></td>
<td align="left"><p>通知驱动程序设备安装完成。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvdisabledriver" data-raw-source="[&lt;strong&gt;DrvDisableDriver&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvdisabledriver)"><strong>DrvDisableDriver</strong></a></p></td>
<td align="left"><p>释放驱动程序的所有已分配资源，并将设备返回到其初始加载状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvdisablepdev" data-raw-source="[&lt;strong&gt;DrvDisablePDEV&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvdisablepdev)"><strong>DrvDisablePDEV</strong></a></p></td>
<td align="left"><p>当不再需要硬件时，将释放设备使用的内存和资源以及创建的任何表面，但尚未删除。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvdisablesurface" data-raw-source="[&lt;strong&gt;DrvDisableSurface&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvdisablesurface)"><strong>DrvDisableSurface</strong></a></p></td>
<td align="left"><p>通知驱动程序不再需要为当前设备创建的图面。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvenablepdev" data-raw-source="[&lt;strong&gt;DrvEnablePDEV&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvenablepdev)"><strong>DrvEnablePDEV</strong></a></p></td>
<td align="left"><p>启用 <a href="/windows-hardware/drivers/#wdkgloss-pdev" data-raw-source="&lt;em&gt;PDEV&lt;/em&gt;"><em>PDEV</em></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvenablesurface" data-raw-source="[&lt;strong&gt;DrvEnableSurface&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvenablesurface)"><strong>DrvEnableSurface</strong></a></p></td>
<td align="left"><p>创建指定硬件设备的图面。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvgetmodes" data-raw-source="[&lt;strong&gt;DrvGetModes&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvgetmodes)"><strong>DrvGetModes</strong></a></p></td>
<td align="left"><p>列出指定视频硬件设备支持的模式。</p></td>
</tr>
</tbody>
</table>

 

所有图形驱动程序所需的函数列表显示在 [所需的图形驱动程序函数](required-graphics-driver-functions.md)中。


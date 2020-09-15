---
title: 允许的驱动程序加速的动态更改
description: 允许的驱动程序加速的动态更改
ms.assetid: a80bb755-f4ff-4d5d-aff1-28f8262061ae
keywords:
- 加速级别 WDK Windows 2000 显示
- 驱动程序加速 WDK Windows 2000 显示
- 控制面板滑块控件 WDK Windows 2000 显示
- GDI 加速更改 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3fc45dadda5a3ecede67f26f59c2d961a6cf36a9
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90107280"
---
# <a name="dynamic-change-of-permitted-driver-accelerations"></a>允许的驱动程序加速的动态更改


## <span id="ddk_dynamic_change_of_permitted_driver_accelerations_gg"></span><span id="DDK_DYNAMIC_CHANGE_OF_PERMITTED_DRIVER_ACCELERATIONS_GG"></span>


通过使用通过单击控制面板中的 "显示" 图标生成的滑块，可以通过用户界面更改驱动程序的加速级别。 根据此滑块设置的值，GDI 允许下表中列出的下列驱动程序加速级别。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">“值”</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>允许使用所有显示器驱动程序加速。</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-drvsetpointershape" data-raw-source="[&lt;strong&gt;DrvSetPointerShape&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvsetpointershape)"><strong>DrvSetPointerShape</strong></a> 和 <a href="/windows/desktop/api/winddi/nf-winddi-drvcreatedevicebitmap" data-raw-source="[&lt;strong&gt;DrvCreateDeviceBitmap&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvcreatedevicebitmap)"><strong>DrvCreateDeviceBitmap</strong></a> 已禁用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>除1外，不允许更复杂的显示驱动程序加速，包括 <a href="/windows/desktop/api/winddi/nf-winddi-drvstretchblt" data-raw-source="[&lt;strong&gt;DrvStretchBlt&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvstretchblt)"><strong>DrvStretchBlt</strong></a>、 <a href="/windows/desktop/api/winddi/nf-winddi-drvfillpath" data-raw-source="[&lt;strong&gt;DrvFillPath&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvfillpath)"><strong>DrvFillPath</strong></a>、 <a href="/windows/desktop/api/winddi/nf-winddi-drvgradientfill" data-raw-source="[&lt;strong&gt;DrvGradientFill&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvgradientfill)"><strong>DrvGradientFill</strong></a>、 <a href="/windows/desktop/api/winddi/nf-winddi-drvlineto" data-raw-source="[&lt;strong&gt;DrvLineTo&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvlineto)"><strong>DrvLineTo</strong></a>、 <a href="/windows/desktop/api/winddi/nf-winddi-drvalphablend" data-raw-source="[&lt;strong&gt;DrvAlphaBlend&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvalphablend)"><strong>DrvAlphaBlend</strong></a>和 <a href="/windows/desktop/api/winddi/nf-winddi-drvtransparentblt" data-raw-source="[&lt;strong&gt;DrvTransparentBlt&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvtransparentblt)"><strong>DrvTransparentBlt</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>3</p></td>
<td align="left"><p>除2外，不允许所有 DirectDraw 和 Direct3D 加速。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>4</p></td>
<td align="left"><p>除了3外，不允许几乎所有显示器驱动程序加速，纯色填充、 <a href="/windows/desktop/api/winddi/nf-winddi-drvcopybits" data-raw-source="[&lt;strong&gt;DrvCopyBits&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvcopybits)"><strong>DrvCopyBits</strong></a>、 <a href="/windows/desktop/api/winddi/nf-winddi-drvtextout" data-raw-source="[&lt;strong&gt;DrvTextOut&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvtextout)"><strong>DrvTextOut</strong></a>和 <a href="/windows/desktop/api/winddi/nf-winddi-drvstrokepath" data-raw-source="[&lt;strong&gt;DrvStrokePath&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvstrokepath)"><strong>DrvStrokePath</strong></a>除外。 <a href="/windows/desktop/api/winddi/nf-winddi-drvescape" data-raw-source="[&lt;strong&gt;DrvEscape&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvescape)"><strong>DrvEscape</strong></a> 已禁用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>5</p></td>
<td align="left"><p>不允许硬件加速。 只会调用该驱动程序来执行从系统内存表面到屏幕的位块传输。</p></td>
</tr>
</tbody>
</table>

 

显示驱动程序可以通过以下方式确定当前加速级别：

-   通过实现 [**DrvNotify**](/windows/desktop/api/winddi/nf-winddi-drvnotify)接收从 GDI 对加速级别的更改的通知。

-   调用 [**EngQueryDeviceAttribute**](/windows/desktop/api/winddi/nf-winddi-engquerydeviceattribute) 以查询当前加速级别。


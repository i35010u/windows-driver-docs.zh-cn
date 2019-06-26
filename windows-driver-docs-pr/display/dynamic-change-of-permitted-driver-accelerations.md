---
title: 允许的驱动程序加速的动态更改
description: 允许的驱动程序加速的动态更改
ms.assetid: a80bb755-f4ff-4d5d-aff1-28f8262061ae
keywords:
- 加速级别 WDK Windows 2000 显示
- 显示驱动程序加速程序 WDK Windows 2000
- 控制面板滑块控件 WDK Windows 2000 显示
- 显示 GDI 加速更改 WDK Windows 2000
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 34eccb53ece05c95a537c9153f2585db1bd90969
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375803"
---
# <a name="dynamic-change-of-permitted-driver-accelerations"></a>允许的驱动程序加速的动态更改


## <span id="ddk_dynamic_change_of_permitted_driver_accelerations_gg"></span><span id="DDK_DYNAMIC_CHANGE_OF_PERMITTED_DRIVER_ACCELERATIONS_GG"></span>


通过使用生成的单击控制面板中的显示图标的滑块，可以通过用户界面更改驱动程序的加速级别。 具体取决于使用此滑块设置的值，GDI 允许以下级别的下表中列出的驱动程序加速。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ReplTest1</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>允许显示驱动程序加速功能。</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsetpointershape" data-raw-source="[&lt;strong&gt;DrvSetPointerShape&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsetpointershape)"><strong>DrvSetPointerShape</strong> </a>并<a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvcreatedevicebitmap" data-raw-source="[&lt;strong&gt;DrvCreateDeviceBitmap&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvcreatedevicebitmap)"> <strong>DrvCreateDeviceBitmap</strong> </a>处于禁用状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>除了 1，不允许更复杂的显示驱动程序加速功能，包括<a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstretchblt" data-raw-source="[&lt;strong&gt;DrvStretchBlt&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstretchblt)"> <strong>DrvStretchBlt</strong></a>， <a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvfillpath" data-raw-source="[&lt;strong&gt;DrvFillPath&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvfillpath)"> <strong>DrvFillPath</strong> </a>， <a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvgradientfill" data-raw-source="[&lt;strong&gt;DrvGradientFill&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvgradientfill)"> <strong>DrvGradientFill</strong></a>， <a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvlineto" data-raw-source="[&lt;strong&gt;DrvLineTo&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvlineto)"> <strong>DrvLineTo</strong></a>， <a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvalphablend" data-raw-source="[&lt;strong&gt;DrvAlphaBlend&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvalphablend)"> <strong>DrvAlphaBlend</strong></a>，并<a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtransparentblt" data-raw-source="[&lt;strong&gt;DrvTransparentBlt&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtransparentblt)"> <strong>DrvTransparentBlt</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>3</p></td>
<td align="left"><p>除了 2，不允许所有 DirectDraw 和 Direct3D 加速。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>4</p></td>
<td align="left"><p>除了 3，几乎所有的显示驱动程序加速程序不允许使用纯色填充除外<a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvcopybits" data-raw-source="[&lt;strong&gt;DrvCopyBits&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvcopybits)"> <strong>DrvCopyBits</strong></a>， <a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtextout" data-raw-source="[&lt;strong&gt;DrvTextOut&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtextout)"> <strong>DrvTextOut</strong> </a>，并<a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstrokepath" data-raw-source="[&lt;strong&gt;DrvStrokePath&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstrokepath)"> <strong>DrvStrokePath</strong></a>。 <a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvescape" data-raw-source="[&lt;strong&gt;DrvEscape&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvescape)"><strong>DrvEscape</strong> </a>被禁用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>5</p></td>
<td align="left"><p>允许没有硬件加速功能。 该驱动程序只会调用从系统内存图面中执行位块传输到屏幕。</p></td>
</tr>
</tbody>
</table>

 

显示驱动程序可以确定由当前的加速级别：

-   接收更改的通知到加速级别从 GDI 通过实现[ **DrvNotify**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvnotify)。

-   调用[ **EngQueryDeviceAttribute** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engquerydeviceattribute)查询当前的加速级别。

 

 






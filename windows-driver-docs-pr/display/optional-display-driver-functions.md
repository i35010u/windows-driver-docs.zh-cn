---
title: 可选的显示驱动程序函数
description: 可选的显示驱动程序函数
ms.assetid: 7c1489c9-40de-4b44-95b7-af227c7d8205
keywords:
- 图形 DDI 函数 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30953153f55fa1691163997f201eec91ddb77b7a
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90106410"
---
# <a name="optional-display-driver-functions"></a>可选的显示驱动程序函数


## <span id="ddk_optional_display_driver_functions_gg"></span><span id="DDK_OPTIONAL_DISPLAY_DRIVER_FUNCTIONS_GG"></span>


为了减小驱动程序的大小，显示驱动程序编写器通常仅添加那些在视频硬件中受支持的可选函数。 显示驱动程序可以实现下表中列出的函数。 这些函数分为以下几类：

位图管理函数

绘制函数

图像颜色管理功能

指针和窗口管理函数

杂项函数

### <a name="span-idddk_bitmap_management_functions_ggspanspan-idddk_bitmap_management_functions_ggspanbitmap-management-functions"></a><span id="ddk_bitmap_management_functions_gg"></span><span id="DDK_BITMAP_MANAGEMENT_FUNCTIONS_GG"></span>位图管理函数

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
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-drvcreatedevicebitmap" data-raw-source="[&lt;strong&gt;DrvCreateDeviceBitmap&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvcreatedevicebitmap)"><strong>DrvCreateDeviceBitmap</strong></a></p></td>
<td align="left"><p>使用驱动程序定义的格式创建和管理位图。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-drvdeletedevicebitmap" data-raw-source="[&lt;strong&gt;DrvDeleteDeviceBitmap&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvdeletedevicebitmap)"><strong>DrvDeleteDeviceBitmap</strong></a></p></td>
<td align="left"><p>删除设备托管的位图。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idddk_drawing_functions_ggspanspan-idddk_drawing_functions_ggspandrawing-functions"></a><span id="ddk_drawing_functions_gg"></span><span id="DDK_DRAWING_FUNCTIONS_GG"></span>绘制函数

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
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-drvalphablend" data-raw-source="[&lt;strong&gt;DrvAlphaBlend&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvalphablend)"><strong>DrvAlphaBlend</strong></a></p></td>
<td align="left"><p>提供带<a href="/windows-hardware/drivers/#wdkgloss-alpha-blending" data-raw-source="&lt;em&gt;alpha blending&lt;/em&gt;"><em>alpha 混合</em></a>的<a href="/windows-hardware/drivers/#wdkgloss-bit-block-transfer" data-raw-source="&lt;em&gt;bit-block transfer&lt;/em&gt;"><em>位块传输</em></a>功能。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-drvbitblt" data-raw-source="[&lt;strong&gt;DrvBitBlt&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvbitblt)"><strong>DrvBitBlt</strong></a></p></td>
<td align="left"><p>提供 <a href="/windows-hardware/drivers/#wdkgloss-device-managed-surface" data-raw-source="&lt;em&gt;device-managed surfaces&lt;/em&gt;"><em>设备管理</em></a>的图面之间的一般位块传输功能，在 GDI 管理的标准格式位图之间，或在设备管理的图面和 GDI 托管的标准格式位图之间提供。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-drvdithercolor" data-raw-source="[&lt;strong&gt;DrvDitherColor&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvdithercolor)"><strong>DrvDitherColor</strong></a></p></td>
<td align="left"><p>请求设备根据 <a href="/windows-hardware/drivers/#wdkgloss-device-palette" data-raw-source="&lt;em&gt;device palette&lt;/em&gt;"><em>设备调色板</em></a>创建画笔抖动。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-drvfillpath" data-raw-source="[&lt;strong&gt;DrvFillPath&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvfillpath)"><strong>DrvFillPath</strong></a></p></td>
<td align="left"><p>为设备管理的图面绘制闭合路径。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-drvgradientfill" data-raw-source="[&lt;strong&gt;DrvGradientFill&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvgradientfill)"><strong>DrvGradientFill</strong></a></p></td>
<td align="left"><p>指定基元的底纹。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-drvlineto" data-raw-source="[&lt;strong&gt;DrvLineTo&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvlineto)"><strong>DrvLineTo</strong></a></p></td>
<td align="left"><p>绘制单个纯纯整数修饰线。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-drvplgblt" data-raw-source="[&lt;strong&gt;DrvPlgBlt&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvplgblt)"><strong>DrvPlgBlt</strong></a></p></td>
<td align="left"><p>在设备托管和 GDI 管理的图面组合之间提供旋转 <a href="/windows-hardware/drivers/#wdkgloss-bit-block-transfer" data-raw-source="&lt;em&gt;bit-block transfer&lt;/em&gt;"><em>位块传输</em></a> 功能。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-drvrealizebrush" data-raw-source="[&lt;strong&gt;DrvRealizeBrush&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvrealizebrush)"><strong>DrvRealizeBrush</strong></a></p></td>
<td align="left"><p>为定义的图面实现指定的画笔。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-drvstretchblt" data-raw-source="[&lt;strong&gt;DrvStretchBlt&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvstretchblt)"><strong>DrvStretchBlt</strong></a></p></td>
<td align="left"><p>允许在设备托管和 GDI 管理的图面之间传输拉伸块。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-drvstretchbltrop" data-raw-source="[&lt;strong&gt;DrvStretchBltROP&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvstretchbltrop)"><strong>DrvStretchBltROP</strong></a></p></td>
<td align="left"><p>使用 <a href="/windows-hardware/drivers/#wdkgloss-raster-operation--rop-" data-raw-source="&lt;em&gt;ROP&lt;/em&gt;"><em>ROP</em></a>执行拉伸位块传输。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-drvstrokeandfillpath" data-raw-source="[&lt;strong&gt;DrvStrokeAndFillPath&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvstrokeandfillpath)"><strong>DrvStrokeAndFillPath</strong></a></p></td>
<td align="left"><p>同时笔划和填充路径。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-drvtransparentblt" data-raw-source="[&lt;strong&gt;DrvTransparentBlt&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvtransparentblt)"><strong>DrvTransparentBlt</strong></a></p></td>
<td align="left"><p>提供具有透明度的位块传输功能。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idddk_image_color_management_functions_ggspanspan-idddk_image_color_management_functions_ggspanimage-color-management-functions"></a><span id="ddk_image_color_management_functions_gg"></span><span id="DDK_IMAGE_COLOR_MANAGEMENT_FUNCTIONS_GG"></span>图像颜色管理功能

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
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-drvicmcheckbitmapbits" data-raw-source="[&lt;strong&gt;DrvIcmCheckBitmapBits&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvicmcheckbitmapbits)"><strong>DrvIcmCheckBitmapBits</strong></a></p></td>
<td align="left"><p>检查指定位图的像素是否位于指定转换的设备范围内。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-drvicmcreatecolortransform" data-raw-source="[&lt;strong&gt;DrvIcmCreateColorTransform&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvicmcreatecolortransform)"><strong>DrvIcmCreateColorTransform</strong></a></p></td>
<td align="left"><p>创建 ICM 颜色转换。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-drvicmdeletecolortransform" data-raw-source="[&lt;strong&gt;DrvIcmDeleteColorTransform&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvicmdeletecolortransform)"><strong>DrvIcmDeleteColorTransform</strong></a></p></td>
<td align="left"><p>删除指定的 ICM 颜色转换。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-drvicmsetdevicegammaramp" data-raw-source="[&lt;strong&gt;DrvIcmSetDeviceGammaRamp&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvicmsetdevicegammaramp)"><strong>DrvIcmSetDeviceGammaRamp</strong></a></p></td>
<td align="left"><p>设置指定显示设备的硬件 <a href="/windows-hardware/drivers/#wdkgloss-gamma-ramp" data-raw-source="&lt;em&gt;gamma ramp&lt;/em&gt;"><em>伽玛坡道</em></a> 。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idddk_pointer_and_window_management_functions_ggspanspan-idddk_pointer_and_window_management_functions_ggspanpointer-and-window-management-functions"></a><span id="ddk_pointer_and_window_management_functions_gg"></span><span id="DDK_POINTER_AND_WINDOW_MANAGEMENT_FUNCTIONS_GG"></span>指针和窗口管理函数

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
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-drvdescribepixelformat" data-raw-source="[&lt;strong&gt;DrvDescribePixelFormat&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvdescribepixelformat)"><strong>DrvDescribePixelFormat</strong></a></p></td>
<td align="left"><p>介绍设备指定的 PDEV 的像素格式，方法是将像素格式说明写入 PIXELFORMATDESCRIPTOR 结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-drvmovepointer" data-raw-source="[&lt;strong&gt;DrvMovePointer&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvmovepointer)"><strong>DrvMovePointer</strong></a></p></td>
<td align="left"><p>将指针移动到一个新位置并进行重绘。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-drvsavescreenbits" data-raw-source="[&lt;strong&gt;DrvSaveScreenBits&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvsavescreenbits)"><strong>DrvSaveScreenBits</strong></a></p></td>
<td align="left"><p>保存或还原屏幕的指定矩形。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-drvsetpixelformat" data-raw-source="[&lt;strong&gt;DrvSetPixelFormat&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvsetpixelformat)"><strong>DrvSetPixelFormat</strong></a></p></td>
<td align="left"><p>设置窗口的像素格式。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-drvsetpointershape" data-raw-source="[&lt;strong&gt;DrvSetPointerShape&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvsetpointershape)"><strong>DrvSetPointerShape</strong></a></p></td>
<td align="left"><p>如果驱动程序已绘制指针，则从屏幕中删除该指针，然后设置新的指针形状。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idddk_miscellaneous_functions_ggspanspan-idddk_miscellaneous_functions_ggspanmiscellaneous-functions"></a><span id="ddk_miscellaneous_functions_gg"></span><span id="DDK_MISCELLANEOUS_FUNCTIONS_GG"></span>杂项函数

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
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-drvdestroyfont" data-raw-source="[&lt;strong&gt;DrvDestroyFont&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvdestroyfont)"><strong>DrvDestroyFont</strong></a></p></td>
<td align="left"><p>通知驱动程序不再需要字体实现;驱动程序可以释放已分配的数据结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-drvdrawescape" data-raw-source="[&lt;strong&gt;DrvDrawEscape&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvdrawescape)"><strong>DrvDrawEscape</strong></a></p></td>
<td align="left"><p>实现绘图类型转义函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-drvescape" data-raw-source="[&lt;strong&gt;DrvEscape&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvescape)"><strong>DrvEscape</strong></a></p></td>
<td align="left"><p>从与设备无关的图形 DDI 中无法使用的设备中查询信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-drvfree" data-raw-source="[&lt;strong&gt;DrvFree&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvfree)"><strong>DrvFree</strong></a></p></td>
<td align="left"><p>释放与指示的数据结构关联的存储。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-drvnotify" data-raw-source="[&lt;strong&gt;DrvNotify&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvnotify)"><strong>DrvNotify</strong></a></p></td>
<td align="left"><p>允许通过 GDI 通知显示驱动程序的某些信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-drvsynchronize" data-raw-source="[&lt;strong&gt;DrvSynchronize&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvsynchronize)"><strong>DrvSynchronize</strong></a></p></td>
<td align="left"><p>协调 GDI 和显示器驱动程序支持的协处理器设备之间的绘图操作;仅适用于 <a href="/windows-hardware/drivers/#wdkgloss-engine-managed-surface" data-raw-source="&lt;em&gt;engine-managed surfaces&lt;/em&gt;"><em>引擎托管</em></a> 的图面。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-drvsynchronizesurface" data-raw-source="[&lt;strong&gt;DrvSynchronizeSurface&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvsynchronizesurface)"><strong>DrvSynchronizeSurface</strong></a></p></td>
<td align="left"><p>允许设备协处理器执行的绘图操作与 GDI 进行协调。</p></td>
</tr>
</tbody>
</table>

 

显示驱动程序还可以选择实现 Microsoft DirectDraw 和/或 Direct3D 接口。 有关详细信息，请参阅以下部分：

[DirectDraw](directdraw.md)

[Direct3D DDI](direct3d.md)

所有图形驱动程序的可选功能列表显示在 [可选图形驱动程序函数](optional-graphics-driver-functions.md)中。


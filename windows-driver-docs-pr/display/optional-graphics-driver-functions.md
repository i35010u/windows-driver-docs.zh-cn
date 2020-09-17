---
title: 可选的图形驱动程序函数
description: 可选的图形驱动程序函数
ms.assetid: 3cdef152-4bcc-426a-9aa7-fd94acf2331f
keywords:
- GDI WDK Windows 2000 显示、功能、可选
- 图形驱动程序 WDK Windows 2000 显示、功能、可选
- 函数 WDK 图形，可选
- 绘制 WDK GDI，函数，可选
- GDI WDK Windows 2000 显示器、DDI、可选功能
- 图形驱动程序 WDK Windows 2000 显示器、DDI、可选功能
- DDI WDK 图形，可选功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4da6a3f1cafdd9cb7be52ab6eb50d2313e85498e
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90714745"
---
# <a name="optional-graphics-driver-functions"></a>可选的图形驱动程序函数


## <span id="ddk_optional_graphics_driver_functions_gg"></span><span id="DDK_OPTIONAL_GRAPHICS_DRIVER_FUNCTIONS_GG"></span>


在降低驱动程序大小时，驱动程序编写者通常仅添加硬件中支持良好的可选函数。 例如，支持图像颜色管理 (ICM) 的硬件驱动程序可以实现 *DrvIcmXxx* 函数。 下表列出了图形驱动程序可以选择实现的函数。

### <a name="span-iddisplay_and_printer_driver_functions_spanspan-iddisplay_and_printer_driver_functions_spanspan-iddisplay_and_printer_driver_functions_spandisplay-and-printer-driver-functions"></a><span id="Display_and_Printer_Driver_Functions_"></span><span id="display_and_printer_driver_functions_"></span><span id="DISPLAY_AND_PRINTER_DRIVER_FUNCTIONS_"></span>显示和打印机驱动程序功能

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
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvalphablend" data-raw-source="[&lt;strong&gt;DrvAlphaBlend&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvalphablend)"><strong>DrvAlphaBlend</strong></a></p></td>
<td align="left"><p>提供带 <a href="/windows-hardware/drivers/#wdkgloss-alpha-blending" data-raw-source="&lt;em&gt;alpha blending&lt;/em&gt;"><em>alpha 混合</em></a>的位块传输功能。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvbitblt" data-raw-source="[&lt;strong&gt;DrvBitBlt&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvbitblt)"><strong>DrvBitBlt</strong></a></p></td>
<td align="left"><p>执行到和从曲面进行的一般位块传输。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvcreatedevicebitmap" data-raw-source="[&lt;strong&gt;DrvCreateDeviceBitmap&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvcreatedevicebitmap)"><strong>DrvCreateDeviceBitmap</strong></a></p></td>
<td align="left"><p>使用驱动程序定义的格式创建和管理位图。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvdeletedevicebitmap" data-raw-source="[&lt;strong&gt;DrvDeleteDeviceBitmap&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvdeletedevicebitmap)"><strong>DrvDeleteDeviceBitmap</strong></a></p></td>
<td align="left"><p>删除设备托管的位图。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvdithercolor" data-raw-source="[&lt;strong&gt;DrvDitherColor&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvdithercolor)"><strong>DrvDitherColor</strong></a></p></td>
<td align="left"><p>请求设备根据 <a href="/windows-hardware/drivers/#wdkgloss-device-palette" data-raw-source="&lt;em&gt;device palette&lt;/em&gt;"><em>设备调色板</em></a>创建画笔抖动。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvfillpath" data-raw-source="[&lt;strong&gt;DrvFillPath&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvfillpath)"><strong>DrvFillPath</strong></a></p></td>
<td align="left"><p>为 <a href="/windows-hardware/drivers/#wdkgloss-device-managed-surface" data-raw-source="&lt;em&gt;device-managed surface&lt;/em&gt;"><em>设备管理的图面</em></a>绘制闭合路径。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvgradientfill" data-raw-source="[&lt;strong&gt;DrvGradientFill&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvgradientfill)"><strong>DrvGradientFill</strong></a></p></td>
<td align="left"><p>指定基元的底纹。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvicmcheckbitmapbits" data-raw-source="[&lt;strong&gt;DrvIcmCheckBitmapBits&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvicmcheckbitmapbits)"><strong>DrvIcmCheckBitmapBits</strong></a></p></td>
<td align="left"><p>检查指定位图的像素是否位于指定转换的设备范围内。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvicmcreatecolortransform" data-raw-source="[&lt;strong&gt;DrvIcmCreateColorTransform&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvicmcreatecolortransform)"><strong>DrvIcmCreateColorTransform</strong></a></p></td>
<td align="left"><p>创建 ICM 颜色转换。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvicmdeletecolortransform" data-raw-source="[&lt;strong&gt;DrvIcmDeleteColorTransform&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvicmdeletecolortransform)"><strong>DrvIcmDeleteColorTransform</strong></a></p></td>
<td align="left"><p>删除指定的 ICM 颜色转换。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvicmsetdevicegammaramp" data-raw-source="[&lt;strong&gt;DrvIcmSetDeviceGammaRamp&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvicmsetdevicegammaramp)"><strong>DrvIcmSetDeviceGammaRamp</strong></a></p></td>
<td align="left"><p>设置指定显示设备的硬件 <a href="/windows-hardware/drivers/#wdkgloss-gamma-ramp" data-raw-source="&lt;em&gt;gamma ramp&lt;/em&gt;"><em>伽玛坡道</em></a> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvlineto" data-raw-source="[&lt;strong&gt;DrvLineTo&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvlineto)"><strong>DrvLineTo</strong></a></p></td>
<td align="left"><p>绘制单个纯纯整数修饰线。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvplgblt" data-raw-source="[&lt;strong&gt;DrvPlgBlt&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvplgblt)"><strong>DrvPlgBlt</strong></a></p></td>
<td align="left"><p>在设备托管和 GDI 管理的图面组合之间提供旋转位块传输功能。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvrealizebrush" data-raw-source="[&lt;strong&gt;DrvRealizeBrush&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvrealizebrush)"><strong>DrvRealizeBrush</strong></a></p></td>
<td align="left"><p>为定义的图面实现指定的画笔。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvstretchblt" data-raw-source="[&lt;strong&gt;DrvStretchBlt&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvstretchblt)"><strong>DrvStretchBlt</strong></a></p></td>
<td align="left"><p>允许在设备托管和 GDI 管理的图面之间传输拉伸块。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvstretchbltrop" data-raw-source="[&lt;strong&gt;DrvStretchBltROP&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvstretchbltrop)"><strong>DrvStretchBltROP</strong></a></p></td>
<td align="left"><p>使用 <a href="/windows-hardware/drivers/#wdkgloss-raster-operation--rop-" data-raw-source="&lt;em&gt;ROP&lt;/em&gt;"><em>ROP</em></a>执行拉伸位块传输。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvstrokeandfillpath" data-raw-source="[&lt;strong&gt;DrvStrokeAndFillPath&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvstrokeandfillpath)"><strong>DrvStrokeAndFillPath</strong></a></p></td>
<td align="left"><p>同时填充和笔划路径。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvsynchronize" data-raw-source="[&lt;strong&gt;DrvSynchronize&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvsynchronize)"><strong>DrvSynchronize</strong></a></p></td>
<td align="left"><p>协调 GDI 和显示器驱动程序支持的协处理器设备之间的绘图操作;仅适用于 <a href="/windows-hardware/drivers/#wdkgloss-engine-managed-surface" data-raw-source="&lt;em&gt;engine-managed surfaces&lt;/em&gt;"><em>引擎托管</em></a> 的图面。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvsynchronizesurface" data-raw-source="[&lt;strong&gt;DrvSynchronizeSurface&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvsynchronizesurface)"><strong>DrvSynchronizeSurface</strong></a></p></td>
<td align="left"><p>协调 GDI 和显示器驱动程序支持的协处理器设备之间的绘图操作;仅适用于引擎托管的图面。 如果驱动程序同时提供了 <em>DrvSynchronize</em> 和 <em>DrvSynchronizeSurface</em>，则 GDI 将仅调用 <em>DrvSynchronizeSurface</em>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvtransparentblt" data-raw-source="[&lt;strong&gt;DrvTransparentBlt&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvtransparentblt)"><strong>DrvTransparentBlt</strong></a></p></td>
<td align="left"><p>提供具有透明度的位块传输功能。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idfunctions_used_exclusively_by_display_driversspanspan-idfunctions_used_exclusively_by_display_driversspanspan-idfunctions_used_exclusively_by_display_driversspanfunctions-used-exclusively-by-display-drivers"></a><span id="Functions_Used_Exclusively_by_Display_Drivers"></span><span id="functions_used_exclusively_by_display_drivers"></span><span id="FUNCTIONS_USED_EXCLUSIVELY_BY_DISPLAY_DRIVERS"></span>由显示驱动程序独占使用的函数

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
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvmovepointer" data-raw-source="[&lt;strong&gt;DrvMovePointer&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvmovepointer)"><strong>DrvMovePointer</strong></a></p></td>
<td align="left"><p>将指针移动到一个新位置，然后重绘该位置。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvsavescreenbits" data-raw-source="[&lt;strong&gt;DrvSaveScreenBits&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvsavescreenbits)"><strong>DrvSaveScreenBits</strong></a></p></td>
<td align="left"><p>仅)  (显示驱动程序的屏幕上保存或还原指定的矩形。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvsetpointershape" data-raw-source="[&lt;strong&gt;DrvSetPointerShape&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvsetpointershape)"><strong>DrvSetPointerShape</strong></a></p></td>
<td align="left"><p>如果驱动程序已绘制指针，则从屏幕中删除该指针，然后设置新的指针形状。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idfunctions_used_primarily_by_printer_driversspanspan-idfunctions_used_primarily_by_printer_driversspanspan-idfunctions_used_primarily_by_printer_driversspanfunctions-used-primarily-by-printer-drivers"></a><span id="Functions_Used_Primarily_by_Printer_Drivers"></span><span id="functions_used_primarily_by_printer_drivers"></span><span id="FUNCTIONS_USED_PRIMARILY_BY_PRINTER_DRIVERS"></span>主要由打印机驱动程序使用的函数

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
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvdestroyfont" data-raw-source="[&lt;strong&gt;DrvDestroyFont&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvdestroyfont)"><strong>DrvDestroyFont</strong></a></p></td>
<td align="left"><p>通知驱动程序不再需要字体实现;驱动程序可以释放已分配的数据结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvdrawescape" data-raw-source="[&lt;strong&gt;DrvDrawEscape&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvdrawescape)"><strong>DrvDrawEscape</strong></a></p></td>
<td align="left"><p>实现绘图类型转义函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvescape" data-raw-source="[&lt;strong&gt;DrvEscape&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvescape)"><strong>DrvEscape</strong></a></p></td>
<td align="left"><p>查询设备上不支持的设备中的信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvfree" data-raw-source="[&lt;strong&gt;DrvFree&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvfree)"><strong>DrvFree</strong></a></p></td>
<td align="left"><p>释放与指示的数据结构关联的字体存储。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idfunctions_used_exclusively_by_printer_driversspanspan-idfunctions_used_exclusively_by_printer_driversspanspan-idfunctions_used_exclusively_by_printer_driversspanfunctions-used-exclusively-by-printer-drivers"></a><span id="Functions_Used_Exclusively_by_Printer_Drivers"></span><span id="functions_used_exclusively_by_printer_drivers"></span><span id="FUNCTIONS_USED_EXCLUSIVELY_BY_PRINTER_DRIVERS"></span>打印机驱动程序专门使用的函数

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
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvenddoc" data-raw-source="[&lt;strong&gt;DrvEndDoc&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvenddoc)"><strong>DrvEndDoc</strong></a></p></td>
<td align="left"><p>发送文档结尾信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvfontmanagement" data-raw-source="[&lt;strong&gt;DrvFontManagement&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvfontmanagement)"><strong>DrvFontManagement</strong></a></p></td>
<td align="left"><p>允许访问无法通过 GDI 直接提供的打印机功能。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvgetglyphmode" data-raw-source="[&lt;strong&gt;DrvGetGlyphMode&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvgetglyphmode)"><strong>DrvGetGlyphMode</strong></a></p></td>
<td align="left"><p>返回要为特定字体存储的字体信息的类型。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvnextband" data-raw-source="[&lt;strong&gt;DrvNextBand&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvnextband)"><strong>DrvNextBand</strong></a></p></td>
<td align="left"><p>认识图面上画的带区的内容。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvqueryperbandinfo" data-raw-source="[&lt;em&gt;DrvQueryPerBandInfo&lt;/em&gt;](/windows/win32/api/winddi/nf-winddi-drvqueryperbandinfo)"><em>DrvQueryPerBandInfo</em></a></p></td>
<td align="left"><p>返回指定的镶边打印机图面的分级信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvsendpage" data-raw-source="[&lt;em&gt;DrvSendPage&lt;/em&gt;](/windows/win32/api/winddi/nf-winddi-drvsendpage)"><em>DrvSendPage</em></a></p></td>
<td align="left"><p>将原始位从表面发送到打印机。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvstartbanding" data-raw-source="[&lt;strong&gt;DrvStartBanding&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvstartbanding)"><strong>DrvStartBanding</strong></a></p></td>
<td align="left"><p>准备适用于分级的驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvstartdoc" data-raw-source="[&lt;strong&gt;DrvStartDoc&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvstartdoc)"><strong>DrvStartDoc</strong></a></p></td>
<td align="left"><p>发送文档开头的控件信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvstartpage" data-raw-source="[&lt;strong&gt;DrvStartPage&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvstartpage)"><strong>DrvStartPage</strong></a></p></td>
<td align="left"><p>发送页面起始控制信息。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idfont_driver_functionspanspan-idfont_driver_functionspanspan-idfont_driver_functionspanfont-driver-function"></a><span id="Font_Driver_Function"></span><span id="font_driver_function"></span><span id="FONT_DRIVER_FUNCTION"></span>Font Driver 函数

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
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvqueryadvancewidths" data-raw-source="[&lt;strong&gt;DrvQueryAdvanceWidths&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvqueryadvancewidths)"><strong>DrvQueryAdvanceWidths</strong></a></p></td>
<td align="left"><p>为一组指定的字形提供字符步进宽度。</p></td>
</tr>
</tbody>
</table>

 


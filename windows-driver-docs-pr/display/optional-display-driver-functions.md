---
title: 可选的显示驱动程序函数
description: 可选的显示驱动程序函数
ms.assetid: 7c1489c9-40de-4b44-95b7-af227c7d8205
keywords:
- 显示图形 DDI 函数 WDK Windows 2000
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30f841fe876dab7b0114b4ceb435625a21450c4e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383989"
---
# <a name="optional-display-driver-functions"></a>可选的显示驱动程序函数


## <span id="ddk_optional_display_driver_functions_gg"></span><span id="DDK_OPTIONAL_DISPLAY_DRIVER_FUNCTIONS_GG"></span>


为了减少驱动程序大小，显示驱动程序编写人员通常将添加仅视频硬件中均受到大力支持这些可选功能。 显示驱动程序可以实现以下各表中列出的函数。 这些函数按以下类别：

位图管理函数

绘图函数

图像颜色管理函数

指针和窗口管理函数

杂项函数

### <a name="span-idddkbitmapmanagementfunctionsggspanspan-idddkbitmapmanagementfunctionsggspanbitmap-management-functions"></a><span id="ddk_bitmap_management_functions_gg"></span><span id="DDK_BITMAP_MANAGEMENT_FUNCTIONS_GG"></span>位图管理函数

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556185" data-raw-source="[&lt;strong&gt;DrvCreateDeviceBitmap&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556185)"><strong>DrvCreateDeviceBitmap</strong></a></p></td>
<td align="left"><p>创建和管理采用驱动程序定义的格式的位图。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556187" data-raw-source="[&lt;strong&gt;DrvDeleteDeviceBitmap&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556187)"><strong>DrvDeleteDeviceBitmap</strong></a></p></td>
<td align="left"><p>删除设备管理的位图。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idddkdrawingfunctionsggspanspan-idddkdrawingfunctionsggspandrawing-functions"></a><span id="ddk_drawing_functions_gg"></span><span id="DDK_DRAWING_FUNCTIONS_GG"></span>绘图函数

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556176" data-raw-source="[&lt;strong&gt;DrvAlphaBlend&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556176)"><strong>DrvAlphaBlend</strong></a></p></td>
<td align="left"><p>提供了<a href="https://msdn.microsoft.com/library/windows/hardware/ff556272#wdkgloss-bit-block-transfer" data-raw-source="&lt;em&gt;bit-block transfer&lt;/em&gt;"><em>位块传输</em></a>使用的功能<a href="https://msdn.microsoft.com/library/windows/hardware/ff556270#wdkgloss-alpha-blending" data-raw-source="&lt;em&gt;alpha blending&lt;/em&gt;"> <em>alpha 值混合处理</em></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556180" data-raw-source="[&lt;strong&gt;DrvBitBlt&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556180)"><strong>DrvBitBlt</strong></a></p></td>
<td align="left"><p>提供常规位块传输之间的功能<a href="https://msdn.microsoft.com/library/windows/hardware/ff556277#wdkgloss-device-managed-surface" data-raw-source="&lt;em&gt;device-managed surfaces&lt;/em&gt;"><em>设备管理面</em></a>、 GDI 托管标准格式的位图，之间或设备管理面和 GDI 托管之间标准格式的位图。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556202" data-raw-source="[&lt;strong&gt;DrvDitherColor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556202)"><strong>DrvDitherColor</strong></a></p></td>
<td align="left"><p>请求针对的设备来创建画笔抖色<a href="https://msdn.microsoft.com/library/windows/hardware/ff556277#wdkgloss-device-palette" data-raw-source="&lt;em&gt;device palette&lt;/em&gt;"><em>设备调色板</em></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556220" data-raw-source="[&lt;strong&gt;DrvFillPath&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556220)"><strong>DrvFillPath</strong></a></p></td>
<td align="left"><p>绘制设备管理面封闭的的路径。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556236" data-raw-source="[&lt;strong&gt;DrvGradientFill&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556236)"><strong>DrvGradientFill</strong></a></p></td>
<td align="left"><p>底纹应用指定的基元。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556245" data-raw-source="[&lt;strong&gt;DrvLineTo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556245)"><strong>DrvLineTo</strong></a></p></td>
<td align="left"><p>绘制单个、 solid、 仅限整数的修饰的行。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556258" data-raw-source="[&lt;strong&gt;DrvPlgBlt&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556258)"><strong>DrvPlgBlt</strong></a></p></td>
<td align="left"><p>提供了旋转<a href="https://msdn.microsoft.com/library/windows/hardware/ff556272#wdkgloss-bit-block-transfer" data-raw-source="&lt;em&gt;bit-block transfer&lt;/em&gt;"><em>位块传输</em></a>之间组合的设备管理和 GDI 管理界面的功能。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556273" data-raw-source="[&lt;strong&gt;DrvRealizeBrush&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556273)"><strong>DrvRealizeBrush</strong></a></p></td>
<td align="left"><p>认识到的指定的画笔来定义的图面。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556302" data-raw-source="[&lt;strong&gt;DrvStretchBlt&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556302)"><strong>DrvStretchBlt</strong></a></p></td>
<td align="left"><p>允许拉伸在设备管理和 GDI 管理界面之间的块传输。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556306" data-raw-source="[&lt;strong&gt;DrvStretchBltROP&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556306)"><strong>DrvStretchBltROP</strong></a></p></td>
<td align="left"><p>执行使用延伸位块传输<a href="https://msdn.microsoft.com/library/windows/hardware/ff556331#wdkgloss-raster-operation--rop-" data-raw-source="&lt;em&gt;ROP&lt;/em&gt;"> <em>ROP</em></a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556311" data-raw-source="[&lt;strong&gt;DrvStrokeAndFillPath&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556311)"><strong>DrvStrokeAndFillPath</strong></a></p></td>
<td align="left"><p>同时描边，并填充一个路径。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff557283" data-raw-source="[&lt;strong&gt;DrvTransparentBlt&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557283)"><strong>DrvTransparentBlt</strong></a></p></td>
<td align="left"><p>使用透明度提供位块传输功能。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idddkimagecolormanagementfunctionsggspanspan-idddkimagecolormanagementfunctionsggspanimage-color-management-functions"></a><span id="ddk_image_color_management_functions_gg"></span><span id="DDK_IMAGE_COLOR_MANAGEMENT_FUNCTIONS_GG"></span>图像颜色管理函数

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556238" data-raw-source="[&lt;strong&gt;DrvIcmCheckBitmapBits&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556238)"><strong>DrvIcmCheckBitmapBits</strong></a></p></td>
<td align="left"><p>检查中指定位图的像素是否包含指定的转换的设备不同时位于。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556239" data-raw-source="[&lt;strong&gt;DrvIcmCreateColorTransform&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556239)"><strong>DrvIcmCreateColorTransform</strong></a></p></td>
<td align="left"><p>创建 ICM 颜色转换。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556241" data-raw-source="[&lt;strong&gt;DrvIcmDeleteColorTransform&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556241)"><strong>DrvIcmDeleteColorTransform</strong></a></p></td>
<td align="left"><p>删除指定的 ICM 颜色转换。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556243" data-raw-source="[&lt;strong&gt;DrvIcmSetDeviceGammaRamp&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556243)"><strong>DrvIcmSetDeviceGammaRamp</strong></a></p></td>
<td align="left"><p>设置硬件<a href="https://msdn.microsoft.com/library/windows/hardware/ff556283#wdkgloss-gamma-ramp" data-raw-source="&lt;em&gt;gamma ramp&lt;/em&gt;"><em>伽马</em></a>的指定的显示设备。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idddkpointerandwindowmanagementfunctionsggspanspan-idddkpointerandwindowmanagementfunctionsggspanpointer-and-window-management-functions"></a><span id="ddk_pointer_and_window_management_functions_gg"></span><span id="DDK_POINTER_AND_WINDOW_MANAGEMENT_FUNCTIONS_GG"></span>指针和窗口管理函数

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556190" data-raw-source="[&lt;strong&gt;DrvDescribePixelFormat&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556190)"><strong>DrvDescribePixelFormat</strong></a></p></td>
<td align="left"><p>介绍设备指定 PDEV 向 PIXELFORMATDESCRIPTOR 结构写入像素格式描述像素格式。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556248" data-raw-source="[&lt;strong&gt;DrvMovePointer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556248)"><strong>DrvMovePointer</strong></a></p></td>
<td align="left"><p>将指针移至新位置并重新绘制它。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556278" data-raw-source="[&lt;strong&gt;DrvSaveScreenBits&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556278)"><strong>DrvSaveScreenBits</strong></a></p></td>
<td align="left"><p>将保存或还原指定的矩形的屏幕。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556285" data-raw-source="[&lt;strong&gt;DrvSetPixelFormat&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556285)"><strong>DrvSetPixelFormat</strong></a></p></td>
<td align="left"><p>设置窗口的像素格式。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556289" data-raw-source="[&lt;strong&gt;DrvSetPointerShape&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556289)"><strong>DrvSetPointerShape</strong></a></p></td>
<td align="left"><p>如果该驱动程序已书写，，然后设置新的指针形状，请从屏幕中删除指针。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idddkmiscellaneousfunctionsggspanspan-idddkmiscellaneousfunctionsggspanmiscellaneous-functions"></a><span id="ddk_miscellaneous_functions_gg"></span><span id="DDK_MISCELLANEOUS_FUNCTIONS_GG"></span>杂项函数

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556192" data-raw-source="[&lt;strong&gt;DrvDestroyFont&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556192)"><strong>DrvDestroyFont</strong></a></p></td>
<td align="left"><p>通知驱动程序，但不再需要字体实现;驱动程序可以释放已分配的数据结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556203" data-raw-source="[&lt;strong&gt;DrvDrawEscape&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556203)"><strong>DrvDrawEscape</strong></a></p></td>
<td align="left"><p>实现绘图类型转义函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556217" data-raw-source="[&lt;strong&gt;DrvEscape&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556217)"><strong>DrvEscape</strong></a></p></td>
<td align="left"><p>查询中独立于设备的图形 DDI 中不可用的设备的信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556226" data-raw-source="[&lt;strong&gt;DrvFree&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556226)"><strong>DrvFree</strong></a></p></td>
<td align="left"><p>释放与所指示的数据结构相关联的存储。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556252" data-raw-source="[&lt;strong&gt;DrvNotify&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556252)"><strong>DrvNotify</strong></a></p></td>
<td align="left"><p>使显示驱动程序要将通知通过 GDI 的某些信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556323" data-raw-source="[&lt;strong&gt;DrvSynchronize&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556323)"><strong>DrvSynchronize</strong></a></p></td>
<td align="left"><p>坐标之间 GDI 和显示驱动程序支持协处理器设备; 绘图操作有关<a href="https://msdn.microsoft.com/library/windows/hardware/ff556279#wdkgloss-engine-managed-surface" data-raw-source="&lt;em&gt;engine-managed surfaces&lt;/em&gt;"><em>引擎管理面</em></a>仅。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff557273" data-raw-source="[&lt;strong&gt;DrvSynchronizeSurface&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557273)"><strong>DrvSynchronizeSurface</strong></a></p></td>
<td align="left"><p>允许执行的设备的协处理器要协调用 GDI 绘制操作。</p></td>
</tr>
</tbody>
</table>

 

显示器驱动程序可以选择性地实现 Microsoft DirectDraw 和/或 Direct3D 接口。 请参阅以下各节，有关详细信息：

[DirectDraw](directdraw.md)

[Direct3D DDI](direct3d.md)

所有图形驱动程序的可选函数的列表将显示在[图形驱动程序的可选函数](optional-graphics-driver-functions.md)。

 

 






---
title: GDI 绘图和相关服务
description: GDI 绘图和相关服务
ms.assetid: b5df84ae-05cf-49dc-aa49-79f912ecd029
keywords:
- GDI WDK Windows 2000 显示，绘图服务
- 图形驱动程序 WDK Windows 2000 显示，绘图服务
- 绘制 WDK GDI，支持的绘图服务
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 482d254442605effc92402696ea80fb1c3a2cc75
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065842"
---
# <a name="gdi-drawing-and-related-services"></a>GDI 绘图和相关服务


## <span id="ddk_gdi_drawing_and_related_services_gg"></span><span id="DDK_GDI_DRAWING_AND_RELATED_SERVICES_GG"></span>


为了支持 [**CLIPOBJ**](/windows/desktop/api/winddi/ns-winddi-_clipobj)、 [**BRUSHOBJ**](/windows/desktop/api/winddi/ns-winddi-_brushobj)和 [**XFORMOBJ**](/previous-versions/windows/hardware/drivers/ff570618(v=vs.85)) 结构，GDI 提供了几个在下表中列出的绘图服务。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">GDI 绘图服务函数</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-brushobj_hgetcolortransform" data-raw-source="[&lt;strong&gt;BRUSHOBJ_hGetColorTransform&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-brushobj_hgetcolortransform)"><strong>BRUSHOBJ_hGetColorTransform</strong></a></p></td>
<td align="left"><p>检索指定画笔的颜色转换。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-brushobj_pvallocrbrush" data-raw-source="[&lt;strong&gt;BRUSHOBJ_pvAllocRbrush&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-brushobj_pvallocrbrush)"><strong>BRUSHOBJ_pvAllocRbrush</strong></a></p></td>
<td align="left"><p>为驱动程序的画笔实现分配内存。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-brushobj_pvgetrbrush" data-raw-source="[&lt;strong&gt;BRUSHOBJ_pvGetRbrush&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-brushobj_pvgetrbrush)"><strong>BRUSHOBJ_pvGetRbrush</strong></a></p></td>
<td align="left"><p>返回一个指针，该指针指向驱动程序实现的画笔。 如果尚未实现画笔，则实现它。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-brushobj_ulgetbrushcolor" data-raw-source="[&lt;strong&gt;BRUSHOBJ_ulGetBrushColor&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-brushobj_ulgetbrushcolor)"><strong>BRUSHOBJ_ulGetBrushColor</strong></a></p></td>
<td align="left"><p>返回指定的纯色画笔的 RGB 颜色。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-clipobj_benum" data-raw-source="[&lt;strong&gt;CLIPOBJ_bEnum&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-clipobj_benum)"><strong>CLIPOBJ_bEnum</strong></a></p></td>
<td align="left"><p>从剪辑区域检索一批矩形。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-clipobj_cenumstart" data-raw-source="[&lt;strong&gt;CLIPOBJ_cEnumStart&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-clipobj_cenumstart)"><strong>CLIPOBJ_cEnumStart</strong></a></p></td>
<td align="left"><p>设置所有或部分剪裁区域中矩形的枚举参数。  (可以在不调用此函数的情况下枚举区域，但后续枚举需要此函数的使用) 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-clipobj_ppogetpath" data-raw-source="[&lt;strong&gt;CLIPOBJ_ppoGetPath&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-clipobj_ppogetpath)"><strong>CLIPOBJ_ppoGetPath</strong></a></p></td>
<td align="left"><p>用于检索作为路径的复杂区域。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engalphablend" data-raw-source="[&lt;strong&gt;EngAlphaBlend&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-engalphablend)"><strong>EngAlphaBlend</strong></a></p></td>
<td align="left"><p>提供带 <a href="https://docs.microsoft.com/windows-hardware/drivers/#wdkgloss-alpha-blending" data-raw-source="&lt;em&gt;alpha blending&lt;/em&gt;"><em>alpha 混合</em></a>的位块传输功能。 这是 <a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvalphablend" data-raw-source="[&lt;strong&gt;DrvAlphaBlend&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvalphablend)"><strong>DrvAlphaBlend</strong></a> 函数的 GDI 模拟。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engbitblt" data-raw-source="[&lt;strong&gt;EngBitBlt&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-engbitblt)"><strong>EngBitBlt</strong></a></p></td>
<td align="left"><p>在 <a href="https://docs.microsoft.com/windows-hardware/drivers/#wdkgloss-device-managed-surface" data-raw-source="&lt;em&gt;device-managed surfaces&lt;/em&gt;"><em>设备管理</em></a>的图面之间，或在设备管理的表面与 GDI 托管的标准格式位图之间提供一般的位块传输功能。 这是 <a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvbitblt" data-raw-source="[&lt;strong&gt;DrvBitBlt&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvbitblt)"><strong>DrvBitBlt</strong></a> 函数的 GDI 模拟。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcontrolsprites" data-raw-source="[&lt;strong&gt;EngControlSprites&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-engcontrolsprites)"><strong>EngControlSprites</strong></a></p></td>
<td align="left"><p>泪水在指定的 WNDOBJ 区域上向下或重新绘制子画面。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcopybits" data-raw-source="[&lt;strong&gt;EngCopyBits&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-engcopybits)"><strong>EngCopyBits</strong></a></p></td>
<td align="left"><p>转换设备托管的光栅图面和 GDI 标准格式的位图。 这是 <a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvcopybits" data-raw-source="[&lt;strong&gt;DrvCopyBits&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvcopybits)"><strong>DrvCopyBits</strong></a> 函数的 GDI 模拟。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreateclip" data-raw-source="[&lt;strong&gt;EngCreateClip&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-engcreateclip)"><strong>EngCreateClip</strong></a></p></td>
<td align="left"><p>为驱动程序的临时使用分配 <a href="https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_clipobj" data-raw-source="[&lt;strong&gt;CLIPOBJ&lt;/strong&gt;](/windows/desktop/api/winddi/ns-winddi-_clipobj)"><strong>CLIPOBJ</strong></a> 。 当不再需要驱动程序时，驱动程序应调用 <a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engdeleteclip" data-raw-source="[&lt;strong&gt;EngDeleteClip&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-engdeleteclip)"><strong>EngDeleteClip</strong></a> 函数将其删除。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engdeleteclip" data-raw-source="[&lt;strong&gt;EngDeleteClip&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-engdeleteclip)"><strong>EngDeleteClip</strong></a></p></td>
<td align="left"><p>删除使用 <a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreateclip" data-raw-source="[&lt;strong&gt;EngCreateClip&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-engcreateclip)"><strong>EngCreateClip</strong></a> 函数分配的 CLIPOBJ。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engdeviceiocontrol" data-raw-source="[&lt;strong&gt;EngDeviceIoControl&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-engdeviceiocontrol)"><strong>EngDeviceIoControl</strong></a></p></td>
<td align="left"><p>将控制代码发送到指定的视频微型端口驱动程序，导致设备执行指定的操作。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engfillpath" data-raw-source="[&lt;strong&gt;EngFillPath&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-engfillpath)"><strong>EngFillPath</strong></a></p></td>
<td align="left"><p>填充 (绘制) 指定的路径。 这是 <a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvfillpath" data-raw-source="[&lt;strong&gt;DrvFillPath&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvfillpath)"><strong>DrvFillPath</strong></a> 函数的 GDI 模拟。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-enggradientfill" data-raw-source="[&lt;strong&gt;EngGradientFill&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-enggradientfill)"><strong>EngGradientFill</strong></a></p></td>
<td align="left"><p>对指定的图形基元进行底纹。 这是 <a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvgradientfill" data-raw-source="[&lt;strong&gt;DrvGradientFill&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvgradientfill)"><strong>DrvGradientFill</strong></a> 函数的 GDI 模拟。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-englineto" data-raw-source="[&lt;strong&gt;EngLineTo&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-englineto)"><strong>EngLineTo</strong></a></p></td>
<td align="left"><p>绘制单个纯纯整数修饰线。 这是 <a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvlineto" data-raw-source="[&lt;strong&gt;DrvLineTo&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvlineto)"><strong>DrvLineTo</strong></a> 函数的 GDI 模拟。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engmovepointer" data-raw-source="[&lt;strong&gt;EngMovePointer&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-engmovepointer)"><strong>EngMovePointer</strong></a></p></td>
<td align="left"><p>在设备上移动引擎托管指针。 这是 <a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvmovepointer" data-raw-source="[&lt;strong&gt;DrvMovePointer&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvmovepointer)"><strong>DrvMovePointer</strong></a> 函数的 GDI 模拟。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engpaint" data-raw-source="[&lt;strong&gt;EngPaint&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-engpaint)"><strong>EngPaint</strong></a></p></td>
<td align="left"><p>绘制指定的区域。 这是已过时的 <a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvpaint" data-raw-source="[&lt;strong&gt;DrvPaint&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvpaint)"><strong>DrvPaint</strong></a> 函数的 GDI 模拟。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engplgblt" data-raw-source="[&lt;strong&gt;EngPlgBlt&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-engplgblt)"><strong>EngPlgBlt</strong></a></p></td>
<td align="left"><p>执行旋转位块传输。 这是 <a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvplgblt" data-raw-source="[&lt;strong&gt;DrvPlgBlt&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvplgblt)"><strong>DrvPlgBlt</strong></a> 函数的 GDI 模拟。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engsetpointershape" data-raw-source="[&lt;strong&gt;EngSetPointerShape&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-engsetpointershape)"><strong>EngSetPointerShape</strong></a></p></td>
<td align="left"><p>设置指针的形状。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engsetpointertag" data-raw-source="[&lt;strong&gt;EngSetPointerTag&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-engsetpointertag)"><strong>EngSetPointerTag</strong></a></p></td>
<td align="left"><p>创建一个与镜像系统中其他关联驱动程序的 <a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsetpointershape" data-raw-source="[&lt;strong&gt;DrvSetPointerShape&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvsetpointershape)"><strong>DrvSetPointerShape</strong></a> 调用上的应用程序指针形状运算的形状。</p>
<div>
 
</div>
此功能在 Windows 2000 和更高版本中已过时。</td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engstretchblt" data-raw-source="[&lt;strong&gt;EngStretchBlt&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-engstretchblt)"><strong>EngStretchBlt</strong></a></p></td>
<td align="left"><p>执行拉伸位块传输。 这是 <a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstretchblt" data-raw-source="[&lt;strong&gt;DrvStretchBlt&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvstretchblt)"><strong>DrvStretchBlt</strong></a> 函数的 GDI 模拟。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engstretchbltrop" data-raw-source="[&lt;strong&gt;EngStretchBltROP&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-engstretchbltrop)"><strong>EngStretchBltROP</strong></a></p></td>
<td align="left"><p>使用 <a href="https://docs.microsoft.com/windows-hardware/drivers/#wdkgloss-raster-operation--rop-" data-raw-source="&lt;em&gt;ROP&lt;/em&gt;"><em>ROP</em></a>执行拉伸位块传输。 这是 <a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstretchbltrop" data-raw-source="[&lt;strong&gt;DrvStretchBltROP&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvstretchbltrop)"><strong>DrvStretchBltROP</strong></a> 函数的 GDI 模拟。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engstrokeandfillpath" data-raw-source="[&lt;strong&gt;EngStrokeAndFillPath&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-engstrokeandfillpath)"><strong>EngStrokeAndFillPath</strong></a></p></td>
<td align="left"><p>笔划 (绘制路径) 并同时填充该路径。 这是 <a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstrokeandfillpath" data-raw-source="[&lt;strong&gt;DrvStrokeAndFillPath&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvstrokeandfillpath)"><strong>DrvStrokeAndFillPath</strong></a> 函数的 GDI 模拟。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engstrokepath" data-raw-source="[&lt;strong&gt;EngStrokePath&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-engstrokepath)"><strong>EngStrokePath</strong></a></p></td>
<td align="left"><p>笔划 (绘制) 路径。 这是 <a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstrokepath" data-raw-source="[&lt;strong&gt;DrvStrokePath&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvstrokepath)"><strong>DrvStrokePath</strong></a> 函数的 GDI 模拟。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engtransparentblt" data-raw-source="[&lt;strong&gt;EngTransparentBlt&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-engtransparentblt)"><strong>EngTransparentBlt</strong></a></p></td>
<td align="left"><p>执行透明的 blt。 这是 <a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtransparentblt" data-raw-source="[&lt;strong&gt;DrvTransparentBlt&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvtransparentblt)"><strong>DrvTransparentBlt</strong></a> 函数的 GDI 模拟。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-xformobj_bapplyxform" data-raw-source="[&lt;strong&gt;XFORMOBJ_bApplyXform&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-xformobj_bapplyxform)"><strong>XFORMOBJ_bApplyXform</strong></a></p></td>
<td align="left"><p>将给定的转换或反转到给定的点数组。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-xformobj_igetfloatobjxform" data-raw-source="[&lt;strong&gt;XFORMOBJ_iGetFloatObjXform&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-xformobj_igetfloatobjxform)"><strong>XFORMOBJ_iGetFloatObjXform</strong></a></p></td>
<td align="left"><p>将 FLOATOBJ 转换下载到驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-xformobj_igetxform" data-raw-source="[&lt;strong&gt;XFORMOBJ_iGetXform&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-xformobj_igetxform)"><strong>XFORMOBJ_iGetXform</strong></a></p></td>
<td align="left"><p>下载对驱动程序的转换。</p></td>
</tr>
</tbody>
</table>

 

 


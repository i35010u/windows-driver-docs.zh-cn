---
title: GDI 绘图和相关服务
description: GDI 绘图和相关服务
ms.assetid: b5df84ae-05cf-49dc-aa49-79f912ecd029
keywords:
- GDI WDK Windows 2000 显示，绘制服务
- 显示图形驱动程序 WDK Windows 2000，绘制服务
- 绘制 WDK GDI，绘制支持的服务
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15c8f5cfab2b7d971e7fcf70da986c6883cbbba3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379486"
---
# <a name="gdi-drawing-and-related-services"></a>GDI 绘图和相关服务


## <span id="ddk_gdi_drawing_and_related_services_gg"></span><span id="DDK_GDI_DRAWING_AND_RELATED_SERVICES_GG"></span>


若要支持[ **CLIPOBJ**](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_clipobj)， [ **BRUSHOBJ**](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_brushobj)，并[ **XFORMOBJ** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff570618(v=vs.85))结构，GDI 提供了多个绘图的服务下, 表中列出。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">GDI 绘图服务函数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-brushobj_hgetcolortransform" data-raw-source="[&lt;strong&gt;BRUSHOBJ_hGetColorTransform&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-brushobj_hgetcolortransform)"><strong>BRUSHOBJ_hGetColorTransform</strong></a></p></td>
<td align="left"><p>检索指定画笔的颜色转换。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-brushobj_pvallocrbrush" data-raw-source="[&lt;strong&gt;BRUSHOBJ_pvAllocRbrush&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-brushobj_pvallocrbrush)"><strong>BRUSHOBJ_pvAllocRbrush</strong></a></p></td>
<td align="left"><p>画笔的驱动程序的实现，为分配内存。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-brushobj_pvgetrbrush" data-raw-source="[&lt;strong&gt;BRUSHOBJ_pvGetRbrush&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-brushobj_pvgetrbrush)"><strong>BRUSHOBJ_pvGetRbrush</strong></a></p></td>
<td align="left"><p>返回一个指向的画笔的驱动程序的实现。 如果它的未尚未实现，认识到画笔。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-brushobj_ulgetbrushcolor" data-raw-source="[&lt;strong&gt;BRUSHOBJ_ulGetBrushColor&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-brushobj_ulgetbrushcolor)"><strong>BRUSHOBJ_ulGetBrushColor</strong></a></p></td>
<td align="left"><p>返回指定实心画笔的 RGB 颜色。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-clipobj_benum" data-raw-source="[&lt;strong&gt;CLIPOBJ_bEnum&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-clipobj_benum)"><strong>CLIPOBJ_bEnum</strong></a></p></td>
<td align="left"><p>从剪辑区域中检索一批的矩形。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-clipobj_cenumstart" data-raw-source="[&lt;strong&gt;CLIPOBJ_cEnumStart&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-clipobj_cenumstart)"><strong>CLIPOBJ_cEnumStart</strong></a></p></td>
<td align="left"><p>为枚举的矩形中所有或部分剪辑区域设置参数。 （而不会调用此函数中，可以一次枚举该区域，但后续枚举需要此函数，请使用）。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-clipobj_ppogetpath" data-raw-source="[&lt;strong&gt;CLIPOBJ_ppoGetPath&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-clipobj_ppogetpath)"><strong>CLIPOBJ_ppoGetPath</strong></a></p></td>
<td align="left"><p>用于检索作为路径的复杂的区域。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engalphablend" data-raw-source="[&lt;strong&gt;EngAlphaBlend&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engalphablend)"><strong>EngAlphaBlend</strong></a></p></td>
<td align="left"><p>提供功能的位块传输<a href="https://docs.microsoft.com/windows-hardware/drivers/#wdkgloss-alpha-blending" data-raw-source="&lt;em&gt;alpha blending&lt;/em&gt;"> <em>alpha 值混合处理</em></a>。 这是 GDI 模拟<a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvalphablend" data-raw-source="[&lt;strong&gt;DrvAlphaBlend&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvalphablend)"> <strong>DrvAlphaBlend</strong> </a>函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engbitblt" data-raw-source="[&lt;strong&gt;EngBitBlt&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engbitblt)"><strong>EngBitBlt</strong></a></p></td>
<td align="left"><p>提供常规位块传输功能要么之间<a href="https://docs.microsoft.com/windows-hardware/drivers/#wdkgloss-device-managed-surface" data-raw-source="&lt;em&gt;device-managed surfaces&lt;/em&gt;"><em>设备管理面</em></a>，之间或设备管理面和 GDI 托管标准格式位图。 这是 GDI 模拟<a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvbitblt" data-raw-source="[&lt;strong&gt;DrvBitBlt&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvbitblt)"> <strong>DrvBitBlt</strong> </a>函数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcontrolsprites" data-raw-source="[&lt;strong&gt;EngControlSprites&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcontrolsprites)"><strong>EngControlSprites</strong></a></p></td>
<td align="left"><p>关闭或重新指定 WNDOBJ 区域上绘制 sprite。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcopybits" data-raw-source="[&lt;strong&gt;EngCopyBits&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcopybits)"><strong>EngCopyBits</strong></a></p></td>
<td align="left"><p>设备管理光栅图面和 GDI 标准格式位图之间进行转换。 这是 GDI 模拟<a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvcopybits" data-raw-source="[&lt;strong&gt;DrvCopyBits&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvcopybits)"> <strong>DrvCopyBits</strong> </a>函数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreateclip" data-raw-source="[&lt;strong&gt;EngCreateClip&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreateclip)"><strong>EngCreateClip</strong></a></p></td>
<td align="left"><p>分配<a href="https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_clipobj" data-raw-source="[&lt;strong&gt;CLIPOBJ&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_clipobj)"> <strong>CLIPOBJ</strong> </a>驱动程序的临时使用。 该驱动程序应调用<a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engdeleteclip" data-raw-source="[&lt;strong&gt;EngDeleteClip&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engdeleteclip)"> <strong>EngDeleteClip</strong> </a>函数不再需要时将其删除。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engdeleteclip" data-raw-source="[&lt;strong&gt;EngDeleteClip&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engdeleteclip)"><strong>EngDeleteClip</strong></a></p></td>
<td align="left"><p>删除与分配 CLIPOBJ <a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreateclip" data-raw-source="[&lt;strong&gt;EngCreateClip&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreateclip)"> <strong>EngCreateClip</strong> </a>函数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engdeviceiocontrol" data-raw-source="[&lt;strong&gt;EngDeviceIoControl&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engdeviceiocontrol)"><strong>EngDeviceIoControl</strong></a></p></td>
<td align="left"><p>将控制代码发送到指定视频的微型端口驱动程序，从而导致设备执行指定的操作。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engfillpath" data-raw-source="[&lt;strong&gt;EngFillPath&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engfillpath)"><strong>EngFillPath</strong></a></p></td>
<td align="left"><p>填充 （绘制） 指定的路径。 这是 GDI 模拟<a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvfillpath" data-raw-source="[&lt;strong&gt;DrvFillPath&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvfillpath)"> <strong>DrvFillPath</strong> </a>函数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-enggradientfill" data-raw-source="[&lt;strong&gt;EngGradientFill&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-enggradientfill)"><strong>EngGradientFill</strong></a></p></td>
<td align="left"><p>底纹应用指定的图形基元。 这是 GDI 模拟<a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvgradientfill" data-raw-source="[&lt;strong&gt;DrvGradientFill&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvgradientfill)"> <strong>DrvGradientFill</strong> </a>函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-englineto" data-raw-source="[&lt;strong&gt;EngLineTo&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-englineto)"><strong>EngLineTo</strong></a></p></td>
<td align="left"><p>绘制单个、 solid、 仅限整数的修饰的行。 这是 GDI 模拟<a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvlineto" data-raw-source="[&lt;strong&gt;DrvLineTo&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvlineto)"> <strong>DrvLineTo</strong> </a>函数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engmovepointer" data-raw-source="[&lt;strong&gt;EngMovePointer&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engmovepointer)"><strong>EngMovePointer</strong></a></p></td>
<td align="left"><p>将移动设备上的引擎托管指针。 这是 GDI 模拟<a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvmovepointer" data-raw-source="[&lt;strong&gt;DrvMovePointer&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvmovepointer)"> <strong>DrvMovePointer</strong> </a>函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engpaint" data-raw-source="[&lt;strong&gt;EngPaint&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engpaint)"><strong>EngPaint</strong></a></p></td>
<td align="left"><p>绘制指定的区域。 这是为已过时的 GDI 模拟<a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvpaint" data-raw-source="[&lt;strong&gt;DrvPaint&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvpaint)"> <strong>DrvPaint</strong> </a>函数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engplgblt" data-raw-source="[&lt;strong&gt;EngPlgBlt&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engplgblt)"><strong>EngPlgBlt</strong></a></p></td>
<td align="left"><p>执行旋转的位块传输。 这是 GDI 模拟<a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvplgblt" data-raw-source="[&lt;strong&gt;DrvPlgBlt&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvplgblt)"> <strong>DrvPlgBlt</strong> </a>函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engsetpointershape" data-raw-source="[&lt;strong&gt;EngSetPointerShape&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engsetpointershape)"><strong>EngSetPointerShape</strong></a></p></td>
<td align="left"><p>设置指针的形状。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engsetpointertag" data-raw-source="[&lt;strong&gt;EngSetPointerTag&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engsetpointertag)"><strong>EngSetPointerTag</strong></a></p></td>
<td align="left"><p>创建与应用程序的指针形状是或运算, 一个形状<a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsetpointershape" data-raw-source="[&lt;strong&gt;DrvSetPointerShape&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsetpointershape)"> <strong>DrvSetPointerShape</strong> </a>调用其他镜像系统中关联的驱动程序。</p>
<div>
 
</div>
此函数是过时的 Windows 2000 及更高版本。</td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engstretchblt" data-raw-source="[&lt;strong&gt;EngStretchBlt&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engstretchblt)"><strong>EngStretchBlt</strong></a></p></td>
<td align="left"><p>执行延伸位块传输。 这是 GDI 模拟<a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstretchblt" data-raw-source="[&lt;strong&gt;DrvStretchBlt&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstretchblt)"> <strong>DrvStretchBlt</strong> </a>函数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engstretchbltrop" data-raw-source="[&lt;strong&gt;EngStretchBltROP&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engstretchbltrop)"><strong>EngStretchBltROP</strong></a></p></td>
<td align="left"><p>执行使用延伸位块传输<a href="https://docs.microsoft.com/windows-hardware/drivers/#wdkgloss-raster-operation--rop-" data-raw-source="&lt;em&gt;ROP&lt;/em&gt;"> <em>ROP</em></a>。 这是 GDI 模拟<a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstretchbltrop" data-raw-source="[&lt;strong&gt;DrvStretchBltROP&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstretchbltrop)"> <strong>DrvStretchBltROP</strong> </a>函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engstrokeandfillpath" data-raw-source="[&lt;strong&gt;EngStrokeAndFillPath&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engstrokeandfillpath)"><strong>EngStrokeAndFillPath</strong></a></p></td>
<td align="left"><p>笔画 （绘制） 路径，并在同一时间进行填充。 这是 GDI 模拟<a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstrokeandfillpath" data-raw-source="[&lt;strong&gt;DrvStrokeAndFillPath&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstrokeandfillpath)"> <strong>DrvStrokeAndFillPath</strong> </a>函数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engstrokepath" data-raw-source="[&lt;strong&gt;EngStrokePath&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engstrokepath)"><strong>EngStrokePath</strong></a></p></td>
<td align="left"><p>笔画 （绘制） 路径。 这是 GDI 模拟<a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstrokepath" data-raw-source="[&lt;strong&gt;DrvStrokePath&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstrokepath)"> <strong>DrvStrokePath</strong> </a>函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engtransparentblt" data-raw-source="[&lt;strong&gt;EngTransparentBlt&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engtransparentblt)"><strong>EngTransparentBlt</strong></a></p></td>
<td align="left"><p>执行透明 blt。 这是 GDI 模拟<a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtransparentblt" data-raw-source="[&lt;strong&gt;DrvTransparentBlt&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtransparentblt)"> <strong>DrvTransparentBlt</strong> </a>函数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-xformobj_bapplyxform" data-raw-source="[&lt;strong&gt;XFORMOBJ_bApplyXform&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-xformobj_bapplyxform)"><strong>XFORMOBJ_bApplyXform</strong></a></p></td>
<td align="left"><p>将给定的转换或及其反转应用于给定的点数组。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-xformobj_igetfloatobjxform" data-raw-source="[&lt;strong&gt;XFORMOBJ_iGetFloatObjXform&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-xformobj_igetfloatobjxform)"><strong>XFORMOBJ_iGetFloatObjXform</strong></a></p></td>
<td align="left"><p>下载 FLOATOBJ 转换到驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-xformobj_igetxform" data-raw-source="[&lt;strong&gt;XFORMOBJ_iGetXform&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-xformobj_igetxform)"><strong>XFORMOBJ_iGetXform</strong></a></p></td>
<td align="left"><p>下载一个转换，转换到驱动程序。</p></td>
</tr>
</tbody>
</table>

 

 

 






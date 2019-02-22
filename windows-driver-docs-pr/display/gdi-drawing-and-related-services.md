---
title: GDI 绘图和相关的服务
description: GDI 绘图和相关的服务
ms.assetid: b5df84ae-05cf-49dc-aa49-79f912ecd029
keywords:
- GDI WDK Windows 2000 显示，绘制服务
- 显示图形驱动程序 WDK Windows 2000，绘制服务
- 绘制 WDK GDI，绘制支持的服务
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a99ff67b3900fa6d7f384462fe8c7262f8e9240f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519665"
---
# <a name="gdi-drawing-and-related-services"></a>GDI 绘图和相关的服务


## <span id="ddk_gdi_drawing_and_related_services_gg"></span><span id="DDK_GDI_DRAWING_AND_RELATED_SERVICES_GG"></span>


若要支持[ **CLIPOBJ**](https://msdn.microsoft.com/library/windows/hardware/ff539417)， [ **BRUSHOBJ**](https://msdn.microsoft.com/library/windows/hardware/ff538261)，并[ **XFORMOBJ** ](https://msdn.microsoft.com/library/windows/hardware/ff570618)结构，GDI 提供了多个绘图的服务下, 表中列出。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff538262" data-raw-source="[&lt;strong&gt;BRUSHOBJ_hGetColorTransform&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff538262)"><strong>BRUSHOBJ_hGetColorTransform</strong></a></p></td>
<td align="left"><p>检索指定画笔的颜色转换。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff538263" data-raw-source="[&lt;strong&gt;BRUSHOBJ_pvAllocRbrush&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff538263)"><strong>BRUSHOBJ_pvAllocRbrush</strong></a></p></td>
<td align="left"><p>为驱动程序分配内存&#39;s 实现的画笔。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff538264" data-raw-source="[&lt;strong&gt;BRUSHOBJ_pvGetRbrush&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff538264)"><strong>BRUSHOBJ_pvGetRbrush</strong></a></p></td>
<td align="left"><p>返回一个指向该驱动程序&#39;s 实现的画笔。 如果它的未尚未实现，认识到画笔。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff538265" data-raw-source="[&lt;strong&gt;BRUSHOBJ_ulGetBrushColor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff538265)"><strong>BRUSHOBJ_ulGetBrushColor</strong></a></p></td>
<td align="left"><p>返回指定实心画笔的 RGB 颜色。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff539420" data-raw-source="[&lt;strong&gt;CLIPOBJ_bEnum&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff539420)"><strong>CLIPOBJ_bEnum</strong></a></p></td>
<td align="left"><p>从剪辑区域中检索一批的矩形。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff539421" data-raw-source="[&lt;strong&gt;CLIPOBJ_cEnumStart&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff539421)"><strong>CLIPOBJ_cEnumStart</strong></a></p></td>
<td align="left"><p>为枚举的矩形中所有或部分剪辑区域设置参数。 (而不会调用此函数中，可以一次枚举该区域，但后续枚举需要此函数&#39;使用)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff539423" data-raw-source="[&lt;strong&gt;CLIPOBJ_ppoGetPath&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff539423)"><strong>CLIPOBJ_ppoGetPath</strong></a></p></td>
<td align="left"><p>用于检索作为路径的复杂的区域。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564182" data-raw-source="[&lt;strong&gt;EngAlphaBlend&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564182)"><strong>EngAlphaBlend</strong></a></p></td>
<td align="left"><p>提供功能的位块传输<a href="https://msdn.microsoft.com/library/windows/hardware/ff556270#wdkgloss-alpha-blending" data-raw-source="&lt;em&gt;alpha blending&lt;/em&gt;"> <em>alpha 值混合处理</em></a>。 这是 GDI 模拟<a href="https://msdn.microsoft.com/library/windows/hardware/ff556176" data-raw-source="[&lt;strong&gt;DrvAlphaBlend&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556176)"> <strong>DrvAlphaBlend</strong> </a>函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564185" data-raw-source="[&lt;strong&gt;EngBitBlt&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564185)"><strong>EngBitBlt</strong></a></p></td>
<td align="left"><p>提供常规位块传输功能要么之间<a href="https://msdn.microsoft.com/library/windows/hardware/ff556277#wdkgloss-device-managed-surface" data-raw-source="&lt;em&gt;device-managed surfaces&lt;/em&gt;"><em>设备管理面</em></a>，之间或设备管理面和 GDI 托管标准格式位图。 这是 GDI 模拟<a href="https://msdn.microsoft.com/library/windows/hardware/ff556180" data-raw-source="[&lt;strong&gt;DrvBitBlt&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556180)"> <strong>DrvBitBlt</strong> </a>函数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564193" data-raw-source="[&lt;strong&gt;EngControlSprites&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564193)"><strong>EngControlSprites</strong></a></p></td>
<td align="left"><p>关闭或重新指定 WNDOBJ 区域上绘制 sprite。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564196" data-raw-source="[&lt;strong&gt;EngCopyBits&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564196)"><strong>EngCopyBits</strong></a></p></td>
<td align="left"><p>设备管理光栅图面和 GDI 标准格式位图之间进行转换。 这是 GDI 模拟<a href="https://msdn.microsoft.com/library/windows/hardware/ff556182" data-raw-source="[&lt;strong&gt;DrvCopyBits&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556182)"> <strong>DrvCopyBits</strong> </a>函数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564202" data-raw-source="[&lt;strong&gt;EngCreateClip&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564202)"><strong>EngCreateClip</strong></a></p></td>
<td align="left"><p>分配<a href="https://msdn.microsoft.com/library/windows/hardware/ff539417" data-raw-source="[&lt;strong&gt;CLIPOBJ&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff539417)"> <strong>CLIPOBJ</strong> </a>驱动程序的&#39;s 临时使用。 该驱动程序应调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff564786" data-raw-source="[&lt;strong&gt;EngDeleteClip&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564786)"> <strong>EngDeleteClip</strong> </a>函数不再需要时将其删除。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564786" data-raw-source="[&lt;strong&gt;EngDeleteClip&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564786)"><strong>EngDeleteClip</strong></a></p></td>
<td align="left"><p>删除与分配 CLIPOBJ <a href="https://msdn.microsoft.com/library/windows/hardware/ff564202" data-raw-source="[&lt;strong&gt;EngCreateClip&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564202)"> <strong>EngCreateClip</strong> </a>函数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564838" data-raw-source="[&lt;strong&gt;EngDeviceIoControl&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564838)"><strong>EngDeviceIoControl</strong></a></p></td>
<td align="left"><p>将控制代码发送到指定视频的微型端口驱动程序，从而导致设备执行指定的操作。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564860" data-raw-source="[&lt;strong&gt;EngFillPath&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564860)"><strong>EngFillPath</strong></a></p></td>
<td align="left"><p>填充 （绘制） 指定的路径。 这是 GDI 模拟<a href="https://msdn.microsoft.com/library/windows/hardware/ff556220" data-raw-source="[&lt;strong&gt;DrvFillPath&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556220)"> <strong>DrvFillPath</strong> </a>函数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564957" data-raw-source="[&lt;strong&gt;EngGradientFill&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564957)"><strong>EngGradientFill</strong></a></p></td>
<td align="left"><p>底纹应用指定的图形基元。 这是 GDI 模拟<a href="https://msdn.microsoft.com/library/windows/hardware/ff556236" data-raw-source="[&lt;strong&gt;DrvGradientFill&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556236)"> <strong>DrvGradientFill</strong> </a>函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564962" data-raw-source="[&lt;strong&gt;EngLineTo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564962)"><strong>EngLineTo</strong></a></p></td>
<td align="left"><p>绘制单个、 solid、 仅限整数的修饰的行。 这是 GDI 模拟<a href="https://msdn.microsoft.com/library/windows/hardware/ff556245" data-raw-source="[&lt;strong&gt;DrvLineTo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556245)"> <strong>DrvLineTo</strong> </a>函数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564977" data-raw-source="[&lt;strong&gt;EngMovePointer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564977)"><strong>EngMovePointer</strong></a></p></td>
<td align="left"><p>将移动设备上的引擎托管指针。 这是 GDI 模拟<a href="https://msdn.microsoft.com/library/windows/hardware/ff556248" data-raw-source="[&lt;strong&gt;DrvMovePointer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556248)"> <strong>DrvMovePointer</strong> </a>函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564981" data-raw-source="[&lt;strong&gt;EngPaint&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564981)"><strong>EngPaint</strong></a></p></td>
<td align="left"><p>绘制指定的区域。 这是为已过时的 GDI 模拟<a href="https://msdn.microsoft.com/library/windows/hardware/ff556256" data-raw-source="[&lt;strong&gt;DrvPaint&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556256)"> <strong>DrvPaint</strong> </a>函数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564982" data-raw-source="[&lt;strong&gt;EngPlgBlt&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564982)"><strong>EngPlgBlt</strong></a></p></td>
<td align="left"><p>执行旋转的位块传输。 这是 GDI 模拟<a href="https://msdn.microsoft.com/library/windows/hardware/ff556258" data-raw-source="[&lt;strong&gt;DrvPlgBlt&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556258)"> <strong>DrvPlgBlt</strong> </a>函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565017" data-raw-source="[&lt;strong&gt;EngSetPointerShape&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565017)"><strong>EngSetPointerShape</strong></a></p></td>
<td align="left"><p>设置指针的形状。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565018" data-raw-source="[&lt;strong&gt;EngSetPointerTag&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565018)"><strong>EngSetPointerTag</strong></a></p></td>
<td align="left"><p>创建与应用程序是或运算的形状&#39;上的 s 指针形状<a href="https://msdn.microsoft.com/library/windows/hardware/ff556289" data-raw-source="[&lt;strong&gt;DrvSetPointerShape&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556289)"> <strong>DrvSetPointerShape</strong> </a>调用其他镜像系统中关联的驱动程序。</p>
<div>
 
</div>
此函数是过时的 Windows 2000 及更高版本。</td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565025" data-raw-source="[&lt;strong&gt;EngStretchBlt&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565025)"><strong>EngStretchBlt</strong></a></p></td>
<td align="left"><p>执行延伸位块传输。 这是 GDI 模拟<a href="https://msdn.microsoft.com/library/windows/hardware/ff556302" data-raw-source="[&lt;strong&gt;DrvStretchBlt&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556302)"> <strong>DrvStretchBlt</strong> </a>函数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565027" data-raw-source="[&lt;strong&gt;EngStretchBltROP&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565027)"><strong>EngStretchBltROP</strong></a></p></td>
<td align="left"><p>执行使用延伸位块传输<a href="https://msdn.microsoft.com/library/windows/hardware/ff556331#wdkgloss-raster-operation--rop-" data-raw-source="&lt;em&gt;ROP&lt;/em&gt;"> <em>ROP</em></a>。 这是 GDI 模拟<a href="https://msdn.microsoft.com/library/windows/hardware/ff556306" data-raw-source="[&lt;strong&gt;DrvStretchBltROP&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556306)"> <strong>DrvStretchBltROP</strong> </a>函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565030" data-raw-source="[&lt;strong&gt;EngStrokeAndFillPath&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565030)"><strong>EngStrokeAndFillPath</strong></a></p></td>
<td align="left"><p>笔画 （绘制） 路径，并在同一时间进行填充。 这是 GDI 模拟<a href="https://msdn.microsoft.com/library/windows/hardware/ff556311" data-raw-source="[&lt;strong&gt;DrvStrokeAndFillPath&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556311)"> <strong>DrvStrokeAndFillPath</strong> </a>函数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565033" data-raw-source="[&lt;strong&gt;EngStrokePath&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565033)"><strong>EngStrokePath</strong></a></p></td>
<td align="left"><p>笔画 （绘制） 路径。 这是 GDI 模拟<a href="https://msdn.microsoft.com/library/windows/hardware/ff556316" data-raw-source="[&lt;strong&gt;DrvStrokePath&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556316)"> <strong>DrvStrokePath</strong> </a>函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565037" data-raw-source="[&lt;strong&gt;EngTransparentBlt&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565037)"><strong>EngTransparentBlt</strong></a></p></td>
<td align="left"><p>执行透明 blt。 这是 GDI 模拟<a href="https://msdn.microsoft.com/library/windows/hardware/ff557283" data-raw-source="[&lt;strong&gt;DrvTransparentBlt&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557283)"> <strong>DrvTransparentBlt</strong> </a>函数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570623" data-raw-source="[&lt;strong&gt;XFORMOBJ_bApplyXform&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570623)"><strong>XFORMOBJ_bApplyXform</strong></a></p></td>
<td align="left"><p>将给定的转换或及其反转应用于给定的点数组。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570627" data-raw-source="[&lt;strong&gt;XFORMOBJ_iGetFloatObjXform&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570627)"><strong>XFORMOBJ_iGetFloatObjXform</strong></a></p></td>
<td align="left"><p>下载 FLOATOBJ 转换到驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570630" data-raw-source="[&lt;strong&gt;XFORMOBJ_iGetXform&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570630)"><strong>XFORMOBJ_iGetXform</strong></a></p></td>
<td align="left"><p>下载一个转换，转换到驱动程序。</p></td>
</tr>
</tbody>
</table>

 

 

 






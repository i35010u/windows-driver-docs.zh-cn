---
title: 使用 DrvEnableDirectDraw 的 DirectDraw 回调支持
description: 使用 DrvEnableDirectDraw 的 DirectDraw 回调支持
ms.assetid: 74caab2b-6976-411a-97af-7c94b0c12fa0
keywords:
- DirectDraw 驱动程序初始化 WDK Windows 2000 显示，Windows 2000
- 回调函数 WDK DirectDraw
- DrvEnableDirectDraw
- DirectDraw 驱动程序初始化 WDK Windows 2000 显示，回调函数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21c69438c3048498dbc4241c6f56786837c2b18e
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90106290"
---
# <a name="directdraw-callback-support-using-drvenabledirectdraw"></a>使用 DrvEnableDirectDraw 的 DirectDraw 回调支持


## <span id="ddk_directdraw_callback_support_using_drvenabledirectdraw_gg"></span><span id="DDK_DIRECTDRAW_CALLBACK_SUPPORT_USING_DRVENABLEDIRECTDRAW_GG"></span>


显示驱动程序可以实现 [**DrvEnableDirectDraw**](/windows/desktop/api/winddi/nf-winddi-drvenabledirectdraw) 函数以指示各种 DirectDraw 回调支持。 为了指示支持，驱动程序将在*pCallBacks*、 *pSurfaceCallBacks*和*PPaletteCallBacks*参数中返回指向[**dd \_ 回调**](/windows/desktop/api/ddrawint/ns-ddrawint-dd_callbacks)、 [**dd \_ SURFACECALLBACKS**](/windows/desktop/api/ddrawint/ns-ddrawint-dd_surfacecallbacks)和[**dd \_ PALETTECALLBACKS**](/windows/desktop/api/ddrawint/ns-ddrawint-dd_palettecallbacks)结构的指针。

驱动程序将填充 [**DD \_ 回调**](/windows/desktop/api/ddrawint/ns-ddrawint-dd_callbacks) 结构的成员，以指示它支持以下回调函数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">回调函数</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="/previous-versions/windows/hardware/drivers/ff549213(v=vs.85)" data-raw-source="[&lt;em&gt;DdCanCreateSurface&lt;/em&gt;](/previous-versions/windows/hardware/drivers/ff549213(v=vs.85))"><em>DdCanCreateSurface</em></a></p></td>
<td align="left"><p>返回一个值，该值指示驱动程序是否可以创建指定表面说明的图面。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createpalette" data-raw-source="[&lt;em&gt;DdCreatePalette&lt;/em&gt;](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createpalette)"><em>DdCreatePalette</em></a></p></td>
<td align="left"><p>为指定的 DirectDraw 对象创建 DirectDrawPalette 对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/previous-versions/windows/hardware/drivers/ff549263(v=vs.85)" data-raw-source="[&lt;em&gt;DdCreateSurface&lt;/em&gt;](/previous-versions/windows/hardware/drivers/ff549263(v=vs.85))"><em>DdCreateSurface</em></a></p></td>
<td align="left"><p>创建 DirectDraw 面。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getscanline" data-raw-source="[&lt;em&gt;DdGetScanLine&lt;/em&gt;](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getscanline)"><em>DdGetScanLine</em></a></p></td>
<td align="left"><p>返回当前物理扫描行的行号。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mapmemory" data-raw-source="[&lt;em&gt;DdMapMemory&lt;/em&gt;](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mapmemory)"><em>DdMapMemory</em></a></p></td>
<td align="left"><p>将帧缓冲区的可应用程序可修改部分映射到指定进程的用户模式地址空间，或 messagebox 取消内存。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/ddrawint/nc-ddrawint-pdd_waitforverticalblank" data-raw-source="[&lt;em&gt;DdWaitForVerticalBlank&lt;/em&gt;](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_waitforverticalblank)"><em>DdWaitForVerticalBlank</em></a></p></td>
<td align="left"><p>返回设备的垂直空白状态。</p></td>
</tr>
</tbody>
</table>

 

驱动程序将填充 [**DD \_ SURFACECALLBACKS**](/windows/desktop/api/ddrawint/ns-ddrawint-dd_surfacecallbacks) 结构的成员，以指示它支持以下回调函数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">回调函数</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_addattachedsurface" data-raw-source="[&lt;em&gt;DdAddAttachedSurface&lt;/em&gt;](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_addattachedsurface)"><em>DdAddAttachedSurface</em></a></p></td>
<td align="left"><p>将图面附加到另一个图面。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_blt" data-raw-source="[&lt;em&gt;DdBlt&lt;/em&gt;](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_blt)"><em>DdBlt</em></a></p></td>
<td align="left"><p>执行位块传输 (blt 将源图面上的显示数据) 到目标图面。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_destroysurface" data-raw-source="[&lt;em&gt;DdDestroySurface&lt;/em&gt;](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_destroysurface)"><em>DdDestroySurface</em></a></p></td>
<td align="left"><p>销毁 DirectDraw 面。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_flip" data-raw-source="[&lt;em&gt;DdFlip&lt;/em&gt;](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_flip)"><em>DdFlip</em></a></p></td>
<td align="left"><p>使与目标图面关联的图面成为主要表面，并使当前曲面成为主要表面。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_getbltstatus" data-raw-source="[&lt;em&gt;DdGetBltStatus&lt;/em&gt;](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_getbltstatus)"><em>DdGetBltStatus</em></a></p></td>
<td align="left"><p>查询指定表面的 blt 状态。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_getflipstatus" data-raw-source="[&lt;em&gt;DdGetFlipStatus&lt;/em&gt;](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_getflipstatus)"><em>DdGetFlipStatus</em></a></p></td>
<td align="left"><p>确定是否已在表面上出现最近请求的翻转。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_lock" data-raw-source="[&lt;em&gt;DdLock&lt;/em&gt;](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_lock)"><em>DdLock</em></a></p></td>
<td align="left"><p>锁定指定的 surface 内存区域，并提供指向与图面关联的内存块的有效指针。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_setcolorkey" data-raw-source="[&lt;em&gt;DdSetColorKey&lt;/em&gt;](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_setcolorkey)"><em>DdSetColorKey</em></a></p></td>
<td align="left"><p>设置指定图面的颜色键值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_setoverlayposition" data-raw-source="[&lt;em&gt;DdSetOverlayPosition&lt;/em&gt;](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_setoverlayposition)"><em>DdSetOverlayPosition</em></a></p></td>
<td align="left"><p>设置覆盖的位置。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_setpalette" data-raw-source="[&lt;em&gt;DdSetPalette&lt;/em&gt;](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_setpalette)"><em>DdSetPalette</em></a></p></td>
<td align="left"><p>将调色板附加到指定的图面。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_unlock" data-raw-source="[&lt;em&gt;DdUnlock&lt;/em&gt;](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_unlock)"><em>DdUnlock</em></a></p></td>
<td align="left"><p>释放指定图面上持有的锁。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_updateoverlay" data-raw-source="[&lt;em&gt;DdUpdateOverlay&lt;/em&gt;](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_updateoverlay)"><em>DdUpdateOverlay</em></a></p></td>
<td align="left"><p>重新定位或修改叠加图面的视觉对象特性。</p></td>
</tr>
</tbody>
</table>

 

驱动程序将填充 [**DD \_ PALETTECALLBACKS**](/windows/desktop/api/ddrawint/ns-ddrawint-dd_palettecallbacks) 结构的成员，以指示它支持以下回调函数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">回调函数</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/ddrawint/nc-ddrawint-pdd_palcb_destroypalette" data-raw-source="[&lt;em&gt;DdDestroyPalette&lt;/em&gt;](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_palcb_destroypalette)"><em>DdDestroyPalette</em></a></p></td>
<td align="left"><p>销毁指定的调色板。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/ddrawint/nc-ddrawint-pdd_palcb_setentries" data-raw-source="[&lt;em&gt;DdSetEntries&lt;/em&gt;](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_palcb_setentries)"><em>DdSetEntries</em></a></p></td>
<td align="left"><p>更新指定调色板中的调色板项。</p></td>
</tr>
</tbody>
</table>

 


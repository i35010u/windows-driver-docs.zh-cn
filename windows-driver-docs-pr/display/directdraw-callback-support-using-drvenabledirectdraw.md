---
title: 使用 DrvEnableDirectDraw 的 DirectDraw 回调支持
description: 使用 DrvEnableDirectDraw 的 DirectDraw 回调支持
ms.assetid: 74caab2b-6976-411a-97af-7c94b0c12fa0
keywords:
- DirectDraw 驱动程序初始化 WDK Windows 2000 显示，Windows 2000
- 回调函数 WDK DirectDraw
- DrvEnableDirectDraw
- DirectDraw 驱动程序初始化 WDK Windows 2000 显示中，回调函数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06d711257a6e69c9851fe00a79ce6f69faaa249c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384850"
---
# <a name="directdraw-callback-support-using-drvenabledirectdraw"></a>使用 DrvEnableDirectDraw 的 DirectDraw 回调支持


## <span id="ddk_directdraw_callback_support_using_drvenabledirectdraw_gg"></span><span id="DDK_DIRECTDRAW_CALLBACK_SUPPORT_USING_DRVENABLEDIRECTDRAW_GG"></span>


显示驱动程序可以实现[ **DrvEnableDirectDraw** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenabledirectdraw)函数以指示各种 DirectDraw 回调支持。 若要指示支持，驱动程序将返回指向[ **DD\_回调**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_callbacks)， [ **DD\_SURFACECALLBACKS** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_surfacecallbacks)，并[ **DD\_PALETTECALLBACKS** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_palettecallbacks)中结构*pCallBacks*， *pSurfaceCallBacks*，并*pPaletteCallBacks*参数。

该驱动程序使用的成员来填充[ **DD\_回调**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_callbacks)结构，以指示它支持以下的回调函数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">回调函数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549213(v=vs.85)" data-raw-source="[&lt;em&gt;DdCanCreateSurface&lt;/em&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549213(v=vs.85))"><em>DdCanCreateSurface</em></a></p></td>
<td align="left"><p>返回一个值，指示该驱动程序是否可以创建指定的图面上说明的图面。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createpalette" data-raw-source="[&lt;em&gt;DdCreatePalette&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createpalette)"><em>DdCreatePalette</em></a></p></td>
<td align="left"><p>创建指定的 DirectDraw 对象 DirectDrawPalette 对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549263(v=vs.85)" data-raw-source="[&lt;em&gt;DdCreateSurface&lt;/em&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549263(v=vs.85))"><em>DdCreateSurface</em></a></p></td>
<td align="left"><p>创建 DirectDraw 图面。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getscanline" data-raw-source="[&lt;em&gt;DdGetScanLine&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getscanline)"><em>DdGetScanLine</em></a></p></td>
<td align="left"><p>返回当前物理扫描行数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mapmemory" data-raw-source="[&lt;em&gt;DdMapMemory&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mapmemory)"><em>DdMapMemory</em></a></p></td>
<td align="left"><p>映射应用程序的可修改部分用户模式下的帧缓冲区的地址空间的指定进程，或取消映射内存。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_waitforverticalblank" data-raw-source="[&lt;em&gt;DdWaitForVerticalBlank&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_waitforverticalblank)"><em>DdWaitForVerticalBlank</em></a></p></td>
<td align="left"><p>返回设备的垂直空白状态。</p></td>
</tr>
</tbody>
</table>

 

该驱动程序使用的成员来填充[ **DD\_SURFACECALLBACKS** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_surfacecallbacks)结构，以指示它支持以下的回调函数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">回调函数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_addattachedsurface" data-raw-source="[&lt;em&gt;DdAddAttachedSurface&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_addattachedsurface)"><em>DdAddAttachedSurface</em></a></p></td>
<td align="left"><p>连接到另一个曲面的图面。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_blt" data-raw-source="[&lt;em&gt;DdBlt&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_blt)"><em>DdBlt</em></a></p></td>
<td align="left"><p>位块传输 (blt) 显示数据的源图面中执行到目标图面。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_destroysurface" data-raw-source="[&lt;em&gt;DdDestroySurface&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_destroysurface)"><em>DdDestroySurface</em></a></p></td>
<td align="left"><p>销毁 DirectDraw 图面。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_flip" data-raw-source="[&lt;em&gt;DdFlip&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_flip)"><em>DdFlip</em></a></p></td>
<td align="left"><p>会导致与成为主图面，将目标图面和当前面成为非主键面关联的图面上的内存。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_getbltstatus" data-raw-source="[&lt;em&gt;DdGetBltStatus&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_getbltstatus)"><em>DdGetBltStatus</em></a></p></td>
<td align="left"><p>查询指定的表面的 blt 状态。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_getflipstatus" data-raw-source="[&lt;em&gt;DdGetFlipStatus&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_getflipstatus)"><em>DdGetFlipStatus</em></a></p></td>
<td align="left"><p>确定是否在最近请求翻转发生图面。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_lock" data-raw-source="[&lt;em&gt;DdLock&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_lock)"><em>DdLock</em></a></p></td>
<td align="left"><p>锁定指定的图面上的内存区域，并提供指向与图面相关联的内存块的有效指针。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_setcolorkey" data-raw-source="[&lt;em&gt;DdSetColorKey&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_setcolorkey)"><em>DdSetColorKey</em></a></p></td>
<td align="left"><p>设置指定的表面的颜色键值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_setoverlayposition" data-raw-source="[&lt;em&gt;DdSetOverlayPosition&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_setoverlayposition)"><em>DdSetOverlayPosition</em></a></p></td>
<td align="left"><p>设置一个覆盖区的位置。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_setpalette" data-raw-source="[&lt;em&gt;DdSetPalette&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_setpalette)"><em>DdSetPalette</em></a></p></td>
<td align="left"><p>将调色板附加到指定的图面。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_unlock" data-raw-source="[&lt;em&gt;DdUnlock&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_unlock)"><em>DdUnlock</em></a></p></td>
<td align="left"><p>释放指定的图面上所持有的锁。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_updateoverlay" data-raw-source="[&lt;em&gt;DdUpdateOverlay&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_updateoverlay)"><em>DdUpdateOverlay</em></a></p></td>
<td align="left"><p>重新定位或修改的覆盖面的可视属性。</p></td>
</tr>
</tbody>
</table>

 

该驱动程序使用的成员来填充[ **DD\_PALETTECALLBACKS** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_palettecallbacks)结构，以指示它支持以下的回调函数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">回调函数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_palcb_destroypalette" data-raw-source="[&lt;em&gt;DdDestroyPalette&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_palcb_destroypalette)"><em>DdDestroyPalette</em></a></p></td>
<td align="left"><p>销毁指定的调色板。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_palcb_setentries" data-raw-source="[&lt;em&gt;DdSetEntries&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_palcb_setentries)"><em>DdSetEntries</em></a></p></td>
<td align="left"><p>更新指定调色板中的调色板条目。</p></td>
</tr>
</tbody>
</table>

 

 

 






---
title: 图面的 GDI 支持
description: 图面的 GDI 支持
ms.assetid: 78c1e09d-8c3e-4c5d-b670-2e4adf77814f
keywords:
- DrvEnableSurface
- DrvDisableSurface
- GDI WDK Windows 2000 显示，图面
- 图形驱动程序 WDK Windows 2000 显示，图面
- 绘制 WDK GDI，图面
- 启用和禁用 WDK GDI 图面
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee9b796ca08e8e4eb4c8a458fe46f4a7736195c7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382356"
---
# <a name="gdi-support-for-surfaces"></a>图面的 GDI 支持


## <span id="ddk_gdi_support_for_surfaces_gg"></span><span id="DDK_GDI_SUPPORT_FOR_SURFACES_GG"></span>


每个*PDEV*，驱动程序必须支持[ **DrvEnableSurface** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablesurface)函数。 *DrvEnableSurface*将设置在图面绘制，将其与 PDEV 关联。 该驱动程序还必须支持[ **DrvDisableSurface** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisablesurface)到禁用创建表面的函数。 因为 GDI 创建和维护在图面，该驱动程序依赖于多个 GDI 服务函数，来实现启用和禁用应用层下表中列出。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">函数名称</th>
<th align="left">用途</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engassociatesurface" data-raw-source="[&lt;strong&gt;EngAssociateSurface&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engassociatesurface)"><strong>EngAssociateSurface</strong></a></p></td>
<td align="left"><p>将图面与 PDEV 相关联，并定义驱动程序编写器要为该图面挂接出绘制操作。 它使用 PDEV 的默认调色板和样式的步骤。 该驱动程序必须在执行期间进行此调用主面的<a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablesurface" data-raw-source="[&lt;strong&gt;DrvEnableSurface&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablesurface)"> <strong>DrvEnableSurface</strong></a>。 它在锁定面以在其上书写前启用辅助图面时，驱动程序还必须进行此调用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcheckabort" data-raw-source="[&lt;strong&gt;EngCheckAbort&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcheckabort)"><strong>EngCheckAbort</strong></a></p></td>
<td align="left"><p>（仅限打印机）使打印机驱动程序以确定其打印机作业是否已被终止。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreatebitmap" data-raw-source="[&lt;strong&gt;EngCreateBitmap&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreatebitmap)"><strong>EngCreateBitmap</strong></a></p></td>
<td align="left"><p>创建标准格式<a href="https://docs.microsoft.com/windows-hardware/drivers/#wdkgloss-device-independent-bitmap--dib-" data-raw-source="&lt;em&gt;DIB&lt;/em&gt;"> <em>DIB</em> </a>位图。 GDI 可以执行这种类型的图面上的所有绘制操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreatedevicebitmap" data-raw-source="[&lt;strong&gt;EngCreateDeviceBitmap&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreatedevicebitmap)"><strong>EngCreateDeviceBitmap</strong></a></p></td>
<td align="left"><p>创建驱动程序负责 （尽管它可以被创建为 DIB，在其中用例驱动程序可以回叫，若要具有 GDI 绘制在其上） 上绘制一个依赖于设备的位图。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreatedevicesurface" data-raw-source="[&lt;strong&gt;EngCreateDeviceSurface&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreatedevicesurface)"><strong>EngCreateDeviceSurface</strong></a></p></td>
<td align="left"><p>创建<a href="https://docs.microsoft.com/windows-hardware/drivers/#wdkgloss-device-managed-surface" data-raw-source="&lt;em&gt;device-managed surface&lt;/em&gt;"><em>设备管理面</em></a>。 该驱动程序负责管理此面的某些绘制操作。 该函数返回一个句柄，该驱动程序管理。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreatewnd" data-raw-source="[&lt;strong&gt;EngCreateWnd&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreatewnd)"><strong>EngCreateWnd</strong></a></p></td>
<td align="left"><p>创建<a href="https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_wndobj" data-raw-source="[&lt;strong&gt;WNDOBJ&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_wndobj)"> <strong>WNDOBJ</strong> </a>结构指定的图面上。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engdeletesurface" data-raw-source="[&lt;strong&gt;EngDeleteSurface&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engdeletesurface)"><strong>EngDeleteSurface</strong></a></p></td>
<td align="left"><p>删除图面 （DIB、 设备相关位图或设备管理面）。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engdeletewnd" data-raw-source="[&lt;strong&gt;EngDeleteWnd&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engdeletewnd)"><strong>EngDeleteWnd</strong></a></p></td>
<td align="left"><p>删除<a href="https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_wndobj" data-raw-source="[&lt;strong&gt;WNDOBJ&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_wndobj)"> <strong>WNDOBJ</strong> </a>结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engerasesurface" data-raw-source="[&lt;strong&gt;EngEraseSurface&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engerasesurface)"><strong>EngEraseSurface</strong></a></p></td>
<td align="left"><p>用给定的颜色，以便有效擦除填充图面上指定的矩形。 应调用此函数只是为了清除 GDI 位图的图面。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-englockdirectdrawsurface" data-raw-source="[&lt;strong&gt;EngLockDirectDrawSurface&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-englockdirectdrawsurface)"><strong>EngLockDirectDrawSurface</strong></a></p></td>
<td align="left"><p>锁定的 DirectDraw 表面的内核模式句柄。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-englocksurface" data-raw-source="[&lt;strong&gt;EngLockSurface&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-englocksurface)"><strong>EngLockSurface</strong></a></p></td>
<td align="left"><p>为驱动程序访问提供了到创建的图面，通过创建用户对象 (<a href="https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_surfobj" data-raw-source="[&lt;strong&gt;SURFOBJ&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_surfobj)"><strong>SURFOBJ</strong></a>) 为该图面。 (<a href="surface-negotiation.md" data-raw-source="[primary surface](surface-negotiation.md)">主表面</a>未锁定。)</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engmarkbandingsurface" data-raw-source="[&lt;strong&gt;EngMarkBandingSurface&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engmarkbandingsurface)"><strong>EngMarkBandingSurface</strong></a></p></td>
<td align="left"><p>（仅限打印机）将图面标记为联合的图面。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engmodifysurface" data-raw-source="[&lt;strong&gt;EngModifySurface&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engmodifysurface)"><strong>EngModifySurface</strong></a></p></td>
<td align="left"><p>有关驱动程序创建的表面的属性通知 GDI。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engunlockdirectdrawsurface" data-raw-source="[&lt;strong&gt;EngUnlockDirectDrawSurface&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engunlockdirectdrawsurface)"><strong>EngUnlockDirectDrawSurface</strong></a></p></td>
<td align="left"><p>发布给定的 DirectDraw 指定图面上的锁。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engunlocksurface" data-raw-source="[&lt;strong&gt;EngUnlockSurface&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engunlocksurface)"><strong>EngUnlockSurface</strong></a></p></td>
<td align="left"><p>该驱动程序已完成绘制操作将解除对图面 (禁用时要调用<a href="surface-negotiation.md" data-raw-source="[secondary surface](surface-negotiation.md)">辅助面</a>)。</p></td>
</tr>
</tbody>
</table>

 

 

 






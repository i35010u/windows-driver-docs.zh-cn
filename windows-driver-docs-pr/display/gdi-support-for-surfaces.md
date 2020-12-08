---
title: 图面的 GDI 支持
description: 图面的 GDI 支持
keywords:
- DrvEnableSurface
- DrvDisableSurface
- GDI WDK Windows 2000 显示，表面
- 图形驱动程序 WDK Windows 2000 显示，表面
- 绘制 WDK GDI，图面
- surface 启用和禁用 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 715dbf7637ef9d514e215201927e1fdb3b3702aa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822514"
---
# <a name="gdi-support-for-surfaces"></a>图面的 GDI 支持


## <span id="ddk_gdi_support_for_surfaces_gg"></span><span id="DDK_GDI_SUPPORT_FOR_SURFACES_GG"></span>


对于每个 *PDEV*，驱动程序必须支持 [**DrvEnableSurface**](/windows/win32/api/winddi/nf-winddi-drvenablesurface) 函数。 *DrvEnableSurface* 设置要在其上绘制的图面，并将其与 PDEV 相关联。 驱动程序还必须支持 [**DrvDisableSurface**](/windows/win32/api/winddi/nf-winddi-drvdisablesurface) 函数以禁用创建的图面。 由于 GDI 创建并维护图面，因此驱动程序依赖于下表中列出的几个 GDI 服务函数来实现曲面的启用和禁用。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">函数名称</th>
<th align="left">目的</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engassociatesurface" data-raw-source="[&lt;strong&gt;EngAssociateSurface&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engassociatesurface)"><strong>EngAssociateSurface</strong></a></p></td>
<td align="left"><p>将图面与 PDEV 相关联，并定义驱动程序编写器要为该表面挂钩的绘制操作。 它使用 PDEV 的默认调色板和样式步骤。 在执行 <a href="/windows/win32/api/winddi/nf-winddi-drvenablesurface" data-raw-source="[&lt;strong&gt;DrvEnableSurface&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvenablesurface)"><strong>DrvEnableSurface</strong></a>期间，驱动程序必须对主要表面进行此调用。 当驱动程序启用辅助图面以便在其上写入时，驱动程序也必须进行此调用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engcheckabort" data-raw-source="[&lt;strong&gt;EngCheckAbort&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engcheckabort)"><strong>EngCheckAbort</strong></a></p></td>
<td align="left"><p> (打印机仅) 使打印机驱动程序能够确定其打印机作业是否已终止。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engcreatebitmap" data-raw-source="[&lt;strong&gt;EngCreateBitmap&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engcreatebitmap)"><strong>EngCreateBitmap</strong></a></p></td>
<td align="left"><p>创建标准格式 <a href="/windows-hardware/drivers/#wdkgloss-device-independent-bitmap--dib-" data-raw-source="&lt;em&gt;DIB&lt;/em&gt;"><em>DIB</em></a> 位图。 GDI 可对此类表面执行所有绘图操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engcreatedevicebitmap" data-raw-source="[&lt;strong&gt;EngCreateDeviceBitmap&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engcreatedevicebitmap)"><strong>EngCreateDeviceBitmap</strong></a></p></td>
<td align="left"><p>创建与设备相关的位图，驱动程序负责在 (上进行绘制，尽管可以将其创建为 DIB，在这种情况下，驱动程序可以回调以在其) 上进行 GDI 绘制。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engcreatedevicesurface" data-raw-source="[&lt;strong&gt;EngCreateDeviceSurface&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engcreatedevicesurface)"><strong>EngCreateDeviceSurface</strong></a></p></td>
<td align="left"><p>创建 <a href="/windows-hardware/drivers/#wdkgloss-device-managed-surface" data-raw-source="&lt;em&gt;device-managed surface&lt;/em&gt;"><em>设备管理的图面</em></a>。 驱动程序负责管理此表面的某些绘图操作。 函数将返回驱动程序管理的句柄。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engcreatewnd" data-raw-source="[&lt;strong&gt;EngCreateWnd&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engcreatewnd)"><strong>EngCreateWnd</strong></a></p></td>
<td align="left"><p>在指定表面上创建 <a href="/windows/win32/api/winddi/ns-winddi-wndobj" data-raw-source="[&lt;strong&gt;WNDOBJ&lt;/strong&gt;](/windows/win32/api/winddi/ns-winddi-_wndobj)"><strong>WNDOBJ</strong></a> 结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engdeletesurface" data-raw-source="[&lt;strong&gt;EngDeleteSurface&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engdeletesurface)"><strong>EngDeleteSurface</strong></a></p></td>
<td align="left"><p>删除 (DIB、设备相关位图或设备管理的图面) 的图面。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engdeletewnd" data-raw-source="[&lt;strong&gt;EngDeleteWnd&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engdeletewnd)"><strong>EngDeleteWnd</strong></a></p></td>
<td align="left"><p>删除 <a href="/windows/win32/api/winddi/ns-winddi-wndobj" data-raw-source="[&lt;strong&gt;WNDOBJ&lt;/strong&gt;](/windows/win32/api/winddi/ns-winddi-_wndobj)"><strong>WNDOBJ</strong></a> 结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engerasesurface" data-raw-source="[&lt;strong&gt;EngEraseSurface&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engerasesurface)"><strong>EngEraseSurface</strong></a></p></td>
<td align="left"><p>使用给定的颜色在表面上填充指定的矩形，并有效地将其清除。 只应调用此函数来擦除 GDI 位图的图面。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-englockdirectdrawsurface" data-raw-source="[&lt;strong&gt;EngLockDirectDrawSurface&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-englockdirectdrawsurface)"><strong>EngLockDirectDrawSurface</strong></a></p></td>
<td align="left"><p>锁定 DirectDraw 图面的内核模式句柄。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-englocksurface" data-raw-source="[&lt;strong&gt;EngLockSurface&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-englocksurface)"><strong>EngLockSurface</strong></a></p></td>
<td align="left"><p>为驱动程序提供对创建的图面的访问权限，方法是为该图面创建一个 (<a href="/windows/win32/api/winddi/ns-winddi-surfobj" data-raw-source="[&lt;strong&gt;SURFOBJ&lt;/strong&gt;](/windows/win32/api/winddi/ns-winddi-_surfobj)"><strong>SURFOBJ</strong></a>) 的用户对象。  (<a href="surface-negotiation.md" data-raw-source="[primary surface](surface-negotiation.md)">主要表面</a> 未锁定。 ) </p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engmarkbandingsurface" data-raw-source="[&lt;strong&gt;EngMarkBandingSurface&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engmarkbandingsurface)"><strong>EngMarkBandingSurface</strong></a></p></td>
<td align="left"><p> (打印机仅) 将图面标记为条带图面。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engmodifysurface" data-raw-source="[&lt;strong&gt;EngModifySurface&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engmodifysurface)"><strong>EngModifySurface</strong></a></p></td>
<td align="left"><p>通知 GDI 有关驱动程序所创建的图面的属性。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engunlockdirectdrawsurface" data-raw-source="[&lt;strong&gt;EngUnlockDirectDrawSurface&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engunlockdirectdrawsurface)"><strong>EngUnlockDirectDrawSurface</strong></a></p></td>
<td align="left"><p>释放给定 DirectDraw 指定图面上的锁。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engunlocksurface" data-raw-source="[&lt;strong&gt;EngUnlockSurface&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engunlocksurface)"><strong>EngUnlockSurface</strong></a></p></td>
<td align="left"><p>当驱动程序完成绘图操作 (在禁用 <a href="surface-negotiation.md" data-raw-source="[secondary surface](surface-negotiation.md)">辅助图面</a>) 时调用，从而解锁图面。</p></td>
</tr>
</tbody>
</table>

 


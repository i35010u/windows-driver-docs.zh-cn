---
title: 窗口对象的 GDI 支持
description: 窗口对象的 GDI 支持
ms.assetid: 288120e0-e43c-4733-8bba-0e310ed55aae
keywords:
- GDI WDK Windows 2000 显示，窗口对象
- 图形驱动程序 WDK Windows 2000 显示，窗口对象
- 绘制 WDK GDI，窗口对象
- 窗口对象 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5afff4c362e3c594bcbf3b56472bd49151129745
ms.sourcegitcommit: f8619f20a0903dd64f8641a5266ecad6df5f1d57
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/29/2020
ms.locfileid: "91423976"
---
# <a name="gdi-support-for-window-objects"></a>窗口对象的 GDI 支持


## <span id="ddk_gdi_support_for_window_objects_gg"></span><span id="DDK_GDI_SUPPORT_FOR_WINDOW_OBJECTS_GG"></span>


GDI 为窗口创建和删除以及矩形的枚举提供支持。

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
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engcreatewnd" data-raw-source="[&lt;strong&gt;EngCreateWnd&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engcreatewnd)"><strong>EngCreateWnd</strong></a></p></td>
<td align="left"><p>在指定表面上创建 <a href="/windows/win32/api/winddi/ns-winddi-wndobj" data-raw-source="[&lt;strong&gt;WNDOBJ&lt;/strong&gt;](/windows/win32/api/winddi/ns-winddi-_wndobj)"><strong>WNDOBJ</strong></a> 结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engdeletewnd" data-raw-source="[&lt;strong&gt;EngDeleteWnd&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engdeletewnd)"><strong>EngDeleteWnd</strong></a></p></td>
<td align="left"><p>删除 <a href="/windows/win32/api/winddi/ns-winddi-wndobj" data-raw-source="[&lt;strong&gt;WNDOBJ&lt;/strong&gt;](/windows/win32/api/winddi/ns-winddi-_wndobj)"><strong>WNDOBJ</strong></a> 结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-wndobj_benum" data-raw-source="[&lt;strong&gt;WNDOBJ_bEnum&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-wndobj_benum)"><strong>WNDOBJ_bEnum</strong></a></p></td>
<td align="left"><p>从窗口的可见区域获取矩形的集合。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-wndobj_cenumstart" data-raw-source="[&lt;strong&gt;WNDOBJ_cEnumStart&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-wndobj_cenumstart)"><strong>WNDOBJ_cEnumStart</strong></a></p></td>
<td align="left"><p>设置窗口可见区域中矩形的枚举参数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-wndobj_vsetconsumer" data-raw-source="[&lt;strong&gt;WNDOBJ_vSetConsumer&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-wndobj_vsetconsumer)"><strong>WNDOBJ_vSetConsumer</strong></a></p></td>
<td align="left"><p>在指定的<a href="/windows/win32/api/winddi/ns-winddi-wndobj" data-raw-source="[&lt;strong&gt;WNDOBJ&lt;/strong&gt;](/windows/win32/api/winddi/ns-winddi-_wndobj)"><strong>WNDOBJ</strong></a>结构的<strong>pvConsumer</strong>成员中设置驱动程序定义的值。</p></td>
</tr>
</tbody>
</table>

 


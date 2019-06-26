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
ms.openlocfilehash: 990a67564aecef7ededfb31e235951585917112c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382340"
---
# <a name="gdi-support-for-window-objects"></a>窗口对象的 GDI 支持


## <span id="ddk_gdi_support_for_window_objects_gg"></span><span id="DDK_GDI_SUPPORT_FOR_WINDOW_OBJECTS_GG"></span>


GDI 提供支持的窗口的创建和删除，以及在窗口中的矩形的枚举。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreatewnd" data-raw-source="[&lt;strong&gt;EngCreateWnd&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreatewnd)"><strong>EngCreateWnd</strong></a></p></td>
<td align="left"><p>创建<a href="https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_wndobj" data-raw-source="[&lt;strong&gt;WNDOBJ&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_wndobj)"> <strong>WNDOBJ</strong> </a>结构指定的图面上。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engdeletewnd" data-raw-source="[&lt;strong&gt;EngDeleteWnd&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engdeletewnd)"><strong>EngDeleteWnd</strong></a></p></td>
<td align="left"><p>删除<a href="https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_wndobj" data-raw-source="[&lt;strong&gt;WNDOBJ&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_wndobj)"> <strong>WNDOBJ</strong> </a>结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-wndobj_benum" data-raw-source="[&lt;strong&gt;WNDOBJ_bEnum&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-wndobj_benum)"><strong>WNDOBJ_bEnum</strong></a></p></td>
<td align="left"><p>获取从一个窗口的可见区域的矩形的集合。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-wndobj_cenumstart" data-raw-source="[&lt;strong&gt;WNDOBJ_cEnumStart&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-wndobj_cenumstart)"><strong>WNDOBJ_cEnumStart</strong></a></p></td>
<td align="left"><p>在窗口的可见区域设置参数的矩形的枚举。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-wndobj_vsetconsumer" data-raw-source="[&lt;strong&gt;WNDOBJ_vSetConsumer&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-wndobj_vsetconsumer)"><strong>WNDOBJ_vSetConsumer</strong></a></p></td>
<td align="left"><p>设置中的驱动程序定义的值<strong>pvConsumer</strong>指定的成员<a href="https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_wndobj" data-raw-source="[&lt;strong&gt;WNDOBJ&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_wndobj)"> <strong>WNDOBJ</strong> </a>结构。</p></td>
</tr>
</tbody>
</table>

 

 

 






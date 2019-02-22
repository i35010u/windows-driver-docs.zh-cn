---
title: GDI 支持窗口对象
description: GDI 支持窗口对象
ms.assetid: 288120e0-e43c-4733-8bba-0e310ed55aae
keywords:
- GDI WDK Windows 2000 显示，窗口对象
- 图形驱动程序 WDK Windows 2000 显示，窗口对象
- 绘制 WDK GDI，窗口对象
- 窗口对象 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3493aba14b3bb655c1ae23ee31cbccfb52a41fc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524439"
---
# <a name="gdi-support-for-window-objects"></a>GDI 支持窗口对象


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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564769" data-raw-source="[&lt;strong&gt;EngCreateWnd&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564769)"><strong>EngCreateWnd</strong></a></p></td>
<td align="left"><p>创建<a href="https://msdn.microsoft.com/library/windows/hardware/ff570599" data-raw-source="[&lt;strong&gt;WNDOBJ&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570599)"> <strong>WNDOBJ</strong> </a>结构指定的图面上。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564830" data-raw-source="[&lt;strong&gt;EngDeleteWnd&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564830)"><strong>EngDeleteWnd</strong></a></p></td>
<td align="left"><p>删除<a href="https://msdn.microsoft.com/library/windows/hardware/ff570599" data-raw-source="[&lt;strong&gt;WNDOBJ&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570599)"> <strong>WNDOBJ</strong> </a>结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570602" data-raw-source="[&lt;strong&gt;WNDOBJ_bEnum&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570602)"><strong>WNDOBJ_bEnum</strong></a></p></td>
<td align="left"><p>获取从一个窗口的可见区域的矩形的集合。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570603" data-raw-source="[&lt;strong&gt;WNDOBJ_cEnumStart&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570603)"><strong>WNDOBJ_cEnumStart</strong></a></p></td>
<td align="left"><p>在窗口的可见区域设置参数的矩形的枚举。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570606" data-raw-source="[&lt;strong&gt;WNDOBJ_vSetConsumer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570606)"><strong>WNDOBJ_vSetConsumer</strong></a></p></td>
<td align="left"><p>设置中的驱动程序定义的值<strong>pvConsumer</strong>指定的成员<a href="https://msdn.microsoft.com/library/windows/hardware/ff570599" data-raw-source="[&lt;strong&gt;WNDOBJ&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570599)"> <strong>WNDOBJ</strong> </a>结构。</p></td>
</tr>
</tbody>
</table>

 

 

 






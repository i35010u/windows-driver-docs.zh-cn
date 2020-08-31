---
title: 路径的 GDI 服务
description: 路径的 GDI 服务
ms.assetid: 8fc51b7e-d787-48ed-a865-528547abefc5
keywords:
- GDI WDK Windows 2000 显示，路径
- 图形驱动程序 WDK Windows 2000 显示，路径
- 绘制 WDK GDI，路径
- 路径 WDK GDI
- 填充路径 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5fd880880fc043aaab466163a68a971c889e0aee
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89064256"
---
# <a name="gdi-services-for-paths"></a>路径的 GDI 服务


## <span id="ddk_gdi_services_for_paths_gg"></span><span id="DDK_GDI_SERVICES_FOR_PATHS_GG"></span>


为了帮助矢量设备填充复杂区域，其驱动程序可以调用下表中列出的用于创建、修改和枚举路径的引擎函数。 驱动程序可以通过 [**PATHOBJ**](/windows/desktop/api/winddi/ns-winddi-_pathobj) 结构访问路径。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">GDI 路径服务函数</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreatepath" data-raw-source="[&lt;strong&gt;EngCreatePath&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-engcreatepath)"><strong>EngCreatePath</strong></a></p></td>
<td align="left"><p>为驱动程序的临时使用分配一个路径。 在从其当前的绘图调用返回到 GDI 之前，驱动程序应删除此路径。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engdeletepath" data-raw-source="[&lt;strong&gt;EngDeletePath&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-engdeletepath)"><strong>EngDeletePath</strong></a></p></td>
<td align="left"><p>删除由 <strong>EngCreatePath</strong> 函数分配的路径。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-pathobj_bclosefigure" data-raw-source="[&lt;strong&gt;PATHOBJ_bCloseFigure&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-pathobj_bclosefigure)"><strong>PATHOBJ_bCloseFigure</strong></a></p></td>
<td align="left"><p>关闭路径 (用于填充) ，方法是将行绘制回开始点。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-pathobj_benum" data-raw-source="[&lt;strong&gt;PATHOBJ_bEnum&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-pathobj_benum)"><strong>PATHOBJ_bEnum</strong></a></p></td>
<td align="left"><p>检索路径中的下一个 <a href="https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_pathdata" data-raw-source="[&lt;strong&gt;PATHDATA&lt;/strong&gt;](/windows/desktop/api/winddi/ns-winddi-_pathdata)"><strong>PATHDATA</strong></a> 记录。 每条记录描述全部或部分子路径。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-pathobj_benumcliplines" data-raw-source="[&lt;strong&gt;PATHOBJ_bEnumClipLines&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-pathobj_benumcliplines)"><strong>PATHOBJ_bEnumClipLines</strong></a></p></td>
<td align="left"><p>枚举路径中的剪裁线段。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-pathobj_bmoveto" data-raw-source="[&lt;strong&gt;PATHOBJ_bMoveTo&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-pathobj_bmoveto)"><strong>PATHOBJ_bMoveTo</strong></a></p></td>
<td align="left"><p>更改 <a href="https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_pathobj" data-raw-source="[&lt;strong&gt;PATHOBJ&lt;/strong&gt;](/windows/desktop/api/winddi/ns-winddi-_pathobj)"><strong>PATHOBJ</strong></a>定义路径中的当前位置。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-pathobj_bpolybezierto" data-raw-source="[&lt;strong&gt;PATHOBJ_bPolyBezierTo&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-pathobj_bpolybezierto)"><strong>PATHOBJ_bPolyBezierTo</strong></a></p></td>
<td align="left"><p>在 PATHOBJ 定义的路径中绘制)  (三次曲线的贝塞尔曲线。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-pathobj_bpolylineto" data-raw-source="[&lt;strong&gt;PATHOBJ_bPolyLineTo&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-pathobj_bpolylineto)"><strong>PATHOBJ_bPolyLineTo</strong></a></p></td>
<td align="left"><p>在 PATHOBJ 定义的路径中绘制线条。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-pathobj_venumstart" data-raw-source="[&lt;strong&gt;PATHOBJ_vEnumStart&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-pathobj_venumstart)"><strong>PATHOBJ_vEnumStart</strong></a></p></td>
<td align="left"><p>通知 <a href="https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_pathobj" data-raw-source="[&lt;strong&gt;PATHOBJ&lt;/strong&gt;](/windows/desktop/api/winddi/ns-winddi-_pathobj)"><strong>PATHOBJ</strong></a> 驱动程序将开始调用 <strong>PATHOBJ_bEnum</strong> 来枚举指定路径中的曲线。 如果重启枚举，则必须调用此函数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-pathobj_venumstartcliplines" data-raw-source="[&lt;strong&gt;PATHOBJ_vEnumStartClipLines&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-pathobj_venumstartcliplines)"><strong>PATHOBJ_vEnumStartClipLines</strong></a></p></td>
<td align="left"><p>允许驱动程序要求在 <a href="https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_clipobj" data-raw-source="&lt;strong&gt;CLIPOBJ&lt;/strong&gt;"><em>剪辑区域</em></a> 上剪裁的行比单个矩形更复杂。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-pathobj_vgetbounds" data-raw-source="[&lt;strong&gt;PATHOBJ_vGetBounds&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-pathobj_vgetbounds)"><strong>PATHOBJ_vGetBounds</strong></a></p></td>
<td align="left"><p>返回路径的边框。</p></td>
</tr>
</tbody>
</table>

 

 


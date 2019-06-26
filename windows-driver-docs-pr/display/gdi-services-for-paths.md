---
title: 路径的 GDI 服务
description: 路径的 GDI 服务
ms.assetid: 8fc51b7e-d787-48ed-a865-528547abefc5
keywords:
- GDI WDK Windows 2000 显示中路径
- 图形驱动程序 WDK Windows 2000 显示路径
- 绘制 WDK GDI，路径
- 路径 WDK GDI
- 填充路径 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 26da52fcfa7359513615bd9a10bd7eba1d4ebb5c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354721"
---
# <a name="gdi-services-for-paths"></a>路径的 GDI 服务


## <span id="ddk_gdi_services_for_paths_gg"></span><span id="DDK_GDI_SERVICES_FOR_PATHS_GG"></span>


若要帮助向量设备填充复杂的方面，其驱动程序可以调用引擎列出的函数下, 表中的创建、 修改和枚举路径。 该驱动程序有权访问通过路径[ **PATHOBJ** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_pathobj)结构。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">GDI 路径服务函数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreatepath" data-raw-source="[&lt;strong&gt;EngCreatePath&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreatepath)"><strong>EngCreatePath</strong></a></p></td>
<td align="left"><p>驱动程序的临时用于分配一个路径。 该驱动程序应从其当前的绘图调用返回到 GDI 之前删除此路径。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engdeletepath" data-raw-source="[&lt;strong&gt;EngDeletePath&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engdeletepath)"><strong>EngDeletePath</strong></a></p></td>
<td align="left"><p>删除分配的路径<strong>EngCreatePath</strong>函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-pathobj_bclosefigure" data-raw-source="[&lt;strong&gt;PATHOBJ_bCloseFigure&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-pathobj_bclosefigure)"><strong>PATHOBJ_bCloseFigure</strong></a></p></td>
<td align="left"><p>通过返回到起始点绘制一条直线，闭合路径 （适用于填满）。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-pathobj_benum" data-raw-source="[&lt;strong&gt;PATHOBJ_bEnum&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-pathobj_benum)"><strong>PATHOBJ_bEnum</strong></a></p></td>
<td align="left"><p>检索下一步<a href="https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_pathdata" data-raw-source="[&lt;strong&gt;PATHDATA&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_pathdata)"> <strong>PATHDATA</strong> </a>记录从路径。 每条记录描述子路径的全部或部分。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-pathobj_benumcliplines" data-raw-source="[&lt;strong&gt;PATHOBJ_bEnumClipLines&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-pathobj_benumcliplines)"><strong>PATHOBJ_bEnumClipLines</strong></a></p></td>
<td align="left"><p>枚举从路径剪切的直线线段。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-pathobj_bmoveto" data-raw-source="[&lt;strong&gt;PATHOBJ_bMoveTo&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-pathobj_bmoveto)"><strong>PATHOBJ_bMoveTo</strong></a></p></td>
<td align="left"><p>更改中的当前位置<a href="https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_pathobj" data-raw-source="[&lt;strong&gt;PATHOBJ&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_pathobj)"> <strong>PATHOBJ</strong></a>-定义路径。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-pathobj_bpolybezierto" data-raw-source="[&lt;strong&gt;PATHOBJ_bPolyBezierTo&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-pathobj_bpolybezierto)"><strong>PATHOBJ_bPolyBezierTo</strong></a></p></td>
<td align="left"><p>PATHOBJ 定义路径中绘制贝塞尔曲线 （三次方样条）。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-pathobj_bpolylineto" data-raw-source="[&lt;strong&gt;PATHOBJ_bPolyLineTo&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-pathobj_bpolylineto)"><strong>PATHOBJ_bPolyLineTo</strong></a></p></td>
<td align="left"><p>绘制 PATHOBJ 定义路径中的行。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-pathobj_venumstart" data-raw-source="[&lt;strong&gt;PATHOBJ_vEnumStart&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-pathobj_venumstart)"><strong>PATHOBJ_vEnumStart</strong></a></p></td>
<td align="left"><p>通知<a href="https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_pathobj" data-raw-source="[&lt;strong&gt;PATHOBJ&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_pathobj)"> <strong>PATHOBJ</strong> </a>驱动程序将开始调用<strong>PATHOBJ_bEnum</strong>枚举指定的路径中的曲线。 必须发生枚举重新启动时调用此函数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-pathobj_venumstartcliplines" data-raw-source="[&lt;strong&gt;PATHOBJ_vEnumStartClipLines&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-pathobj_venumstartcliplines)"><strong>PATHOBJ_vEnumStartClipLines</strong></a></p></td>
<td align="left"><p>使驱动程序请求行，以针对剪辑<a href="https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_clipobj" data-raw-source="&lt;strong&gt;CLIPOBJ&lt;/strong&gt;"><em>剪辑区域</em></a>比单个矩形更为复杂。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-pathobj_vgetbounds" data-raw-source="[&lt;strong&gt;PATHOBJ_vGetBounds&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-pathobj_vgetbounds)"><strong>PATHOBJ_vGetBounds</strong></a></p></td>
<td align="left"><p>返回路径的绑定矩形。</p></td>
</tr>
</tbody>
</table>

 

 

 






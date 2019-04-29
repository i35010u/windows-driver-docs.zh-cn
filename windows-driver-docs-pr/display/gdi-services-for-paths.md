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
ms.openlocfilehash: 8cb464f3a1b384e1aa6be90b0f7a1c45927b1f2d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63371563"
---
# <a name="gdi-services-for-paths"></a>路径的 GDI 服务


## <span id="ddk_gdi_services_for_paths_gg"></span><span id="DDK_GDI_SERVICES_FOR_PATHS_GG"></span>


若要帮助向量设备填充复杂的方面，其驱动程序可以调用引擎列出的函数下, 表中的创建、 修改和枚举路径。 该驱动程序有权访问通过路径[ **PATHOBJ** ](https://msdn.microsoft.com/library/windows/hardware/ff568849)结构。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564755" data-raw-source="[&lt;strong&gt;EngCreatePath&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564755)"><strong>EngCreatePath</strong></a></p></td>
<td align="left"><p>驱动程序的临时用于分配一个路径。 该驱动程序应从其当前的绘图调用返回到 GDI 之前删除此路径。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564811" data-raw-source="[&lt;strong&gt;EngDeletePath&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564811)"><strong>EngDeletePath</strong></a></p></td>
<td align="left"><p>删除分配的路径<strong>EngCreatePath</strong>函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568850" data-raw-source="[&lt;strong&gt;PATHOBJ_bCloseFigure&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568850)"><strong>PATHOBJ_bCloseFigure</strong></a></p></td>
<td align="left"><p>通过返回到起始点绘制一条直线，闭合路径 （适用于填满）。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568851" data-raw-source="[&lt;strong&gt;PATHOBJ_bEnum&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568851)"><strong>PATHOBJ_bEnum</strong></a></p></td>
<td align="left"><p>检索下一步<a href="https://msdn.microsoft.com/library/windows/hardware/ff568848" data-raw-source="[&lt;strong&gt;PATHDATA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568848)"> <strong>PATHDATA</strong> </a>记录从路径。 每条记录描述子路径的全部或部分。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568852" data-raw-source="[&lt;strong&gt;PATHOBJ_bEnumClipLines&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568852)"><strong>PATHOBJ_bEnumClipLines</strong></a></p></td>
<td align="left"><p>枚举从路径剪切的直线线段。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568853" data-raw-source="[&lt;strong&gt;PATHOBJ_bMoveTo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568853)"><strong>PATHOBJ_bMoveTo</strong></a></p></td>
<td align="left"><p>更改中的当前位置<a href="https://msdn.microsoft.com/library/windows/hardware/ff568849" data-raw-source="[&lt;strong&gt;PATHOBJ&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568849)"> <strong>PATHOBJ</strong></a>-定义路径。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568854" data-raw-source="[&lt;strong&gt;PATHOBJ_bPolyBezierTo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568854)"><strong>PATHOBJ_bPolyBezierTo</strong></a></p></td>
<td align="left"><p>PATHOBJ 定义路径中绘制贝塞尔曲线 （三次方样条）。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568855" data-raw-source="[&lt;strong&gt;PATHOBJ_bPolyLineTo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568855)"><strong>PATHOBJ_bPolyLineTo</strong></a></p></td>
<td align="left"><p>绘制 PATHOBJ 定义路径中的行。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568856" data-raw-source="[&lt;strong&gt;PATHOBJ_vEnumStart&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568856)"><strong>PATHOBJ_vEnumStart</strong></a></p></td>
<td align="left"><p>通知<a href="https://msdn.microsoft.com/library/windows/hardware/ff568849" data-raw-source="[&lt;strong&gt;PATHOBJ&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568849)"> <strong>PATHOBJ</strong> </a>驱动程序将开始调用<strong>PATHOBJ_bEnum</strong>枚举指定的路径中的曲线。 必须发生枚举重新启动时调用此函数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568857" data-raw-source="[&lt;strong&gt;PATHOBJ_vEnumStartClipLines&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568857)"><strong>PATHOBJ_vEnumStartClipLines</strong></a></p></td>
<td align="left"><p>使驱动程序请求行，以针对剪辑<a href="https://msdn.microsoft.com/library/windows/hardware/ff539417" data-raw-source="&lt;strong&gt;CLIPOBJ&lt;/strong&gt;"><em>剪辑区域</em></a>比单个矩形更为复杂。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568858" data-raw-source="[&lt;strong&gt;PATHOBJ_vGetBounds&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568858)"><strong>PATHOBJ_vGetBounds</strong></a></p></td>
<td align="left"><p>返回路径的绑定矩形。</p></td>
</tr>
</tbody>
</table>

 

 

 






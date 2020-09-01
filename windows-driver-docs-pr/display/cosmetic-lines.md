---
title: 装饰线条
description: 装饰线条
ms.assetid: eb9651dd-cc77-469f-8441-4bb958bd374d
keywords:
- 线条 WDK GDI，修饰
- GDI WDK Windows 2000 显示，线条，修饰
- 图形驱动程序 WDK Windows 2000 显示，线条，修饰
- 绘制 WDK GDI，线条，修饰
- 修饰线 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 73c9e5ea1f7fdefe96fe5cfb92ae2499dcb1741e
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89067452"
---
# <a name="cosmetic-lines"></a>装饰线条


## <span id="ddk_cosmetic_lines_gg"></span><span id="DDK_COSMETIC_LINES_GG"></span>


*修饰*线的宽度始终为一个像素，并使用纯色画笔进行绘制。 它根据网格交集量化 (GIQ) 菱形约定进行呈现，这将确定哪些像素应打开以呈现修饰线。

下图显示了在矩形网格上叠加的线条，其中像素位于网格交点处。 若要确定哪些像素应亮起，请假设菱形上有一个菱形，并沿其上滑。 菱形的宽度和高度完全等于相邻像素中心之间的距离。 当菱形沿线条移动时，其中心完全覆盖的任何像素都将打开。 如果直线经过两个相邻像素中间的一个点，则要打开的像素取决于直线的斜率和相邻像素的方向：水平 (并排) ，或垂直方向 (其他) 上方。

下表总结了这些情况。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">线条 (绝对值) </th>
<th align="left">相邻像素为定向</th>
<th align="left">结果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>斜率 &lt; 1</p>
<div>
 
</div>
或
<div>
 
</div>
斜率 &gt; 1</td>
<td align="left"><p>水平旋转</p></td>
<td align="left"><p>浅菱形左侧顶点处的像素。</p></td>
</tr>
<tr class="even">
<td align="left"><p>斜率 &lt; 1</p>
<div>
 
</div>
或
<div>
 
</div>
斜率 &gt; 1</td>
<td align="left"><p>方向</p></td>
<td align="left"><p>浅菱形的顶部顶点处的像素。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>斜率 = 1</p></td>
<td align="left"><p>水平旋转</p></td>
<td align="left"><p>浅菱形的顶部顶点处的像素。</p></td>
</tr>
<tr class="even">
<td align="left"><p>斜率 = 1</p></td>
<td align="left"><p>方向</p></td>
<td align="left"><p>浅菱形右顶点处的像素。</p></td>
</tr>
</tbody>
</table>

 

菱形约定对于介于-1 和1之间倾斜的线条，每列中的一个像素亮一，在绝对值大于1的行中，每行中有一个像素。 这样一来，修饰线就会呈现出来。

修饰线的起始和结束像素也由菱形约定决定。 修饰线是第一个像素（含）和最后一个像素专用;也就是说，如果线条在像素的菱形内开始，则该像素会亮起。 同样，如果线条在菱形的菱形内结束，则该像素不会亮起。

下图演示了装饰线条的菱形约定。

![阐释装饰线条菱形约定的关系图](images/102-01b.png)

对于呈现修饰线， [**DrvStrokePath**](/windows/desktop/api/winddi/nf-winddi-drvstrokepath) 函数遵循 GIQ 菱形约定。 [**DrvLineTo**](/windows/desktop/api/winddi/nf-winddi-drvlineto)函数是一个可选入口点，驱动程序可以将该入口点提供给 Microsoft Win32 **LineTo**函数的应用程序调用的优化。 **DrvLineTo** 比 **DrvStrokePath** 更简单，因为它仅支持整数终结点和实线修饰直线。

对于支持 R2 \_ 非混合模式的光栅设备，将目标颜色更改为其逆颜色的二元光栅操作，驱动程序必须使用精确的呈现。 对于需要 GDI 和驱动程序呈现的设备，呈现也应是精确的。 这包括在某些位图上绘制 GDI 的设备，驱动程序会在其他图面上绘制 (除非这些像素太小以致) 明显差异。 这还包括请求 GDI 处理复杂剪辑的设备。

 


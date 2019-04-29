---
title: 装饰线条
description: 装饰线条
ms.assetid: eb9651dd-cc77-469f-8441-4bb958bd374d
keywords:
- 线条 WDK GDI、 表面
- GDI WDK Windows 2000 显示、 线、 表面
- 显示的图形驱动程序 WDK Windows 2000，行，修饰
- 绘制 WDK GDI，线、 表面
- 修饰的行 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6dfe54234eba20470d04b46666640ca82c7d19fa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390029"
---
# <a name="cosmetic-lines"></a>装饰线条


## <span id="ddk_cosmetic_lines_gg"></span><span id="DDK_COSMETIC_LINES_GG"></span>


一个*修饰*行始终是一个像素宽和使用纯色画笔来绘制字符。 它基于网格相交量化 (GIQ) 菱形约定，它确定哪些像素应打开要呈现的修饰的行呈现。

下图显示了叠加在矩形网格中，在其中像素都是位于网格交叉点处的行。 若要确定哪些像素应点亮，假设一个菱形，在行中，居中并沿其滑动。 菱形的宽度和高度都完全相等的相邻像素中心之间的距离。 当菱形移动沿该线时，则打开其中心完全覆盖的菱形框任何像素。 要打开的像素行，如果通过一个点中间两个相邻像素之间依赖于行相邻像素都是面向的斜率： 水平 （并行），或垂直 （上面另一个）。

下表总结了这些情况。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">行 （绝对值） 的斜率</th>
<th align="left">相邻像素的方向</th>
<th align="left">结果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>增量的斜率&lt;1</p>
<div>
 
</div>
或
<div>
 
</div>
增量的斜率&gt;1</td>
<td align="left"><p>水平</p></td>
<td align="left"><p>光在钻石的左侧顶点的像素。</p></td>
</tr>
<tr class="even">
<td align="left"><p>增量的斜率&lt;1</p>
<div>
 
</div>
或
<div>
 
</div>
增量的斜率&gt;1</td>
<td align="left"><p>垂直</p></td>
<td align="left"><p>在钻石的顶部顶点上浅色像素。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>增量的斜率 = 1</p></td>
<td align="left"><p>水平</p></td>
<td align="left"><p>在钻石的顶部顶点上浅色像素。</p></td>
</tr>
<tr class="even">
<td align="left"><p>增量的斜率 = 1</p></td>
<td align="left"><p>垂直</p></td>
<td align="left"><p>在钻石的右顶点上浅色像素。</p></td>
</tr>
</tbody>
</table>

 

菱形约定灯行与每个列中的一个像素与大于 1 的绝对值的斜率倾斜之间为-1 和 1，以及每个行的行中的一个像素。 与无间隔这样一来，呈现修饰的行。

菱形约定还取决于开始和结束的像素为单位的修饰的行。 修饰的行是第一个像素含和最后一个像素独占;也就是说，如果在行内一个像素菱形开始，该像素照亮。 同样，如果在行内一个像素菱形结束，则该像素不照亮。

下图演示了修饰的行的菱形约定。

![说明修饰的行的菱形约定的关系图](images/102-01b.png)

用于呈现修饰的行[ **DrvStrokePath** ](https://msdn.microsoft.com/library/windows/hardware/ff556316)函数遵循 GIQ 菱形约定。 [ **DrvLineTo** ](https://msdn.microsoft.com/library/windows/hardware/ff556245)函数是驱动程序可以作为一种优化对 Microsoft Win32 应用程序调用提供的可选入口点**LineTo**函数。 **DrvLineTo**比简单**DrvStrokePath**因为它支持仅整数终结点，并且修饰实线。

光栅支持的设备 R2\_混合模式下，目标颜色更改为及其反转二进制光栅操作，该驱动程序必须使用完全呈现。 呈现也应该是确切都需要通过 GDI 和驱动程序的呈现的设备。 这包括 GDI 绘制一些位图的设备，该驱动程序会在绘制其他表面 （除非像素都是太小，无法进行的任何可见的差异）。 这还包括请求 GDI 来处理复杂的剪辑的设备。

 

 






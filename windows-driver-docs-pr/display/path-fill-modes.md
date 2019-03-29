---
title: 路径填充模式
description: 路径填充模式
ms.assetid: fa1fb4b9-5ed6-44a2-8a9e-0c1c82f5ea39
keywords:
- GDI WDK Windows 2000 显示、 路径、 填充模式
- 图形驱动程序 WDK Windows 2000 显示、 路径、 填充模式
- 绘制 WDK GDI、 路径、 填充模式
- 填充路径 WDK GDI，填充模式
- 路径 WDK GDI，填充模式
- FP_ALTERNATEMODE
- FP_WINDINGMODE
- 备用填充 WDK GDI
- 卷绕填充 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd7e4e0318240210bee2270403b150332ad73ecd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566919"
---
# <a name="path-fill-modes"></a>路径填充模式


## <span id="ddk_path_fill_modes_gg"></span><span id="DDK_PATH_FILL_MODES_GG"></span>


两个填充模式为路径是定义*备用*并*缠绕*。 这两种填充模式使用奇偶规则来确定如何填充闭合的路径。

FP\_ALTERNATEMODE 适用奇偶规则，如下所示： 到某个时间点显然之外封闭路径从封闭路径中的任意起始点绘制线条。 如果在行超过了奇数个路径段，起始点在已关闭的区域内，因此填充区域的一部分。 为偶数的交点意味着该点不是在要填充的区域中。

FP\_WINDINGMODE 考虑不仅数乘以向量跨越该路径的段，但也会考虑每个段的方向。 考虑使用该路径从开始到结束，每个段的方向为隐式指定的点的顺序绘制： 一个段的第一个顶点的作用是"发件人"，并第二个顶点都是"收件人"点。 现在绘制备用模式中所述的相同的任意行。 从零开始，添加另一个用于将超过行，每个"向前"段，并减去另一个用于删除线的每个"反向"段。 （正向和反向基于个段，在任意行的点积。）如果数计算结果为非零值，然后开始点位于填充区域，则计数为零意味着该点之外的填充区域。

下图显示了如何将这两个规则应用于自相交的路径的更复杂的情况。

![说明备用和环绕填充模式的关系图](images/102-03.png)

在交替填充模式中，A 点位于外部，则通过直线线段，时点 B 和 C 为奇数的射线 1 传递，因此因为射线 2 和 3 通过数量为偶数的段。 绕组填充模式中，在点 A 和 C 位于，因为之和 （正值） 的正向和反向 （负） 的直线线段相交叉的其大气，1 和 3 分别不为零，而 B 点之外，是因为之和的正向和反向直线线段ray 2 每当是零。

 

 






---
title: 路径填充模式
description: 路径填充模式
keywords:
- GDI WDK Windows 2000 显示、路径、填充模式
- 图形驱动程序 WDK Windows 2000 显示、路径、填充模式
- 绘制 WDK GDI，路径，填充模式
- 填充路径 WDK GDI，填充模式
- 路径 WDK GDI，填充模式
- FP_ALTERNATEMODE
- FP_WINDINGMODE
- 备用填充 WDK GDI
- 缠绕填充 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 170e9afae2147b29e9009d58f1c627c7fe54a353
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798268"
---
# <a name="path-fill-modes"></a>路径填充模式


## <span id="ddk_path_fill_modes_gg"></span><span id="DDK_PATH_FILL_MODES_GG"></span>


为路径定义的两种填充模式为 *替代* 和 *缠绕*。 这两种填充模式都使用奇数规则来确定如何填充闭合的路径。

FP \_ ALTERNATEMODE 按如下所示应用奇偶规则：从闭合路径中的任何任意开始点绘制一条直线到明显在闭合路径之外的某个点。 如果行跨越奇数个路径段，则起点在闭合区域内，因而是填充区域的一部分。 偶数个交叉点表示该点不在要填充的区域中。

FP \_ WINDINGMODE 不仅考虑矢量跨越路径段的次数，还考虑每个段的方向。 该路径被视为从开始到结束绘制，每个段的方向由其指定点的顺序隐含：段的第一个顶点是 "发件人" 点，第二个顶点是 "to" 点。 现在绘制在备用模式下所述的相同任意行。 从零开始，为行跨越的每个 "前进" 方向段添加一个，并为跨越的每个 "反转" 方向段减去一个。  (正向和反向，则基于段的点积和任意线条 ) 。如果 count 结果为非零值，则起始点在填充区域内;如果计数为零，则表示该点不在填充区域内。

下图显示了如何将这两种规则应用于自交叉路径更复杂的情况。

![说明替代和缠绕填充模式的关系图](images/102-03.png)

在备用填充模式下，点 A 位于内部，因为 ray 1 经过奇数个直线段，而点 B 和 C 位于外部，因为光线2和3通过偶数个段。 在缠绕填充模式下，点 A 和 C 位于内部，这是因为前向前 (正) 并反转 (其射线跨越的负) 行段（分别为1和3）不为零，而点 B 则不为零，而点 B 则为零。

 

 






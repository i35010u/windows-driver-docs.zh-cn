---
title: 多矩阵顶点混合
description: 多矩阵顶点混合
keywords:
- 借贷 WDK Direct3D
- 顶点混合 WDK Direct3D
- Direct3D WDK Windows 2000 显示，顶点混合
- multimatrix 顶点混合 WDK Direct3D
- multimatrix 顶点混合 WDK Direct3D，关于 multimatrix 顶点混合
- 转换 WDK Direct3D
- 皮肤混合 WDK Direct3D
- 混合 WDK Direct3D 的几何
- 混合 WDK Direct3D
- 矩阵顶点混合 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1cb7ec681c4635afa8fbe6fbdfede638c7bfb17b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830641"
---
# <a name="multimatrix-vertex-blending"></a>多矩阵顶点混合


## <span id="ddk_multimatrix_vertex_blending_gg"></span><span id="DDK_MULTIMATRIX_VERTEX_BLENDING_GG"></span>


Multimatrix 顶点混合是一种用平滑混合的外观联接来渲染对象的技术。 虽然这种特定的技术在当前软件中并不常见，但某些平滑外观当前适用于涉及动画字符的大多数游戏。

有多种几何混合技术。 此处所述的方法是一种几何混合形式。 此方法将顶点与分段的已表述模型相结合，从而提高了真实感，减少了多边形计数。 随着每个帧中的联合更改，几何图形管道会更新附近顶点的位置，以在该接头的段之间平稳地混合。 此功能可以在不同于旋转类型（如平移、缩放、shears 或可由4X4 变换矩阵表示的组合）相关的段之间运行。

一般原则是通过混合网格顶点来扩展典型分段字符。

分段模型被视为由每个由变换矩阵定义的段或坐标系统生成。 通常，网格的每个顶点被视为仅属于一个线段。 此模式已经过扩展，使顶点可以在其他段中具有部分成员身份。 两个或多个段间的接合附近的每个顶点都可以有一个外观权重 *Beta 值*，表示它实际属于其他段的比例。

在经典分层建模中使用时，根段不会混合。 它始终是一种严格的主体，因为没有可用于混合的其他转换。 外观权重 Beta 定义为要使用的父坐标系统比例。 如果整个对象完全是严格体，则这将为0.0。

对于未严格附加到父段的那些部分，Beta 将为1.0。 这将作为父段的所占比例的比例下降。 其中必须有一些点，其中包含 1.0 (和 0.0) 才能维护多个段间的几何连续性。

Multimatrix 顶点混合允许通过更新每个顶点的位置来执行平滑的外观混合，无需为每个顶点指定单独的4X4 转换。 它解决了连续平滑表面的常见情况，而且只需要一个额外的值（外观权重 *Beta* --每个顶点），从而将额外的带宽要求降至最低。

指定的顶点位置数据由所有活跃世界矩阵转换，并使用相应的顶点权重将结果混合在一起。

对于顶点中的任何正常情况都执行相同的步骤。 这会生成一个顶点 (，其中包含位置和正常) ，然后将其送入其余的管道，以便进行常规的照明和修剪。 有关更多详细信息，请参阅 [Multimatrix 顶点混合算法](multimatrix-vertex-blending-algorithm.md)。

字符通常可以包含场景中的大部分多边形，这是关键的性能问题。 不能顺利处理平滑的几何管道将会很难处理大部分内容。

而且，可见字符数是场景最常变化的部分。 这会对帧速率协调行为产生严重影响。 对于交互式应用程序，级别帧速率比高平均帧速率更重要，使得有效的字符呈现成为一项非常重要的功能。

转换后必须执行顶点混合。 如果混合未集成到呈现管道，则必须执行两次转换：一次用于外观，一次用于呈现。

如果将顶点混合集成到几何图形管道中，则可以通过对顶点数据进行单个遍历来处理此情况，这使其在带宽有限的情况下与 unblended 的顶点速度一样快。

以下各节提供了 multimatrix 顶点混合的实现细节：

[多矩阵顶点混合算法](multimatrix-vertex-blending-algorithm.md)

[FVF 代码更改](fvf-code-changes.md)

[D3DTRANSFORMSTATE 更改](d3dtransformstate-changes.md)

[D3DRENDERSTATETYPE 更改](d3drenderstatetype-changes.md)

 

 






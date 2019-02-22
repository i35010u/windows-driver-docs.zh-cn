---
title: Multimatrix 顶点值混合处理
description: Multimatrix 顶点值混合处理
ms.assetid: d7348609-324d-4852-b217-4c298b8aaab7
keywords:
- 贷款 WDK Direct3D
- 混合 WDK Direct3D 的顶点
- Direct3D WDK Windows 2000 显示顶点值混合处理
- 混合 WDK Direct3D multimatrix 顶点
- 关于 multimatrix 顶点混合混合 WDK Direct3D multimatrix 顶点
- 转换 WDK Direct3D
- 设置混合 WDK Direct3D 的外观
- 混合 WDK Direct3D 的几何图形
- 混合 WDK Direct3D 的联合
- 矩阵顶点混合 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef426d08b1e3e987abbf4763805faa93a7602eb3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522085"
---
# <a name="multimatrix-vertex-blending"></a>Multimatrix 顶点值混合处理


## <span id="ddk_multimatrix_vertex_blending_gg"></span><span id="DDK_MULTIMATRIX_VERTEX_BLENDING_GG"></span>


Multimatrix 顶点值混合处理是一种技术用于呈现具有顺利混合的外观关节的对象。 尽管此特定方法不是在最新的软件中常见的涉及经过动画处理的字符的大多数游戏当前使用某种类型的外观平滑设置。

有各种混合技术的几何图形。 此处所述的技术是一种形式的几何图形值混合处理。 此技术的分段明确的模型，提供具有降低的多边形计数增加的真实性关节跨混合顶点。 为每个帧中的联合更改，几何管道会更新的位置的附近顶点，若要在该联合的网段之间顺利地混合。 此功能可以操作之间的联合类型而不是旋转，如转换、 缩放、 扭曲或能够用表示 4x4 转换矩阵的任意组合相关的段。

一般原则是扩展的典型的分段的字符通过混合接头网格顶点。

分段的模型将被视为从段或坐标系统的构建，每个定义的转换矩阵。 传统上，网格的每个顶点均被视为属于单个段。 此模式已扩展为允许在其他段中有部分成员身份的顶点。 每个顶点近两个或多个段之间联合可以具有外观权重*Beta 值*，表示依据它实际上属于其他段的比例。

经典的层次结构建模中使用时，根段获取没有值混合处理。 它始终是一个刚体，因为不没有要进行混合与任何其他转换。 Beta 中的外观权重定义为要使用父坐标系统的比例。 如果它是完全的刚体，则为 0.0，在整个对象。

Beta 版将为 1.0 严格附加到父段这些部分。 这将删除到 blend 删除父段的发布内容的比例。 必须使用它们 （和 0.0） 中以维护多个段之间的几何连续性 1.0 某些组的点。

Multimatrix 顶点混合允许值混合处理由更新每个顶点的位置，而无需单独的 4 X 4 转换以指定的每个顶点执行平滑外观。 它解决了常见的情况下连续平滑面并且尚未需要只有一个其他值--外观权重*Beta* -每个顶点，最大程度减少额外的带宽要求。

通过所有活动世界矩阵转换指定的顶点位置数据和混合在一起使用的相应顶点权重的结果。

对于任何正常存在顶点中执行相同的步骤。 这会生成单个顶点 （具有位置并处于正常状态），然后填充到传统的照明和剪辑的管道的其余部分。 有关更多详细信息，请参阅[Multimatrix 顶点混合算法](multimatrix-vertex-blending-algorithm.md)。

字符通常可以包含一个场景中的多边形大部分和关键性能问题。 几何管道无法处理平滑流外观也将有困难的大部分内容。

此外，可见的字符数是在场景的大多数的变化很大组件之一。 这对帧速率调配行为有严重的影响。 对于交互式应用程序级别的帧速率是比高平均帧速率，使呈现一项非常重要功能的有效字符更重要。

必须在转换后执行顶点值混合处理。 如果未集成到呈现管道值混合处理，必须两次执行的转换： 外观设置一次，一次用于呈现。

将集成顶点混合到几何管道允许这种情况下，若要使用单一遍历的顶点数据，这使得它非常快作为混合顶点在带宽有限的情况下处理。

以下部分提供用于 multimatrix 顶点混合实现的详细信息：

[Multimatrix 顶点混合算法](multimatrix-vertex-blending-algorithm.md)

[FVF 代码更改](fvf-code-changes.md)

[D3DTRANSFORMSTATE 更改](d3dtransformstate-changes.md)

[D3DRENDERSTATETYPE 更改](d3drenderstatetype-changes.md)

 

 






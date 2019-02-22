---
title: 顶点雾
description: 顶点雾
ms.assetid: 55083ccb-b93e-4506-baf2-358f90e2c6a6
keywords:
- 顶点雾 WDK Direct3D
- 循环访问的雾 WDK Direct3D
- 本地雾 WDK Direct3D
- 雾化 WDK Direct3D
- D3DRENDERSTATE_FOGENABLE
- 透视更正雾 WDK Direct3D
- 分层 atmosphere 模型 WDK Direct3D
- 颜色雾计算 WDK Direct3D
- D3DPRASTERCAPS_FOGVERTEX
- D3DRENDERSTATE_FOGDENSITY
- D3DRENDERSTATE_FOGCOLOR
- D3DRENDERSTATE_SHADEMODE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a6696a374f48089573141d3084203284d5dea6c4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524013"
---
# <a name="vertex-fog"></a>顶点雾


## <span id="ddk_vertex_fog_gg"></span><span id="DDK_VERTEX_FOG_GG"></span>


使用 D3DRENDERSTATE 启用顶点雾\_FOGENABLE 呈现状态。 顶点雾可角度来看更正。 对于具有大型的多边形的场景，顶点雾不可能更好的选择，因为顶点相差更远。

顶点雾可以使用以下两种方式：

1.  请使用 Direct3D 照明代码使用 D3DVERTEX 结构 （Direct3D SDK 文档中所述） 来定义混合身份雾。

2.  请使用 D3DLVERTEX 或 D3DTLVERTEX 结构 （同时 Direct3D SDK 文档中介绍）。 这可用于执行分层的雾、 基于范围的雾和卷雾等的自定义的模糊效果。

使用与 D3DVERTEX 结构雾时**PRIMCAPS.dwRasterCaps**具有 D3DPRASTERCAPS\_FOGVERTEX 标志设置。 调用个人**IDirect3DDevice7::SetRenderState**方法用于设置 D3DRENDERSTATE\_到 FOGENABLE **TRUE**，和 D3DRENDERSTATE\_24 位 rgb FOGCOLOR颜色。 对于线性雾**IDirect3DDevice7::SetRenderState**方法用于设置 D3DRENDERSTATE\_FOGSTART 和 D3DRENDERSTATE\_FOGEND。 有关指数和指数的平方雾，D3DRENDERSTATE\_FOGDENSITY 呈现状态设置为 D3DLIGHTSTATETYPE。 有关详细信息，请参阅 Direct3D SDK 文档。

时与 D3DTLVERTEX 结构中，使用雾**IDirect3DDevice7::SetRenderState**方法用于设置 D3DRENDERSTATE\_到 FOGENABLE **TRUE**，设置雾中的颜色D3DRENDERSTATE\_FOGCOLOR，并设置 D3DRENDERSTATE\_FOGTABLEMODE 到 D3DFOG\_NONE （这设置 D3DTLVERTEX 结构本身中）。 一团迷雾 blend 系数**f**定义的每个顶点。 这是反射 RGBA alpha 组件。

下图说明了分层的 atmosphere 模型中的海拔高度和雾密度之间的示例关系。

![说明示例关系分层的 atmosphere 模型中的海拔高度和雾密度之间的关系图](images/d3dfig25.png)

混合身份雾计算照明阶段，并放入顶点中的反射颜色值的 alpha 分量。 然后应根据当前的阴影模式设置 D3DRENDERSTATE 插入这\_SHADEMODE 呈现状态。

值混合处理顶点 v1 的因素雾，v2 和 v3 确定通过使用以下计算。

![说明用于顶点 v1、 v2 和 v3 的雾混合因素计算](images/d3dfig8.png)

f1，f2 和 f3 跨基于当前的阴影模式的三角形内插。

新颜色**C**，来自以下公式：

**C = (1-f)\*雾\_颜色 + f \* src\_颜色**

在此公式中，

-   **f**是源内, 插的雾混合身份

-   **雾\_颜色**是当前雾颜色 (由呈现状态 D3DRENDERSTATE 设置\_FOGCOLOR)

-   **src\_颜色**是源内, 插，设置纹理的颜色

如果**f**、 混合因子、 雾为 0.0，则**C**设置为等于雾颜色值。 如果**f**是 1.0 没有任何雾影响。

顶点雾因素是距离的到顶点照相机的位置的函数。 无法通过照相机空间中唯一的 Z 值近似等效于此距离。 对于每个顶点雾我们计算 (X<sub>c</sub>，Y<sub>c</sub>，Z<sub>c</sub>) 通过将转换顶点使用照相机中空间**Mworld\*Mview**然后计算与顶点之间的距离和。

在 RGB 模式下，雾化身份**f**进行缩放，以在范围 0 到 255 之间，并且会写入到的反射高光输出颜色的 alpha 分量。

在负载增加模式下，漫射和反射量组件乘以雾身份**f**和限制在范围 0.0 到 1.0 之间。

 

 






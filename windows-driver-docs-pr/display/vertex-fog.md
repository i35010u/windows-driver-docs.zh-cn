---
title: 顶点雾化
description: 顶点雾化
keywords:
- 顶点雾化 WDK Direct3D
- 迭代雾化 WDK Direct3D
- 本地雾化 WDK Direct3D
- fogging WDK Direct3D
- D3DRENDERSTATE_FOGENABLE
- 透视正确雾化 WDK Direct3D
- 分层氛围模型 WDK Direct3D
- 颜色雾化计算 WDK Direct3D
- D3DPRASTERCAPS_FOGVERTEX
- D3DRENDERSTATE_FOGDENSITY
- D3DRENDERSTATE_FOGCOLOR
- D3DRENDERSTATE_SHADEMODE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 537d40da05d934e5cfcb3ab3c2c6ac5f856a7c0b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825185"
---
# <a name="vertex-fog"></a>顶点雾化


## <span id="ddk_vertex_fog_gg"></span><span id="DDK_VERTEX_FOG_GG"></span>


使用 D3DRENDERSTATE \_ FOGENABLE 呈现状态启用顶点雾化。 可以使顶点雾化正确透视。 对于包含大型多边形的场景，顶点雾化可能不是更好的选择，因为顶点会相差更远。

可以通过两种方式使用顶点雾化：

1.  使用 Direct3D SDK 文档) 中介绍的 D3DVERTEX (结构利用 Direct3D 照明代码，定义雾化混合系数。

2.   (在 Direct3D SDK 文档) 中介绍了如何使用 D3DLVERTEX 或 D3DTLVERTEX 结构。 这对于执行自定义雾化效果非常有用，例如分层雾化、基于范围的雾化和体积雾化。

使用与 D3DVERTEX 结构的雾化时， **PRIMCAPS dwRasterCaps** 设置了 D3DPRASTERCAPS \_ FOGVERTEX 标志。 对 **IDirect3DDevice7：： SetRenderState** 方法的单个调用用于将 D3DRENDERSTATE FOGENABLE 设置 \_ 为 **TRUE**，将 D3DRENDERSTATE FOGCOLOR 设置为 \_ 24 位 RGB 颜色。 对于线性雾化， **IDirect3DDevice7：： SetRenderState** 方法用于设置 D3DRENDERSTATE \_ FOGSTART 和 D3DRENDERSTATE \_ FOGEND。 对于指数和指数平方雾化，D3DRENDERSTATE \_ FOGDENSITY render 状态设置为 D3DLIGHTSTATETYPE。 有关详细信息，请参阅 Direct3D SDK 文档。

当对 D3DTLVERTEX 结构使用雾化时， **IDirect3DDevice7：： SetRenderState** 方法用于将 D3DRENDERSTATE \_ FOGENABLE 设置为 **TRUE**，设置 D3DRENDERSTATE FOGCOLOR 中雾化的颜色， \_ 并将 D3DRENDERSTATE \_ FOGTABLEMODE 设置为 D3DFOG \_ NONE (这是在 D3DTLVERTEX 结构自身) 设置的。 在每个顶点上定义雾化 blend 因子 **f** 。 这是反射 RGBA 的 alpha 分量。

下图显示了分层氛围模型中的海拔和雾化密度之间的一个示例关系。

![说明分层大气模型中海拔和雾化密度间的样本关系的示意图](images/d3dfig25.png)

雾化混合系数在照明阶段计算，位于顶点的反射颜色值的 alpha 分量中。 然后，应根据由 D3DRENDERSTATE SHADEMODE 呈现状态设置的当前底纹模式来将其插值 \_ 。

使用以下计算确定顶点 v1、v2 和 v3 的雾化混合系数。

![阐释顶点 v1、v2 和 v3 的雾化混合系数的计算](images/d3dfig8.png)

按当前的底纹模式，按 f1、f2 和 f3 插在三角形上。

新颜色 **C** 是从以下公式获取的：

**C = (1-f) \* 雾化 \_ 色 + f \* src \_ 颜色**

在此公式中，

-   **f** 为源，内插雾化混合因子

-   **雾化 \_ 颜色** 是当前雾化颜色 (由渲染状态设置的 D3DRENDERSTATE \_FOGCOLOR) 

-   **src \_ 颜色** 是源，内插，纹理颜色

如果 **f**，雾化混合系数为0.0，则 **C** 设置为与雾化颜色相同的值。 如果 **f** 为1.0，则没有雾化效果。

顶点中的雾化因子是从相机位置到顶点的距离的函数。 通过在相机空间中只使用 Z 值，可以逼近此距离。 对于每个顶点的雾化，我们使用 **Mworld \* Mview** 来转换顶点，计算相机空间中 (X <sub>c</sub>，Y <sub>c</sub>，Z <sub>c</sub>) ，然后计算与顶点的距离。

在 RGB 模式下，雾化因子 **f** 缩放为介于0到255之间，并写入到反射输出颜色的 alpha 分量。

在斜向模式下，扩散和反射组件乘以雾化因子 **f** ，并且限制为介于0.0 到1.0 的范围内。

 

 






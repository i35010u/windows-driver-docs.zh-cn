---
title: 像素雾化
description: 像素雾化
keywords:
- 全局雾化 WDK Direct3D
- 表雾化 WDK Direct3D
- 像素雾化 WDK Direct3D
- fogging WDK Direct3D
- 颜色雾化计算 WDK Direct3D
- D3DRENDERSTATE_RANGEFOGENABLE
- D3DRENDERSTATE_FOGCOLOR
- D3DRENDERSTATE_FOGTABLEMODE
- D3DRENDERSTATE_FOGSTART
- RSTATE_FOGEND
- D3DRENDERSTATE_FOGDENSITY
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 483f4648f82dabe620d4691c60e6ff39e9ba7565
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838057"
---
# <a name="pixel-fog"></a>像素雾化


## <span id="ddk_pixel_fog_gg"></span><span id="DDK_PIXEL_FOG_GG"></span>


像素雾化类似于顶点雾化，但雾化混合系数 **f** 是在光栅化时间而不是在光照时计算的。 像素雾化比顶点雾化更准确。 已忽略 Direct3D SDK 文档)  (中所述的 LVERTEX 或 D3DTLVERTEX 结构中指定的雾化混合系数。 像素雾化限制为三个雾化截面梁类型 (线性雾化、指数雾化和指数方雾化) 。

对于像素雾化，硬件执行表查找每个像素插值的深度值。 如果表条目是线性内插的，则无需256表条目。 DirectX 的未来版本可能会为非线性 z 分布提供补偿。 ZFront 和 ZBack 在时间间隔 \[ 0.0，1.0 中的值 \] 。

通过将 **dwPRasterCaps** 设置为 D3DPRASTERCAPS FOGTABLE 来使用像素雾化 \_ 。 **D3DDevice7：： SetRenderState** 方法将 D3DRENDERSTATE \_ FOGENABLE render 状态设置为 **TRUE**; D3DRENDERSTATE FOGCOLOR 将 \_ 状态呈现为24位 RGB; D3DRENDERSTATE \_ FOGTABLEMODE 将状态呈现为 D3DFOG \_ 线性、D3DFOG \_ EXP 或 D3DFOG \_ EXP2 之一。 此处，将根据以下三个渲染状态计算雾化混合系数：

**fStart** 由 RENDER 状态 D3DRENDERSTATE FOGSTART 确定， \_ 其间隔为 \[ 0.0，1.0 \] 。

**防范** 由 RENDER 状态 D3DRENDERSTATE FOGEND 确定， \_ 其间隔为 \[ 0.0，1.0 \] 。

**fDensity** 由 RENDER 状态 D3DRENDERSTATE FOGDENSITY 确定， \_ 其间隔为 \[ 0.0，1.0 \] 。

雾化混合因子 **f** 的计算基于 z 和刚才介绍的三个雾化呈现状态。 实际的计算取决于 render 状态 D3DRENDERSTATE \_ FOGTABLEMODE。 只有 D3DFOGMODE \_ 线性使用雾化开始值和结束值。

-   \_无 D3DFOGMODE

    不应用像素雾化。

-   D3DFOGMODE \_ 线性

    线性雾化增长。

![线性雾化增长计算](images/d3dfig10.png)

-   D3DFOGMODE \_ EXP

    指数雾化增长。

![指数雾化增长计算](images/d3dfig11.png)

-   D3DFOGMODE \_ EXP2

    指数平方雾化增长。

![指数平方雾化增长计算](images/d3dfig12.png)

通常，指数和指数方雾化过于昂贵，无法直接执行。 相反， \[ \] 使用当前雾化密度为间隔0.0、1.0 中的一些 z 值预先计算查找表。 然后，最接近的表项可用于当前 z 值，或者两个周围 z 值之间的插值值可用于获取适当的雾化因子。

最后一个 fogged color **C** 的计算方法与顶点雾化相同，如下所示：

**C = (1-f) \* 雾化 \_ 色 + f \* src \_ 颜色**

在此公式中，

-   **f** 是雾化混合因子

-   **雾化 \_ 颜色** 是当前雾化颜色 (由渲染状态设置的 D3DRENDERSTATE \_FOGCOLOR) 

-   **src \_ 颜色** 是源，内插，纹理颜色

如果 **f**，雾化混合系数为0.0，则最终的 fogged 颜色与雾化颜色完全相同。 如果 **f** 为1.0，则没有雾化效果。

 

 






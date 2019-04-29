---
title: 像素雾化
description: 像素雾化
ms.assetid: 40896f51-87f5-44e9-9199-e92f51a1e8f1
keywords:
- 全局雾 WDK Direct3D
- 表雾 WDK Direct3D
- 像素雾 WDK Direct3D
- 雾化 WDK Direct3D
- 颜色雾计算 WDK Direct3D
- D3DRENDERSTATE_RANGEFOGENABLE
- D3DRENDERSTATE_FOGCOLOR
- D3DRENDERSTATE_FOGTABLEMODE
- D3DRENDERSTATE_FOGSTART
- RSTATE_FOGEND
- D3DRENDERSTATE_FOGDENSITY
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6470a86c19c3c580044cee5a3099d662d2b3e6d6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352267"
---
# <a name="pixel-fog"></a>像素雾化


## <span id="ddk_pixel_fog_gg"></span><span id="DDK_PIXEL_FOG_GG"></span>


像素雾是类似于顶点雾，但混合因子、 雾**f**，在光栅化时，而不是在照明时间计算。 像素雾是比顶点雾更准确。 忽略雾混合 LVERTEX 中指定的身份或 D3DTLVERTEX 结构 （Direct3D SDK 文档中所述）。 像素雾被限制为三个雾配置文件类型 （线性雾、 指数雾和指数平方的雾）。

对于像素雾硬件将执行内插在每个像素的深度值上某个表查找。 没有必要 256 表项如果内插在它们之间以线性方式。 DirectX 的未来版本可能会提供补偿的非线性 z 分发。 ZFront 和 ZBack 间隔中具有值\[0.0，1.0\]。

通过设置使用像素雾**PRIMCAPS.dwPRasterCaps**到 D3DPRASTERCAPS\_FOGTABLE。 **D3DDevice7::SetRenderState**方法设置 D3DRENDERSTATE\_FOGENABLE 呈现到的状态**TRUE**; D3DRENDERSTATE\_FOGCOLOR 呈现为 24 位 RGB; 的状态和D3DRENDERSTATE\_FOGTABLEMODE 状态呈现给一个 D3DFOG\_线性、 D3DFOG\_EXP、 或 D3DFOG\_EXP2。 在这里，混合身份雾是根据计算的三种呈现状态，如下所示：

**fStart**由呈现状态 D3DRENDERSTATE\_FOGSTART 和间隔\[0.0，1.0\]。

**出去闯荡**由呈现状态 D3DRENDERSTATE\_FOGEND 和间隔\[0.0，1.0\]。

**fDensity**由呈现状态 D3DRENDERSTATE\_FOGDENSITY 和间隔\[0.0，1.0\]。

混合身份雾计算**f** z 和刚刚介绍的三个雾呈现状态为基础。 实际的计算取决于呈现状态 D3DRENDERSTATE\_FOGTABLEMODE。 仅 D3DFOGMODE\_线性使用雾开始和结束值。

-   D3DFOGMODE\_NONE

    应用没有像素雾。

-   D3DFOGMODE\_线性

    线性雾增长。

![计算的线性雾增长](images/d3dfig10.png)

-   D3DFOGMODE\_EXP

    指数雾增长。

![计算指数雾增长](images/d3dfig11.png)

-   D3DFOGMODE\_EXP2

    平方的雾呈指数级增长。

![计算指数平方的雾增长](images/d3dfig12.png)

通常情况下，指数和指数平方的雾是过于昂贵而无法直接执行操作。 相反，查找表已经预先计算好的数的 z 值在间隔\[0.0，1.0\]使用当前雾密度。 最接近的表项然后可用于当前的 z 值，或两个周围的 z 值之间的一个 interpolating 值可用于获取相应雾身份。

最后一个上有雾颜色**C**然后计算中与顶点雾相同的方式，如下所示：

**C = (1-f)\*雾\_颜色 + f \* src\_颜色**

在此公式中，

-   **f**是混合身份雾

-   **雾\_颜色**是当前雾颜色 (由呈现状态 D3DRENDERSTATE 设置\_FOGCOLOR)

-   **src\_颜色**是源内, 插，设置纹理的颜色

如果**f**，混合因子、 雾为 0.0，则最终上有雾的颜色等同于雾颜色。 如果**f**为 1.0，没有任何雾影响。

 

 






---
title: 渲染点精灵
description: 渲染点精灵
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，点子画面
- point sprite WDK DirectX 8。0
- 大小 WDK 点子画面
- 点大小 WDK DirectX 8。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0551f3ff193e866dedd9ce7594bec69b496e2172
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783987"
---
# <a name="rendering-point-sprites"></a>渲染点精灵


## <span id="ddk_rendering_point_sprites_gg"></span><span id="DDK_RENDERING_POINT_SPRITES_GG"></span>


屏幕空间的 **P = (X，Y，Z，W)** 的屏幕 **空间大小将作为带有** 以下4个顶点的四边形进行光栅化：

```cpp
(Xâˆ’S/2, Yâˆ’S/2, Z, W)
(X+S/2, Yâˆ’S/2, Z, W)
(Xâˆ’S/2, Y+S/2, Z, W)
(X+S/2, Y+S/2, Z, W)
```

顶点颜色属性在4个顶点的每个顶点上重复，因此，每个点总是用固定颜色呈现。

纹理坐标的分配由 D3DRS \_ POINTSPRITEENABLE 设置控制。 如果 \_ "D3DRS POINTSPRITEENABLE" 设置为 " **FALSE**"，则顶点的纹理坐标会在4个顶点的每个顶点上重复。 如果顶点中不存在纹理坐标，则 (0.0 f，0.0 f，0.0 f，1.0 f) 的默认值用于点 sprite 的角。 如果将 D3DRS \_ POINTSPRITEENABLE 设置为 **TRUE**，则在4个顶点处从左上角开始，在顺时针方向上的纹理坐标设置为：

```cpp
(0.0f, 0.0f)
(1.0f, 0.0f)
(0.0f, 1.0f)
(1.0f, 1.0f)
```

启用剪辑后，将按如下所示剪切点：如果顶点位于 Z 的视图中， (接近或远) ，则不会呈现该点。 如果将点大小考虑到点大小，则完全在 x 或 y 的视区的外部，则不会呈现该点。 将呈现剩余点。 请注意，点位置可能在 x 或 y) 的视区外 (，但仍部分可见。

可能会也可能不会将点正确剪裁到用户定义的剪辑平面。 如果 \_ 未设置 D3DDEVCAPS CLIPPLANESCALEDPOINTS，则仅根据顶点位置将点剪辑到用户定义的剪辑平面，并忽略点大小。 在这种情况下，当顶点位置位于剪辑平面内时，将完全呈现刻度点，并且当顶点位置位于剪辑平面之外时，将被丢弃。 应用程序可以通过将边框几何添加到最大点大小的剪辑平面来防止潜在的 "弹出" 项目。

如果设置了 D3DDEVCAPS \_ CLIPPLANESCALEDPOINTS 位，则缩放后的点将正确剪裁到用户定义的剪辑平面。

请记住，点 sprite 应不依赖于剔除模式或填充模式，这一点很重要。 不管是否有精选或填充模式，都应始终呈现 Point sprite。

此外，在使用平面底纹的点填充模式下，对基元的平面深浅规则进行编译非常重要。 这意味着，基元的第一个顶点会指示该基元的颜色，从而为基元的每个顶点提供颜色。 参考光栅或示例驱动程序的8.0 版不会出现这种情况，它是在版本8.1 中修复的。

 

 






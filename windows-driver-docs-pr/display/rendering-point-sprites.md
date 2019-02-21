---
title: 呈现点 Sprite
description: 呈现点 Sprite
ms.assetid: f2bdfd93-5b79-4f48-87b6-a76847892f5e
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，点 sprite
- 点 sprite WDK DirectX 8.0
- 大小 WDK 点 sprite
- 点大小 WDK DirectX 8.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9430c504da0b70079b6f613fa2222d1a58ca7a38
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541782"
---
# <a name="rendering-point-sprites"></a>呈现点 Sprite


## <span id="ddk_rendering_point_sprites_gg"></span><span id="DDK_RENDERING_POINT_SPRITES_GG"></span>


屏幕空间点**P = （X、 Y、 Z、 W）** 的屏幕空间大小**S**作为具有以下 4 个顶点四边形是光栅化：

```cpp
(Xâˆ’S/2, Yâˆ’S/2, Z, W)
(X+S/2, Yâˆ’S/2, Z, W)
(Xâˆ’S/2, Y+S/2, Z, W)
(X+S/2, Y+S/2, Z, W)
```

重复每 4 个顶点的顶点颜色属性，因此每个点都呈现使用常量的颜色。

纹理坐标的分配受 D3DRS\_POINTSPRITEENABLE 设置。 如果 D3DRS\_POINTSPRITEENABLE 设置为**FALSE**，然后在每个 4 顶点重复的顶点的纹理坐标。 如果没有纹理坐标都位于顶点 （0.0f，0.0f，0.0f，1.0f） 的默认值用于点子画面的角。 如果 D3DRS\_POINTSPRITEENABLE 设置为**TRUE**，然后从左上角开始的纹理坐标处的 4 个顶点，角并沿顺时针方向，出现在缠绕都设置为：

```cpp
(0.0f, 0.0f)
(1.0f, 0.0f)
(0.0f, 1.0f)
(1.0f, 1.0f)
```

启用剪辑后，点剪裁，如下所示：如果顶点 Z （近或远） 中的视图截锥之外，则不会呈现该点。 如果该点，点大小，考虑到完全 x 在视区外或 y，然后在点则不会呈现。 呈现其余的点。 请注意，则可能要在视区外的点位置 (在 x 或 y)，仍可以部分可见。

点可能会或可能不会正确剪裁到用户定义的剪辑平面。 如果 D3DDEVCAPS\_CLIPPLANESCALEDPOINTS 不设置，则点剪辑到用户定义的剪辑平面仅基于顶点位置忽略点大小。 在这种情况下，缩放的点完全呈现时的顶点位置位于剪辑平面，外部剪裁平面的顶点位置时将被丢弃。 应用程序可能会阻止潜在弹出项目，通过将边框几何图形添加到的最大点大小一样大的剪辑平面。

如果 D3DDEVCAPS\_CLIPPLANESCALEDPOINTS 位未设置，则缩放的点正确剪辑到用户定义的剪辑平面。

请务必记住点 sprite，应消除或填充模式没有任何依赖关系。 始终应在点 sprite 呈现而不考虑剔除或填充模式。

也很重要，使用平面明暗度基元类型的规则来编译使用的平面着色入点填充模式。 这意味着第一个顶点的基元类型决定了该基元的颜色，因此基元的每个顶点的颜色。 这是什么不使用参考光栅器或示例驱动程序的 8.0 版时出现和版本 8.1 中修复。

 

 






---
title: 基于范围的雾化
description: 基于范围的雾化
keywords:
- 基于范围的雾化 WDK Direct3D
- fogging WDK Direct3D
- D3DPRASTERCAPS_FOGRANGE
- D3DRENDERSTATE_RANGEFOGENABLE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17a3364412138396c60b12e31ab7d705ddfb0745
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840179"
---
# <a name="range-based-fog"></a>基于范围的雾化


## <span id="ddk_range_based_fog_gg"></span><span id="DDK_RANGE_BASED_FOG_GG"></span>


雾化还可以基于范围。 对于普通 z，或基于深度的雾化，对象可以出现在视图的一侧，但当查看器向下旋转时，对象会消失，因为其 z 值发生变化。

但是，如果雾化基于范围而不是深度，则它不会随查看器就地旋转而变化，如下图所示。

![阐释基于范围的雾化的关系图](images/d3dfig26.png)

可见的对象保持可见，而不考虑旋转。 这对于航班模拟器、水箱游戏和其他应用程序很有吸引力，因为它不需要在查看器旋转时使对象消失并再次出现。

若要将雾化设置为基于范围的， \_ 应设置 D3DPRASTERCAPS FOGRANGE 和 D3DRENDERSTATE \_ RANGEFOGENABLE 呈现状态。 此呈现状态仅适用于 D3DVERTEX 顶点。 当应用程序指定 D3DLVERTEX 或 D3DTLVERTEX 顶点时，应已为范围更正 RGBF 雾化值的 F (雾化) 组件。 Direct3D SDK 文档中定义了 D3DVERTEX、D3DLVERTEX 和 D3DTLVERTEX 结构。

 

 






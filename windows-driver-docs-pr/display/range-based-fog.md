---
title: 基于范围的雾
description: 基于范围的雾
ms.assetid: 6410dd21-bb9d-4985-a765-03898d9b5d0b
keywords:
- 基于范围的雾 WDK Direct3D
- 雾化 WDK Direct3D
- D3DPRASTERCAPS_FOGRANGE
- D3DRENDERSTATE_RANGEFOGENABLE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a2b0df3d84dfebcdd68f0bd4d0492f0dde1be63
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519908"
---
# <a name="range-based-fog"></a>基于范围的雾


## <span id="ddk_range_based_fog_gg"></span><span id="DDK_RANGE_BASED_FOG_GG"></span>


此外可以基于范围的雾。 正常 z 或基于深度，雾对象可以出现在视图中，在端，但然后朝向它旋转该查看器，该对象将消失，返回到雾因为其 z 值发生更改。

但是，如果雾基于范围而不是深度，而不考虑在查看器中的位置，旋转下图中所示。

![说明基于范围的雾的关系图](images/d3dfig26.png)

可见的对象保持不可见，而不管旋转。 这是极具吸引力的飞行模拟器、 罐游戏和其他应用程序是不可取已消失并重新出现距离，而在查看器将旋转的对象。

若要设置雾为基于范围的 D3DPRASTERCAPS\_FOGRANGE 和 D3DRENDERSTATE\_RANGEFOGENABLE 呈现状态应设置。 这呈现状态仅适用于 D3DVERTEX 顶点。 当应用程序指定 D3DLVERTEX 或 D3DTLVERTEX 顶点时，RGBF 雾值 F （模糊） 部分应已更正了范围。 D3DVERTEX、 D3DLVERTEX 和 D3DTLVERTEX 结构 Direct3D SDK 文档中定义。

 

 






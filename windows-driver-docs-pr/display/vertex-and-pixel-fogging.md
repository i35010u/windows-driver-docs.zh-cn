---
title: 顶点和像素雾化
description: 顶点和像素雾化
keywords:
- 象素 fogging WDK Direct3D
- 顶点雾化 WDK Direct3D
- fogging WDK Direct3D
- 线性雾化 WDK Direct3D
- 指数雾化 WDK Direct3D
- 指数方形雾化 WDK Direct3D
- 单色照明 WDK Direct3D
- 颜色雾化计算 WDK Direct3D
- 混合雾化系数 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f838177220939f63ee97efce62b2f70cd38fe08f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798235"
---
# <a name="vertex-and-pixel-fogging"></a>顶点和像素雾化


## <span id="ddk_vertex_and_pixel_fogging_gg"></span><span id="DDK_VERTEX_AND_PIXEL_FOGGING_GG"></span>


雾化具有三个主要的配置文件类型：线性和指数平方。 还有两种主要实现方法：顶点雾化 (也称为 "循环访问" 或 "局部雾化) " 和 "像素雾化" (也称为 "表" 或 "全局雾化) "。

在单色 (斜坡) 照明模式下，只有当雾化颜色为黑色时，雾化才能正常工作。  (如果没有照明，则任何雾化颜色都将起作用，因为雾化呈现为黑色。 ) 雾化可以视为可见性的度量值，越小，雾化效果越大，对象的可见性就越小。

雾化混合系数 **f** 用于所有雾化计算。 它表示雾化颜色与对象颜色的比例。 最终颜色由以下公式确定：

**Color = f \* objColor + (1.0-f) \* fogColor**

因此，雾化混合系数0.0 为完全雾化颜色，雾化混合系数1.0 为完全对象颜色。 通常情况下， **f** 会降低距离。

如下图所示，线性雾化密度随着距离的增加而以线性方式增加。

![说明线性雾化的关系图](images/d3dfig23.png)

这种线性增长不同于指数雾化，其中雾化密度呈指数级增长。 可以按如下所示设置线性雾化配置文件： D3DRENDERSTATE \_ FOGSTART render 状态设置为 ZFront 和 *f* = 1.0; D3DRENDERSTATE \_ FOGEND Render 状态设置为 ZBack， *f* = 0.0。 忽略 D3DRENDERSTATE \_ FOGDENSITY 呈现状态。

 

 






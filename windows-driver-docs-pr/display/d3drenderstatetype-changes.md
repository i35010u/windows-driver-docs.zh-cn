---
title: D3DRENDERSTATETYPE 更改
description: D3DRENDERSTATETYPE 更改
keywords:
- multimatrix 顶点混合 WDK Direct3D、D3DRENDERSTATETYPE
- D3DRENDERSTATETYPE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 63227b5f1b637761832bba9ab7dbce3576e369fd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827325"
---
# <a name="d3drenderstatetype-changes"></a>D3DRENDERSTATETYPE 更改


## <span id="ddk_d3drenderstatetype_changes_gg"></span><span id="DDK_D3DRENDERSTATETYPE_CHANGES_GG"></span>


定义了一个新的呈现状态以启用和控制 multimatrix 顶点混合操作： D3DRENDERSTATE \_ VERTEXBLEND，这在 DIRECTX SDK 文档中进行了介绍。 此呈现状态的值可以是下列 D3DVERTEXBLENDFLAGS 枚举器之一：

-   D3DVBLEND \_ DISABLE (仅使用 D3DTRANSFORMSTATE 世界转换状态指定的世界矩阵 \_) 

-   D3DVBLEND \_ 1WEIGHT 在 D3DTRANSFORMSTATE \_ 世界和 D3DTRANSFORMSTATE \_ WORLD1 转换状态指定的两个世界矩阵之间 (blend) 

-   D3DVBLEND \_ 2WEIGHTS (D3DTRANSFORMSTATE \_ 世界、D3DTRANSFORMSTATE \_ WORLD1 和 D3DTRANSFORMSTATE \_ WORLD2 转换状态指定的三个世界矩阵之间的混合) 

-   D3DVBLEND \_ 3WEIGHTS (D3DTRANSFORMSTATE \_ 世界、D3DTRANSFORMSTATE \_ WORLD1、D3DTRANSFORMSTATE \_ WORLD2 和 D3DTRANSFORMSTATE \_ WORLD3 转换状态指定的四个世界矩阵之间的混合) 

有关 D3DTRANSFORMSTATE \_ WORLD *n* 转换状态的说明，请参阅 DirectX SDK 文档中的 D3DTRANSFORMSTATETYPE。

即使已使用 Direct3D SDK 文档) 中所述的 **IDirect3DDevice7：： SetTransform** (方法定义了其他混合世界矩阵，发布 (也就是在此呈现状态中指定的数字以外的任何矩阵) 权重设置为零。

 

 






---
title: D3DTRANSFORMSTATE 更改
description: D3DTRANSFORMSTATE 更改
keywords:
- multimatrix 顶点混合 WDK Direct3D、D3DTRANSFORMSTATE
- D3DTRANSFORMSTATE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e72c1b7945a60a0c0cab290d6440be9ddee6550b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814497"
---
# <a name="d3dtransformstate-changes"></a>D3DTRANSFORMSTATE 更改


## <span id="ddk_d3dtransformstate_changes_gg"></span><span id="DDK_D3DTRANSFORMSTATE_CHANGES_GG"></span>


Multimatrix 混合还需要指定三个额外的世界变换矩阵。

除了原始世界变换矩阵以外，D3DTRANSFORMSTATE \_ 世界 (可能被视为 "D3DTRANSFORMSTATE \_ WORLD0" ) 、D3DTRANSFORMSTATE \_ 视图和 D3DTRANSFORMSTATE \_ 投影，现已提供以下世界转换矩阵，如 DirectX SDK 文档中所述：

-   D3DTRANSFORMSTATE \_ WORLD1，要混合的第二个矩阵

-   D3DTRANSFORMSTATE \_ WORLD2，要混合的第三个矩阵

-   D3DTRANSFORMSTATE \_ WORLD3，要混合的第四个矩阵

请注意，这些不是在原始 D3DTRANSFORMSTATE 世界之后连续枚举的 \_ 。

不是通过此调用定义但启用了混合的矩阵被视为标识矩阵。

 

 






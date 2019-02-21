---
title: D3DRENDERSTATETYPE 更改
description: D3DRENDERSTATETYPE 更改
ms.assetid: b62bc1f9-b9f1-40f1-aed1-752285adb3c4
keywords:
- 混合 WDK Direct3D，D3DRENDERSTATETYPE multimatrix 顶点
- D3DRENDERSTATETYPE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b5237a7af393297708301b2e504c1112a56e616
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542411"
---
# <a name="d3drenderstatetype-changes"></a>D3DRENDERSTATETYPE 更改


## <span id="ddk_d3drenderstatetype_changes_gg"></span><span id="DDK_D3DRENDERSTATETYPE_CHANGES_GG"></span>


已启用和控制 multimatrix 顶点混合操作到定义新的呈现状态：D3DRENDERSTATE\_VERTEXBLEND，DirectX SDK 文档中所述。 此呈现器状态的值可以是以下 D3DVERTEXBLENDFLAGS 枚举器之一：

-   D3DVBLEND\_禁用 (使用指定的 D3DTRANSFORMSTATE 世界矩阵\_世界转换状态)

-   D3DVBLEND\_1WEIGHT (blend 之间由 D3DTRANSFORMSTATE 指定两个世界矩阵\_世界和 D3DTRANSFORMSTATE\_WORLD1 转换状态)

-   D3DVBLEND\_2WEIGHTS (blend 之间由 D3DTRANSFORMSTATE 指定三个世界矩阵\_WORLD，D3DTRANSFORMSTATE\_WORLD1 和 D3DTRANSFORMSTATE\_WORLD2 转换状态)

-   D3DVBLEND\_3WEIGHTS (blend 之间指定 D3DTRANSFORMSTATE 的四个世界矩阵\_WORLD，D3DTRANSFORMSTATE\_WORLD1、 D3DTRANSFORMSTATE\_WORLD2 和 D3DTRANSFORMSTATE\_WORLD3 转换状态）

有关说明 D3DTRANSFORMSTATE\_世界*n*转换状态，请参阅 D3DTRANSFORMSTATETYPE DirectX SDK 文档。

即使被定义了其他混合世界矩阵**IDirect3DDevice7::SetTransform**方法 （Direct3D SDK 文档中介绍），超出任何矩阵的贡献 （即，权重）在此呈现器状态中指定数目被设置为零。

 

 






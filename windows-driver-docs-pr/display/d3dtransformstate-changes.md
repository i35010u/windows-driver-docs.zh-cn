---
title: D3DTRANSFORMSTATE 更改
description: D3DTRANSFORMSTATE 更改
ms.assetid: 30d895d5-c9c3-4994-a77b-ee9eeec6d8d8
keywords:
- 混合 WDK Direct3D，D3DTRANSFORMSTATE multimatrix 顶点
- D3DTRANSFORMSTATE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f4819b82cfd8a751bc3dbfeeebc42f550f704048
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569287"
---
# <a name="d3dtransformstate-changes"></a>D3DTRANSFORMSTATE 更改


## <span id="ddk_d3dtransformstate_changes_gg"></span><span id="DDK_D3DTRANSFORMSTATE_CHANGES_GG"></span>


Multimatrix 值混合处理还需要三个其他的世界转换矩阵的规范。

除了原始世界转换矩阵，D3DTRANSFORMSTATE\_世界 (这可能会被视为"D3DTRANSFORMSTATE\_WORLD0")，D3DTRANSFORMSTATE\_视图和 D3DTRANSFORMSTATE\_投影，现在有以下的世界转换矩阵，DirectX SDK 文档中所述：

-   D3DTRANSFORMSTATE\_WORLD1，第二个矩阵进行混合

-   D3DTRANSFORMSTATE\_WORLD2，第三个矩阵进行混合

-   D3DTRANSFORMSTATE\_WORLD3，第四个矩阵进行混合

请注意，这些不连续枚举后原始 D3DTRANSFORMSTATE\_世界。

矩阵未定义的此调用，但启用了混合，则假定为默认值为标识矩阵。

 

 






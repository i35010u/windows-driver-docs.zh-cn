---
title: Direct3D 纹理管理
description: Direct3D 纹理管理
ms.assetid: d67ce56b-ed76-413f-b09f-e25400f1ac6d
keywords:
- 纹理管理 WDK Direct3D
- Direct3D WDK Windows 2000 显示，纹理管理
- 纹理管理 WDK Direct3D 纹理管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a65280100a9285f42e5027e2432fa1c69c0b5a5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541804"
---
# <a name="direct3d-texture-management"></a>Direct3D 纹理管理


## <span id="ddk_direct3d_texture_management_gg"></span><span id="DDK_DIRECT3D_TEXTURE_MANAGEMENT_GG"></span>


虽然纹理支持是可选的今天的驱动程序的大部分都是能够支持它。 支持纹理映射的驱动程序必须响应所有 Microsoft Direct3D DDI 中与纹理相关操作的代码。 有关与纹理相关的操作代码的详细信息，请参阅[ **D3DHAL\_DP2OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff545678)。

驱动程序还必须验证使用的纹理阶段状态[ **D3dValidateTextureStageState** ](https://msdn.microsoft.com/library/windows/hardware/ff549064)回调。

以下部分介绍如何驱动程序实现对纹理的支持：

[多个纹理](multiple-textures.md)

[调色板纹理](paletted-textures.md)

[纹理图阵](texture-blitting.md)

[驱动程序管理的纹理](driver-managed-textures.md)

[驱动程序管理资源](driver-managed-resources.md)

 

 






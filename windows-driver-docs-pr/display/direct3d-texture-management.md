---
title: Direct3D 纹理管理
description: Direct3D 纹理管理
ms.assetid: d67ce56b-ed76-413f-b09f-e25400f1ac6d
keywords:
- 纹理管理 WDK Direct3D
- Direct3D WDK Windows 2000 显示，纹理管理
- 纹理管理 WDK Direct3D，关于纹理管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b4f4e8477ed1588a0e5079def31671c578beb4e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839739"
---
# <a name="direct3d-texture-management"></a>Direct3D 纹理管理


## <span id="ddk_direct3d_texture_management_gg"></span><span id="DDK_DIRECT3D_TEXTURE_MANAGEMENT_GG"></span>


尽管纹理支持是可选的，但现在的大多数驱动程序都可以对其进行支持。 支持纹理映射的驱动程序必须对 Microsoft Direct3D DDI 中所有与纹理相关的操作代码做出响应。 有关纹理相关操作代码的详细信息，请参阅[**D3DHAL\_DP2OPERATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ne-d3dhal-_d3dhal_dp2operation)。

驱动程序还必须通过[**D3dValidateTextureStageState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_validatetexturestagestatecb)回调来验证纹理阶段状态。

以下各节介绍了驱动程序如何实现纹理支持：

[多纹理](multiple-textures.md)

[调色板纹理](paletted-textures.md)

[纹理 Blitting](texture-blitting.md)

[驱动程序托管纹理](driver-managed-textures.md)

[驱动程序管理的资源](driver-managed-resources.md)

 

 






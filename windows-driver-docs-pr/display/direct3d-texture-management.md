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
ms.openlocfilehash: 1d60379f9a2fd3b478e253c21ec89c7b44bb336f
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065904"
---
# <a name="direct3d-texture-management"></a>Direct3D 纹理管理


## <span id="ddk_direct3d_texture_management_gg"></span><span id="DDK_DIRECT3D_TEXTURE_MANAGEMENT_GG"></span>


尽管纹理支持是可选的，但现在的大多数驱动程序都可以对其进行支持。 支持纹理映射的驱动程序必须对 Microsoft Direct3D DDI 中所有与纹理相关的操作代码做出响应。 有关与纹理相关的操作代码的详细信息，请参阅 [**D3DHAL \_ DP2OPERATION**](/windows-hardware/drivers/ddi/d3dhal/ne-d3dhal-_d3dhal_dp2operation)。

驱动程序还必须通过 [**D3dValidateTextureStageState**](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_validatetexturestagestatecb) 回调来验证纹理阶段状态。

以下各节介绍了驱动程序如何实现纹理支持：

[多个纹理](multiple-textures.md)

[调色板式纹理](paletted-textures.md)

[纹理位图传送](texture-blitting.md)

[驱动程序管理的纹理](driver-managed-textures.md)

[驱动程序管理的资源](driver-managed-resources.md)

 


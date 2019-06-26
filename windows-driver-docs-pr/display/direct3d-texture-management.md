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
ms.openlocfilehash: ede23899b81c0d4120fd564a3d24c52e64d62dc4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384862"
---
# <a name="direct3d-texture-management"></a>Direct3D 纹理管理


## <span id="ddk_direct3d_texture_management_gg"></span><span id="DDK_DIRECT3D_TEXTURE_MANAGEMENT_GG"></span>


虽然纹理支持是可选的今天的驱动程序的大部分都是能够支持它。 支持纹理映射的驱动程序必须响应所有 Microsoft Direct3D DDI 中与纹理相关操作的代码。 有关与纹理相关的操作代码的详细信息，请参阅[ **D3DHAL\_DP2OPERATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ne-d3dhal-_d3dhal_dp2operation)。

驱动程序还必须验证使用的纹理阶段状态[ **D3dValidateTextureStageState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_validatetexturestagestatecb)回调。

以下部分介绍如何驱动程序实现对纹理的支持：

[多个纹理](multiple-textures.md)

[调色板纹理](paletted-textures.md)

[纹理图阵](texture-blitting.md)

[驱动程序管理的纹理](driver-managed-textures.md)

[驱动程序管理资源](driver-managed-resources.md)

 

 






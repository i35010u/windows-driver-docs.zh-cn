---
title: 调色板式纹理
description: 调色板式纹理
ms.assetid: eac46256-db08-4a9b-aaaf-2bc8a9f30e98
keywords:
- 纹理管理 WDK Direct3D，调色板纹理
- 调色板纹理 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 087b804e25d8336a01ea9a14558fa457d9fe548e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562217"
---
# <a name="paletted-textures"></a>调色板式纹理


## <span id="ddk_paletted_textures_gg"></span><span id="DDK_PALETTED_TEXTURES_GG"></span>


Direct3D 允许与纹理一起使用的调色板。 调色板可以附加到纹理，就像它可以对任何其他 DirectDrawSurface 对象。 若要支持调色板纹理，驱动程序必须响应 D3DDP2OP\_SETPALETTE 和 D3DDP2OP\_UPDATEPALETTE 操作代码中的其实现[ **D3dDrawPrimitives2** ](https://msdn.microsoft.com/library/windows/hardware/ff544704). 这些操作代码后跟[ **D3DHAL\_DP2SETPALETTE** ](https://msdn.microsoft.com/library/windows/hardware/ff545744)并[ **D3DHAL\_DP2UPDATEPALETTE** ](https://msdn.microsoft.com/library/windows/hardware/ff545923)结构，分别，命令流中。 D3DDP2OP\_SETPALETTE 之间创建关联调色板的句柄和图面上的句柄 (已创建的[ **D3dCreateSurfaceEx**](https://msdn.microsoft.com/library/windows/hardware/ff542840))。 更高版本，D3DDP2OP\_UPDATEPALETTE 可以发送多次设置此纹理的调色板条目的值。

 

 






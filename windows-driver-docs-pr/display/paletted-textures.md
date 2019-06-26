---
title: 调色板式纹理
description: 调色板式纹理
ms.assetid: eac46256-db08-4a9b-aaaf-2bc8a9f30e98
keywords:
- 纹理管理 WDK Direct3D，调色板纹理
- 调色板纹理 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 654754328601f3a8e0f8ec05299dab4d2330cd00
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377360"
---
# <a name="paletted-textures"></a>调色板式纹理


## <span id="ddk_paletted_textures_gg"></span><span id="DDK_PALETTED_TEXTURES_GG"></span>


Direct3D 允许与纹理一起使用的调色板。 调色板可以附加到纹理，就像它可以对任何其他 DirectDrawSurface 对象。 若要支持调色板纹理，驱动程序必须响应 D3DDP2OP\_SETPALETTE 和 D3DDP2OP\_UPDATEPALETTE 操作代码中的其实现[ **D3dDrawPrimitives2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb). 这些操作代码后跟[ **D3DHAL\_DP2SETPALETTE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_dp2setpalette)并[ **D3DHAL\_DP2UPDATEPALETTE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_dp2updatepalette)结构，分别，命令流中。 D3DDP2OP\_SETPALETTE 之间创建关联调色板的句柄和图面上的句柄 (已创建的[ **D3dCreateSurfaceEx**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex))。 更高版本，D3DDP2OP\_UPDATEPALETTE 可以发送多次设置此纹理的调色板条目的值。

 

 






---
title: 调色板式纹理
description: 调色板式纹理
ms.assetid: eac46256-db08-4a9b-aaaf-2bc8a9f30e98
keywords:
- 纹理管理 WDK Direct3D，调色板纹理
- 调色板纹理 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b26f160f67ab5f59aa1e31eb9cece0afa7454638
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826059"
---
# <a name="paletted-textures"></a>调色板式纹理


## <span id="ddk_paletted_textures_gg"></span><span id="DDK_PALETTED_TEXTURES_GG"></span>


Direct3D 允许将调色板与纹理一起使用。 调色板可以附加到纹理，就像它可以附加到任何其他 DirectDrawSurface 对象一样。 若要支持调色板纹理，驱动程序必须在[**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)的实现中对 D3DDP2OP\_SETPALETTE 和 D3DDP2OP\_UPDATEPALETTE 操作代码做出响应。 这些操作代码后跟命令流中的[**D3DHAL\_DP2SETPALETTE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2setpalette)和[**D3DHAL\_DP2UPDATEPALETTE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2updatepalette)结构。 D3DDP2OP\_SETPALETTE 在调色板控点和图面控点（已由[**D3dCreateSurfaceEx**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)创建）之间创建关联。 稍后，可以多次发送 D3DDP2OP\_UPDATEPALETTE，为此纹理设置调色板项的值。

 

 






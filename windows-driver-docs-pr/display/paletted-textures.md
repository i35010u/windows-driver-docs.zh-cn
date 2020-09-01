---
title: 调色板式纹理
description: 调色板式纹理
ms.assetid: eac46256-db08-4a9b-aaaf-2bc8a9f30e98
keywords:
- 纹理管理 WDK Direct3D，调色板纹理
- 调色板纹理 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ecfd1fe55ff3804cbbbf4bd0a109ecd1f9a26859
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89064688"
---
# <a name="paletted-textures"></a>调色板式纹理


## <span id="ddk_paletted_textures_gg"></span><span id="DDK_PALETTED_TEXTURES_GG"></span>


Direct3D 允许将调色板与纹理一起使用。 调色板可以附加到纹理，就像它可以附加到任何其他 DirectDrawSurface 对象一样。 若要支持调色板纹理，驱动程序必须 \_ 在 D3dDrawPrimitives2 的实现中对 D3DDP2OP SETPALETTE 和 D3DDP2OP \_ UPDATEPALETTE 操作[**D3dDrawPrimitives2**](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)代码做出响应。 这些操作代码后跟命令流中的 [**D3DHAL \_ DP2SETPALETTE**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2setpalette) 和 [**D3DHAL \_ DP2UPDATEPALETTE**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2updatepalette) 结构。 D3DDP2OP \_ SETPALETTE 在调色板控点和 (已由 [**D3dCreateSurfaceEx**](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)) 创建的图柄之间创建关联。 稍后， \_ 可以多次发送 D3DDP2OP UPDATEPALETTE，为此纹理设置调色板项的值。

 


---
title: 处理轻量 MIP 贴图纹理
description: 处理轻量 MIP 贴图纹理
ms.assetid: f541b046-2937-428c-ab98-eb1020728e04
keywords:
- MIP map 纹理 WDK DirectX 9.0，轻型
- 轻型 MIP map 纹理 WDK DirectX 9。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eb4b15180d2820abc88a8c638990e76a7359768f
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715830"
---
# <a name="handling-lightweight-mip-map-textures"></a>处理轻量 MIP 贴图纹理


## <span id="ddk_handling_lightweight_mip_map_textures_gg"></span><span id="DDK_HANDLING_LIGHTWEIGHT_MIP_MAP_TEXTURES_GG"></span>


由于轻型 MIP 映射纹理的 MIP 子级别是隐式的，并且没有 ([**DD surface \_ \_ LOCAL**](/windows/win32/api/ddrawint/ns-ddrawint-_dd_surface_local)、 [**dd \_ surface \_ GLOBAL**](/windows/win32/api/ddrawint/ns-ddrawint-_dd_surface_global) 和 [**dd \_ Surface \_ **](/windows/win32/api/ddrawint/ns-ddrawint-_dd_surface_more)) 的相应 DirectDraw 面结构，因此，DirectX 9.0 版本驱动程序可以确定 MIP 地图的纹理是否是轻型的，从而避免创建不必要的驱动程序 surface 结构来节省内存。 若要确定 MIP 地图纹理是否为轻型纹理，驱动程序将验证是否 \_ 设置了纹理图面的 DDSCAPSEX ([**DDSCAPS2**](/previous-versions/windows/hardware/drivers/ff550292(v=vs.85))) 结构的**DWCAPS3**成员中的 DDSCAPS3 LIGHTWEIGHTMIPMAP 位。

请注意，DirectX 9.0 中的所有 MIP map 纹理默认情况下均为轻型。

在处理轻型和重型 MIP 地图纹理时，DirectX 9.0 版本驱动程序将遵循以下规则：

-   DirectX 9.0 和更高版本的驱动程序可以接收 D3DDP2OP \_ TEXBLT 操作代码，其中源 mip 地图纹理为重型，目标 mip 地图纹理为轻型，反之亦然。 当然，驱动程序还可以接收 \_ 源和目标 MIP 地图纹理均为轻型的 D3DDP2OP TEXBLT。

-   由于系统内存轻型 MIP 地图纹理仅消耗单个内存面，因此整个 MIP 地图对于顶级表面中的驱动程序可见。 驱动程序从不需要直接从系统内存轻型 MIP 地图纹理执行纹理操作。 此类 MIP 地图纹理只能是 D3DDP2OP TEXBLT 的源 \_ 。

-   下面的 MIP 映射纹理必须为重型，因为与此类纹理相对应的对视频或 [AGP](agp-support.md) 内存的锁定和直接写入可能如下：

    -   呈现器目标
    -   深度模具
    -   动态
    -   供应商格式

    因此，每个子级都需要完整的表面数据结构。

-   由于视频或 AGP 内存轻型 MIP 地图纹理永远不会被锁定或被其他 DDIs （如 [*DdBlt*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_surfcb_blt)）所引用，因此，驱动程序将确定此类 MIP 地图纹理的子级位置。 因此，无需为此类 MIP 地图纹理的子级别 (显式 **fpVidmem** 成员提供 [**DD \_ SURFACE \_ 全局**](/windows/win32/api/ddrawint/ns-ddrawint-_dd_surface_global) 结构) 。

-   驱动程序托管的轻型 MIP 地图纹理还限制为单个表面，并且必须使用 Direct3D 与系统内存轻型 MIP 地图纹理一起使用的相同布局。 请注意，这不会影响 (除了实现成本) ，因为相应的居民 (视频和 AGP) MIP 地图纹理可以具有其自己的特定于实现的布局。

 


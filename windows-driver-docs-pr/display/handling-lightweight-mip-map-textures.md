---
title: 处理轻量 MIP 贴图纹理
description: 处理轻量 MIP 贴图纹理
ms.assetid: f541b046-2937-428c-ab98-eb1020728e04
keywords:
- MIP 映射纹理 WDK DirectX 9.0 中，轻量
- 轻型 MIP 贴图纹理 WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e4dad90cecaf1e112ce8ef0850cf54b07d4325d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323717"
---
# <a name="handling-lightweight-mip-map-textures"></a>处理轻量 MIP 贴图纹理


## <span id="ddk_handling_lightweight_mip_map_textures_gg"></span><span id="DDK_HANDLING_LIGHTWEIGHT_MIP_MAP_TEXTURES_GG"></span>


因为轻型 MIP 贴图纹理 MIP 子级别是隐式的但没有相应的 DirectDraw 图面上结构 ([**DD\_面\_本地**](https://msdn.microsoft.com/library/windows/hardware/ff551733)， [**DD\_图面\_GLOBAL** ](https://msdn.microsoft.com/library/windows/hardware/ff551726)并[ **DD\_面\_详细**](https://msdn.microsoft.com/library/windows/hardware/ff551737))、如果 MIP 贴图纹理是轻量级的这样可以避免创建不必要的驱动程序图面上结构，以节省内存，可以确定 DirectX 9.0 版本驱动程序。 若要确定是否 MIP 贴图纹理是轻量，该驱动程序将验证是否 DDSCAPS3\_LIGHTWEIGHTMIPMAP 位**dwCaps3** DDSCAPSEX 的成员 ([**DDSCAPS2** ](https://msdn.microsoft.com/library/windows/hardware/ff550292))设置纹理图面的结构。

请注意，DirectX 9.0 中的所有 MIP 贴图纹理轻型默认情况下。

DirectX 9.0 版本驱动程序处理轻量和重量级选手 MIP 贴图纹理时遵循下列规则：

-   DirectX 9.0 和更高版本的驱动程序可以接收 D3DDP2OP\_TEXBLT 操作代码在其中源 MIP 贴图纹理是重量级和目标 MIP 贴图纹理是轻型，反之亦然。 当然，该驱动程序还可以接收 D3DDP2OP\_TEXBLT 源和目标 MIP 贴图纹理程。

-   由于系统内存轻型 MIP 贴图纹理会消耗仅内存的单个图面，整个 MIP 映射是对顶级图面中的驱动程序可见。 驱动程序永远不会是执行直接从系统内存轻型 MIP 贴图纹理的纹理操作所必需的。 MIP 贴图纹理只能是 D3DDP2OP 源\_TEXBLT。

-   以下 MIP 贴图的纹理必须是重量级，因为锁和直接写入视频或[AGP](agp-support.md)对应于每个子级的内存而言，可能有此类纹理：

    -   呈现器目标
    -   深度模具
    -   动态
    -   格式化的供应商

    因此，完整图面上的数据结构是要求每个子级。

-   由于视频或 AGP 内存轻型 MIP 贴图纹理永远不会锁定或如引用的其他 DDIs [ *DdBlt*](https://msdn.microsoft.com/library/windows/hardware/ff549205)，该驱动程序确定 MIP 贴图纹理的子项位置。 因此，完整的图面 (显式**fpVidmem**的成员[ **DD\_图面\_全局**](https://msdn.microsoft.com/library/windows/hardware/ff551726)结构) 的此类子级别MIP 贴图纹理不是必需的。

-   管理驱动程序的轻型 MIP 贴图纹理也限制为单个图面，并且必须使用完全相同的布局的 Direct3D 使用轻量 MIP 贴图纹理的系统内存。 请注意，这有任何负面影响 （而不是实现成本），因为相应的居民 (视频和 AGP) MIP 贴图纹理可以有其自己的特定于实现的布局。

 

 






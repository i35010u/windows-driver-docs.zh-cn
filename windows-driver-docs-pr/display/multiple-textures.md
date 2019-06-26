---
title: 多个纹理
description: 多个纹理
ms.assetid: 3c7b4ac7-eabc-442d-aede-a65ee3b6e20c
keywords:
- 纹理管理 WDK Direct3D，多个纹理
- 多个纹理 WDK Direct3D
- 有关多个纹理的多个纹理 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e19b222b688e8b3ad397a5da68963d57e01845eb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372825"
---
# <a name="multiple-textures"></a>多个纹理


## <span id="ddk_multiple_textures_gg"></span><span id="DDK_MULTIPLE_TEXTURES_GG"></span>


Direct3D 驱动程序可以通过使用纹理阶段状态类型 D3DTEXTURESTAGESTATETYPE，DirectX SDK 文档中所述的纹理阶段状态支持同时使用多个纹理。 此类型，要定义和与指定独立的纹理坐标数据集的顶点扩展结合使用的纹理的所有属性。

添加多个纹理支持 Direct3D 驱动程序需要设置的正确功能位 (Cap)，实现混合纹理，并实现[ **D3dValidateTextureStageState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_validatetexturestagestatecb)。

若要符合 DirectX 6.0 及更高版本，驱动程序是需要以正确解析最多八个纹理坐标集，即使该设备只能循环访问和使用的定义中的坐标数**dwFVFCaps**的成员[ **D3DHAL\_D3DEXTENDEDCAPS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_d3dextendedcaps)结构。 驱动程序使用 D3DTSS\_TEXCOORDINDEX 若要获取正确的坐标，若要使用的纹理。

灵活的顶点格式 ([FVF](fvf--flexible-vertex-format-.md)) 允许多个纹理，因为它们可以使顶点结构中传递多个纹理坐标。 然后，将多个纹理混合在一起的迭代过程中并将其应用于几何图形的一段。

由 Direct3D 驱动程序不会再生成纹理句柄。 相反，由 Direct3D 运行时生成纹理句柄。 纹理缓存管理是通过完全 Direct3D 运行时以便到驱动程序，纹理始终显示为来自应用程序本身。 所有纹理状态都发送到中的驱动程序[ **D3dDrawPrimitives2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)命令流。

通过添加多个纹理，混合和纹理筛选的方法也已经改进，从而提供更明确且更多个定义完善的机制，用于混合。 有关这些值混合处理和纹理筛选机制的详细信息，请参阅 Microsoft DirectX SDK 文档。

如果驱动程序设置 D3DDEVCAPS\_SEPARATETEXTUREMEMORIES 标志在**DevCaps** D3DCAPS8 结构的成员，它指示到 DirectX 8.0 及更高版本的应用程序从禁用同时使用多个纹理。 该驱动程序在响应中返回 D3DCAPS8 结构**GetDriverInfo2**查询中所述[报告 DirectX 8.0 样式 Direct3D 功能](reporting-directx-8-0-style-direct3d-capabilities.md)。 此查询的支持中所述[支持 GetDriverInfo2](supporting-getdriverinfo2.md)。

 

 






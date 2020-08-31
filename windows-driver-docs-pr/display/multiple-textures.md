---
title: 多个纹理
description: 多个纹理
ms.assetid: 3c7b4ac7-eabc-442d-aede-a65ee3b6e20c
keywords:
- 纹理管理 WDK Direct3D，多纹理
- 多纹理 WDK Direct3D
- 多纹理 WDK Direct3D，多纹理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 48d48d75340c86bdd2d9d70e5bb12ae733f6a052
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063866"
---
# <a name="multiple-textures"></a>多个纹理


## <span id="ddk_multiple_textures_gg"></span><span id="DDK_MULTIPLE_TEXTURES_GG"></span>


Direct3D 驱动程序可以通过使用 "纹理阶段状态类型 D3DTEXTURESTAGESTATETYPE" 的纹理贴图阶段状态支持同时使用多个纹理，这在 DirectX SDK 文档中进行了介绍。 此类型允许定义纹理的所有属性，并将其与指定独立纹理坐标数据集的顶点扩展结合使用。

为 Direct3D 驱动程序添加多个纹理支持需要将正确的功能位设置 (Cap) ，实现纹理混合，并实现 [**D3dValidateTextureStageState**](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_validatetexturestagestatecb)。

为了符合 DirectX 6.0 和更高版本，驱动程序需要正确分析多达八个纹理坐标集，即使设备只能循环访问并使用[**D3DHAL \_ D3DEXTENDEDCAPS**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_d3dextendedcaps)结构的**dwFVFCaps**成员中定义的坐标数。 驱动程序使用 D3DTSS \_ TEXCOORDINDEX 获取用于纹理的正确坐标。

灵活的顶点格式 ([FVF](fvf--flexible-vertex-format-.md)) 允许多纹理，因为它们可以在顶点结构中传递多个纹理坐标。 然后，可以将多个纹理组合在一起，并将其应用于一段几何。

Direct3D 驱动程序不再生成纹理句柄。 相反，纹理句柄由 Direct3D 运行时生成。 自动完成纹理缓存管理是通过 Direct3D 运行时完成的，因此，对于驱动程序，纹理始终显示为来自应用程序本身。 所有纹理状态都将发送到 [**D3dDrawPrimitives2**](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb) 命令流中的驱动程序。

除了添加多纹理以外，还改进了混合和纹理筛选的方法，以便为混合提供更清晰和更完善的机制。 有关这些混合和纹理筛选机制的详细信息，请参阅 Microsoft DirectX SDK 文档。

如果驱动程序 \_ 在 D3DCAPS8 结构的 **DevCaps** 成员中设置 D3DDEVCAPS SEPARATETEXTUREMEMORIES 标志，则它会向 DirectX 8.0 和更高版本的应用程序指出，使用多个纹理同时禁用了它们。 驱动程序将返回 D3DCAPS8 结构来响应 **GetDriverInfo2** 查询，如 [报告 DirectX 8.0 样式 Direct3D 功能](reporting-directx-8-0-style-direct3d-capabilities.md)中所述。 支持 [GetDriverInfo2](supporting-getdriverinfo2.md)中介绍了此查询的支持。

 


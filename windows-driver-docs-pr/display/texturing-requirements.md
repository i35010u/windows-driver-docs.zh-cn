---
title: 纹理要求
description: 纹理要求
ms.assetid: 5fb64c9e-1c6d-4a8a-9a8f-7d4ed6d5c301
keywords:
- 纹理大小 WDK Direct3D
- 纹理筛选 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f32d40969ee7b2c4462193e3ed985ada9a4e4a37
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384587"
---
# <a name="texturing-requirements"></a>纹理要求


## <span id="ddk_texturing_requirements_gg"></span><span id="DDK_TEXTURING_REQUIREMENTS_GG"></span>


本部分列出了纹理大小和纹理筛选的要求。 此外，还有与纹理相关的要求**IDirect3DDevice7::ValidateDevice**方法。

### <a name="span-idtexturesizesspanspan-idtexturesizesspantexture-sizes"></a><span id="texture_sizes"></span><span id="TEXTURE_SIZES"></span>纹理大小

纹理大小的要求如下：

1.  该驱动程序必须公开通过其最小值和最大的纹理尺寸**dwMinTextureWidth**， **dwMinTextureHeight**， **dwMaxTextureWidth**，以及**dwMaxTextureHeight** D3DDEVICEDESC7 结构的成员。 此结构在 Direct3D SDK 文档中定义。

2.  如果硬件具有其纹理上有纵横比的限制，必须位于该比率**dwMaxTextureAspectRatio** D3DDEVICEDESC7 结构中的成员。

3.  如果设备支持仅纹理维度的 2 的幂，则它必须设置**dwTextureCaps**的成员[ **D3DPRIMCAPS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dcaps/ns-d3dcaps-_d3dprimcaps)为包含结构D3DPTEXTURECAPS\_POW2 标志在相应的基元类型 （行或三角形）。

4.  如果设备可以支持任意大小的二维 (2D) 纹理 （即，不卷或多维数据集纹理） 时为纹理贴图层的纹理寻址模式设置为 D3DTADDRESS\_次固定，为纹理贴图层纹理换行功能禁用 (D3DRENDERSTATE\_包装*n*设置为 0)，和 MIP 映射不是在使用中，则它必须设置 D3DPTEXTURECAPS\_NONPOW2CONDITIONAL 标志。

5.  如果设备仅支持的纹理维度是否相等，则它必须设置**dwTextureCaps**的成员[ **D3DPRIMCAPS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dcaps/ns-d3dcaps-_d3dprimcaps)为包含结构D3DPTEXTURECAPS\_SQUAREONLY 标志在相应的基元类型 （行或三角形）。

如果设备支持不受限制地以外的第一个和第二个要求中所述的任意大小的纹理，则它必须不设置任何第三中, 所述，第四和第五个要求的标志。

### <a name="span-idtexturefilteringspanspan-idtexturefilteringspantexture-filtering"></a><span id="texture_filtering"></span><span id="TEXTURE_FILTERING"></span>纹理筛选

放大和缩小纹理的筛选器必须启用和禁用通过 D3DTSS\_MAGFILTER 和 D3DTSS\_MINFILTER 纹理阶段状态。 此筛选必须不是自动执行在这些状态被禁用时。 详细了解 D3DTSS\_*Xxx*纹理阶段状态，请参阅 Direct3D SDK 文档中的 D3DTEXTURESTAGESTATETYPE 枚举类型。

必须启用和禁用通过 D3DTSS 纹理 MIP 映射\_MIPFILTER 纹理阶段状态。 如果禁用此状态，但作为 MIP 映射创建纹理，设备必须使用 MIP 映射中的，只有最高级别。 此状态下处于禁用状态时，MIP 映射筛选必须执行。

如果设备支持各向异性筛选，必须通过的值导出的最大各向异性级别**dwMaxAnisotropy** D3DDEVICEDESC7 结构 （Direct3D SDK 文档中定义） 中的成员。 此外，设备必须接受从 1 到任何设置**dwMaxAnisotropy** D3DTSS 中\_MAXANISOTROPY 纹理阶段状态。

设备必须能够将所有受支持的筛选器模式下应用于任何受支持的格式的纹理。 例如，如果具有其他纹理格式支持 MIP 映射，则 MIP 映射筛选的 YUV 纹理应该能够执行。

**请注意**   DirectX 9.0 和更高版本的应用程序可以使用枚举中值 D3DSAMPLERSTATETYPE 来控制的采样器与纹理相关渲染状态特征。 在 DirectX 8.0 及更早版本，D3DTEXTURESTAGESTATETYPE 枚举中包含这些采样器状态。 在运行时映射用户模式下采样器状态 (D3DSAMP\_*Xxx*) 到内核模式 D3DTSS\_*Xxx*值，因此驱动程序不需要处理用户模式下采样器状态。 有关 D3DSAMPLERSTATETYPE 详细信息，请参阅最新的 DirectX SDK 文档。

 

### <a name="span-ididirect3ddevice7validatedevicespanspan-ididirect3ddevice7validatedevicespanidirect3ddevice7validatedevice"></a><span id="idirect3ddevice7_validatedevice"></span><span id="IDIRECT3DDEVICE7_VALIDATEDEVICE"></span>IDirect3DDevice7::ValidateDevice

如果设备支持混合操作和单个传递中的操作数的纹理阶段状态的特定组合，则设备必须返回 DD\_确定，通过调用**IDirect3DDevice7::ValidateDevice**方法 (Direct3D SDK 文档中所述） 为每个此类组合。

如果设备不支持的特定组合的混合操作在单个传递中的纹理阶段状态或不支持一个或多个混合操作或操作数，则它必须返回允许的错误代码之一**IDirect3DDevice7::ValidateDevice**方法。 无效值混合处理操作不能以静默方式失败**IDirect3DDevice7::ValidateDevice**方法。

 

 






---
title: 纹理要求
description: 纹理要求
keywords:
- 纹理尺寸 WDK Direct3D
- 纹理筛选 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fdb1312c967cdbcae9ecedcae69ed3a2688cc074
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801807"
---
# <a name="texturing-requirements"></a>纹理要求


## <span id="ddk_texturing_requirements_gg"></span><span id="DDK_TEXTURING_REQUIREMENTS_GG"></span>


本节列出了纹理大小和纹理筛选的要求。 对于 **IDirect3DDevice7：： ValidateDevice** 方法还有与纹理相关的要求。

### <a name="span-idtexture_sizesspanspan-idtexture_sizesspantexture-sizes"></a><span id="texture_sizes"></span><span id="TEXTURE_SIZES"></span>纹理大小

下面是纹理大小的要求：

1.  驱动程序必须通过 D3DDEVICEDESC7 结构的 **dwMinTextureWidth**、 **dwMinTextureHeight**、 **dwMaxTextureWidth** 和 **dwMaxTextureHeight** 成员公开其最小和最大纹理尺寸。 此结构在 Direct3D SDK 文档中定义。

2.  如果硬件在其纹理上具有纵横比限制，则该比率必须存在于 D3DDEVICEDESC7 结构的 **dwMaxTextureAspectRatio** 成员中。

3.  如果设备仅支持作为2的幂的纹理维度，则必须将 [**D3DPRIMCAPS**](/windows-hardware/drivers/ddi/d3dcaps/ns-d3dcaps-_d3dprimcaps)结构的 **dwTextureCaps** 成员设置为包含 \_ (线条或三角形) 的相应基元类型的 D3DPTEXTURECAPS POW2 标志。

4.  如果该设备可以支持二维 (2D) 纹理 (，而不是在纹理阶段的纹理寻址模式设置为 D3DTADDRESS 的情况下，不) 任意大小的卷或多维数据集纹理 \_ ，则会禁用纹理阶段的纹理换行 (D3DRENDERSTATE \_ WRAP *n* 设置为 0) ，并且未使用 MIP 映射，则必须设置 D3DPTEXTURECAPS \_ NONPOW2CONDITIONAL 标志。

5.  如果设备仅支持维度相等的纹理，则必须将 [**D3DPRIMCAPS**](/windows-hardware/drivers/ddi/d3dcaps/ns-d3dcaps-_d3dprimcaps)结构的 **dwTextureCaps** 成员设置为包含 \_ (线条或三角形) 的相应基元类型的 D3DPTEXTURECAPS SQUAREONLY 标志。

如果设备支持任意大小的纹理而不受第一次和第二次要求中描述的限制，则不能设置第三、第四和第五个要求中所述的任何标志。

### <a name="span-idtexture_filteringspanspan-idtexture_filteringspantexture-filtering"></a><span id="texture_filtering"></span><span id="TEXTURE_FILTERING"></span>纹理筛选

必须通过 D3DTSS \_ MAGFILTER 和 D3DTSS \_ MINFILTER 纹理阶段状态启用和禁用放大纹理的筛选器。 禁用这些状态时，不得自动执行此筛选。 有关 D3DTSS \_ *Xxx* 纹理阶段状态的详细信息，请参阅 Direct3D SDK 文档中的 D3DTEXTURESTAGESTATETYPE 枚举类型。

必须通过 D3DTSS \_ MIPFILTER 纹理阶段状态启用和禁用纹理 MIP 映射。 如果此状态为 "已禁用"，但纹理是作为 MIP map 创建的，则设备必须仅使用 MIP map 的顶级。 禁用此状态时，不能执行 MIP 映射筛选。

如果设备支持各向异性筛选，则必须通过 Direct3D SDK 文档) 中定义 (的 D3DDEVICEDESC7 结构的 **dwMaxAnisotropy** 成员值导出最大各向异性级别。 此外，设备必须在 D3DTSS **dwMaxAnisotropy** \_ MAXANISOTROPY 纹理阶段状态中接受从1到 dwMaxAnisotropy 的任何设置。

设备必须能够将所有受支持的筛选器模式应用于任何支持的格式的纹理。 例如，如果支持采用其他纹理格式的 MIP 映射，则应该可以执行 YUV 纹理的 YUV 映射筛选。

**注意**   DirectX 9.0 和更高版本的应用程序可以使用 D3DSAMPLERSTATETYPE 枚举中的值来控制采样器纹理相关呈现器状态的特征。 在 DirectX 8.0 及更早版本中，这些采样器状态包含在 D3DTEXTURESTAGESTATETYPE 枚举中。 运行时将用户模式采样器状态映射 (D3DSAMP \_ *Xxx*) 为内核模式 D3DTSS \_ *Xxx* 值，以便驱动程序无需处理用户模式采样器状态。 有关 D3DSAMPLERSTATETYPE 的详细信息，请参阅最新的 DirectX SDK 文档。

 

### <a name="span-ididirect3ddevice7_validatedevicespanspan-ididirect3ddevice7_validatedevicespanidirect3ddevice7validatedevice"></a><span id="idirect3ddevice7_validatedevice"></span><span id="IDIRECT3DDEVICE7_VALIDATEDEVICE"></span>IDirect3DDevice7::ValidateDevice

如果设备在单个传递中支持纹理阶段状态混合操作和操作数的特定组合，则设备必须 \_ 从对 **IDirect3DDevice7：： ValidateDevice** 方法的调用返回 DD OK， (在 Direct3D SDK 文档) 中对每个此类组合进行了说明。

如果设备不支持单个传递中的纹理阶段状态混合操作的特定组合，或者不支持一个或多个混合操作或操作数，则它必须返回允许用于 **IDirect3DDevice7：： ValidateDevice** 方法的错误代码之一。 无效的混合操作无法以无提示方式将 **IDirect3DDevice7：： ValidateDevice** 方法失败。

 


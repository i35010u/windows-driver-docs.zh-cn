---
title: 明暗度要求
description: 明暗度要求
ms.assetid: 6c4f3dee-a955-4140-8b64-e9289094f530
keywords:
- 明暗度 WDK Direct3D
- 平面着色 WDK Direct3D
- 高氏着色 WDK Direct3D
- 反射突出显示的 WDK Direct3D
- alpha 值混合处理 WDK Direct3D
- 抖动 WDK Windows 2000 显示
- 颜色键 WDK Direct3D
- 透明度 WDK Direct3D
- 混合 WDK Direct3D
- 突出显示 WDK Direct3D
- D3DPRIMCAPS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5d4c8dfbcc11e7d0f6d8e1cd5cec489dcc8767a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544907"
---
# <a name="shading-requirements"></a>明暗度要求


## <span id="ddk_shading_requirements_gg"></span><span id="DDK_SHADING_REQUIREMENTS_GG"></span>


平面着色，高氏着色、 反射照明后，alpha 值混合处理的要求，抖动，以及颜色键如下所示：

### <a name="span-idflatshadingspanspan-idflatshadingspanflat-shading"></a><span id="flat_shading"></span><span id="FLAT_SHADING"></span>平面着色

D3DPSHADECAPS\_COLORFLATRGB 位**dwShadeCap**的成员[ **D3DPRIMCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff549034)结构必须设置为适当的基元类型 （行或三角形） 就可指示该基元类型支持平面着色。

对于除三角形赛事的球迷们的所有基元类型，颜色，反射 （如果支持） 和 alpha 数据来自于每个基元的第一个顶点。 对于三角形赛事的球迷们，使用第二个顶点。 这些颜色中保持不变的整个三角形 （即，不插入它们）。

### <a name="span-idgouraudshadingspanspan-idgouraudshadingspangouraud-shading"></a><span id="gouraud_shading"></span><span id="GOURAUD_SHADING"></span>高氏着色

**DwShadeCaps**的成员[ **D3DPRIMCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff549034)结构必须具有 D3DPSHADECAPS\_COLORGOURAUDRGB 位集为适当的基元类型 （线条或三角形） 以指示支持高氏的内插的颜色。 颜色和反射分量同时以线性方式内插的顶点之间。

所有基元的颜色数据必须使用的基元，顶点间的线性插值，并且必须符合由参考光栅器生成的图像。 此外，所有颜色和 alpha 组件必须以相同方式都插入它们是否存在。 例如，不正确，若要使用的一种颜色的 RGB 组件时使用的 alpha 分量平面着色的 Gouraud 内插。 异常传输通过反射颜色的 alpha 分量雾组件哪些应永远不会是平面的阴影。

循环访问的颜色组件的角度来看更正建议。 请注意，在最新版本中直接 X 参考光栅器已经采取了颜色组件的角度来看更正。 这是考虑到当前测试过程中。

### <a name="span-idspecularhighlightingspanspan-idspecularhighlightingspanspecular-highlighting"></a><span id="specular_highlighting"></span><span id="SPECULAR_HIGHLIGHTING"></span>反射照明后

如果公开突出显示的支持，则一个或两个下列标志必须设置的反射高光**dwShadeCaps**的成员[ **D3DPRIMCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff549034)结构适当的基元类型 （行或三角形）：

-   D3DPSHADECAPS\_必须设置 SPECULARFLATRGB，如果支持平面着色。

-   D3DPSHADECAPS\_必须设置 SPECULARGOURAUDRGB，如果支持高氏着色。

此外，它必须能够启用或禁用通过设置适当的值的 D3DRENDERSTATE 镜面\_SPECULARENABLE 呈现状态。

反射照明后必须是完整的颜色，并且必须能够生成各种可用于呈现器目标的颜色。 单色镜面不足以满足此要求。

D3DPSHADECAPS\_SPECULARFLATMONO 和 D3DPSHADECAPS\_SPECULARGOURAUDMONO 标志将不用于指示单色反射突出显示。 它们仅指示，在负载增加模式下支持反射照明。 可指示适配器支持仅单色反射高光 RGB 模式下没有上限。 如果您的适配器支持仅单色反射高光 RGB 模式下，不应设置 SPECULARFLATRGB 或 SPECULARGOURAUDRGB cap。 与 monomodes，硬件应只需执行内插反射分量的蓝色通道为白色的强度。 这由 D3DRENDERSTATE 控制\_MONOENABLE 呈现状态。

若要正确实现反射高光，另外一系列 interpolants 是必需的。 但是，硬件部件该支持 z 缓冲和值混合处理通常通过可模拟反射高光这样做经过 z 比较函数带有三角形的第二个混合设置为 D3DCMP\_相等 (请参阅中的 D3DCMPFUNC 枚举类型DirectX SDK 文档）。 此第二个阶段执行 blend 将内插的反射高光组件添加到第一次传递; 期间写入的像素值超出了最大值应为白色饱和。

### <a name="span-idalphablendingspanspan-idalphablendingspanalpha-blending"></a><span id="alpha_blending"></span><span id="ALPHA_BLENDING"></span>Alpha 值混合处理

若要公开的 alpha 值混合处理的支持，以下标志必须设置**dwShadeCaps**的成员[ **D3DPRIMCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff549034)结构对相应基元类型 （线条或三角形）：

-   D3DPSHADECAPS\_必须设置 ALPHAFLATBLEND，如果使用 alpha 支持平面着色。

-   D3DPSHADECAPS\_必须设置 ALPHAGOURAUDBLEND，如果高氏着色 alpha 受支持。

如果支持 alpha 值混合处理，则它必须能够启用或禁用通过设置适当的值的 D3DRENDERSTATE\_ALPHABLENDENABLE 呈现状态。

Alpha 值混合处理，或 （从 3D 空间），真正的透明调制传入颜色的值已存在于帧缓冲区中的数据的过程。 此呈现器状态有模式可以设置的 D3DRENDERSTATE\_SRCBLEND 和 D3DRENDERSTATE\_DESTBLEND 呈现状态。

当执行混合操作的 alpha 值不可用时，它必须假设为 1.0 （不透明）。 这是可行的示例与有无 alpha 通道的纹理混合。

如果向其写入结果的像素的目标包含 alpha 通道，从任何 alpha 值混合处理操作所产生的 alpha 值必须写入到该通道，允许正确累积的透明度。

### <a name="span-idditheringspanspan-idditheringspandithering"></a><span id="dithering"></span><span id="DITHERING"></span>抖色

如果针对特定的基元类型 （行或三角形），支持则抖动**dwRasterCaps**的成员[ **D3DPRIMCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff549034)结构必须具有 D3DPRASTERCAPS\_抖动标志设置。 该功能必须通过 D3DRENDERSTATE 可控\_DITHERENABLE 呈现状态。

如果支持抖色，则它可能不默认为始终关闭或始终在。

### <a name="span-idcolorkeyspanspan-idcolorkeyspancolor-key"></a><span id="color_key"></span><span id="COLOR_KEY"></span>颜色键

颜色键与纹理透明度和 D3DPTEXTURECAPS\_透明度 cap (请参阅**dwTextureCaps**的成员[ **D3DPRIMCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff549034)结构）。

用于创建 2D 动画层的颜色键透明度与帧缓冲区中位于其下的颜色替换对象的某些颜色。 该驱动程序应使应用程序可以启用整个场景，颜色键，但仅使用附加的颜色键值，而不是打开颜色键打开和关闭每个面的某些图面上的颜色键。

如果启用颜色抠像 D3DRENDERSTATE\_COLORKEYENABLE 呈现状态设置为**TRUE**和纹理面具有 DDRAWISURF\_HASCKEYSRCBLT 位集

如果启用颜色键 D3DRENDERSTATE\_COLORKEYENABLE 呈现状态设置为**TRUE**和纹理面具有 DDRAWISURF\_HASCKEYSRCBLT 位集。 (请参阅**dwFlags**的成员[ **DD\_图面\_本地**](https://msdn.microsoft.com/library/windows/hardware/ff551733)结构的详细信息。)应用程序创建的纹理表面上使用 DDSD\_CKSRCBLT，然后调用**IDirect3DDevice7::SetRenderState**方法替换 D3DRENDERSTATE\_COLORKEYENABLE 和**TRUE**. 这两种必须满足的色码发生，并且应用程序，必须允许保留的呈现状态 **，则返回 TRUE**所有的时间和仍有选择地使用颜色密钥对的帧的纹理子集 (即，那些具有DDRAWISURF\_HASCKEYSRCBLT 位集)。 负责驱动程序来正确处理此行为。 有关详细信息**IDirect3DDevice7::SetRenderState**，请参阅 Direct3D SDK 文档。

 

 






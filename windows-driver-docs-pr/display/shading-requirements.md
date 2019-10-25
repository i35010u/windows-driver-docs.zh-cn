---
title: 着色要求
description: 着色要求
ms.assetid: 6c4f3dee-a955-4140-8b64-e9289094f530
keywords:
- 底纹 WDK Direct3D
- 平面底纹 WDK Direct3D
- Gouraud 明暗度 WDK Direct3D
- 镜面突出显示 WDK Direct3D
- alpha 混合 WDK Direct3D
- 抖动 WDK Windows 2000 显示
- 颜色密钥 WDK Direct3D
- 透明 WDK Direct3D
- 混合 WDK Direct3D
- 突出显示 WDK Direct3D
- D3DPRIMCAPS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0678a0e7f7e8f6e608ee398caa2220965025d6a6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825729"
---
# <a name="shading-requirements"></a>着色要求


## <span id="ddk_shading_requirements_gg"></span><span id="DDK_SHADING_REQUIREMENTS_GG"></span>


平面底纹、Gouraud 着色、反射高光、alpha 混合、仿色和颜色键的要求如下：

### <a name="span-idflat_shadingspanspan-idflat_shadingspanflat-shading"></a><span id="flat_shading"></span><span id="FLAT_SHADING"></span>平面底纹

[**D3DPRIMCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dcaps/ns-d3dcaps-_d3dprimcaps)结构的**dwShadeCap**成员中的 D3DPSHADECAPS\_COLORFLATRGB 位必须设置为相应的基元类型（线条或三角形），以便指示该基元类型支持平面底纹。

对于除三角形风扇以外的所有基元类型，颜色、镜面（如果支持）和 alpha 数据来自每个基元的第一个顶点。 对于三角形风扇，将使用第二个顶点。 这些颜色在整个三角形中保持不变（即它们不是插值）。

### <a name="span-idgouraud_shadingspanspan-idgouraud_shadingspangouraud-shading"></a><span id="gouraud_shading"></span><span id="GOURAUD_SHADING"></span>Gouraud 底纹

[**D3DPRIMCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dcaps/ns-d3dcaps-_d3dprimcaps)结构的**dwShadeCaps**成员必须为适当的基元类型（线条或三角形）设置 D3DPSHADECAPS\_COLORGOURAUDRGB 位，以指示支持 Gouraud 颜色的内插。 颜色和反射组件都在顶点之间进行了线性内插。

对于所有基元，颜色数据必须在基元的顶点之间使用线性内插，并且必须符合由引用光栅者生成的图像。 此外，所有颜色和 alpha 组件都必须以相同的方式进行插入（如果存在）。 例如，使用单色的 RGB 组件的 Gouraud 内插法时，将平面底纹用于 alpha 分量。 异常是通过反射颜色的 alpha 分量传输雾化组件，此颜色不应为平面着色。

建议对迭代颜色组件进行透视更正。 请注意，最新直接 X 版本中的引用光栅程序已对颜色组件进行透视更正。 在当前的测试过程中考虑到这一点。

### <a name="span-idspecular_highlightingspanspan-idspecular_highlightingspanspecular-highlighting"></a><span id="specular_highlighting"></span><span id="SPECULAR_HIGHLIGHTING"></span>镜面突出显示

如果公开了反射突出显示支持，则必须在[**D3DPRIMCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dcaps/ns-d3dcaps-_d3dprimcaps)结构的**dwShadeCaps**成员中为适当的基元类型（线条或三角形）设置以下一个或两个标志：

-   如果支持平面底纹，则必须设置 D3DPSHADECAPS\_SPECULARFLATRGB。

-   如果支持 Gouraud 底纹，则必须设置 D3DPSHADECAPS\_SPECULARGOURAUDRGB。

此外，还必须能够通过设置 D3DRENDERSTATE\_SPECULARENABLE 呈现状态的适当值，启用或禁用反射突出显示。

反射突出显示必须是完整的颜色，并且必须能够生成可用于呈现器目标的所有颜色范围。 单色镜面突出显示不足以满足此要求。

不会使用 D3DPSHADECAPS\_SPECULARFLATMONO 和 D3DPSHADECAPS\_SPECULARGOURAUDMONO 标志来指示单色反光。 它们仅指示在斜坡模式下支持反射突出显示。 没有上限可指示适配器仅支持 RGB 模式下的单色反射高光。 如果适配器仅支持 RGB 模式下的单色反射高光，则不应设置 SPECULARFLATRGB 或 SPECULARGOURAUDRGB cap。 使用 monomodes，硬件只需将反射组件的蓝色通道插入为白色强度即可。 这由 D3DRENDERSTATE\_MONOENABLE 呈现状态控制。

为了正确实现镜面高光，需要另一组 interpolants。 但是，支持 z 缓冲和混合的硬件部分通常可以通过在将 z 比较函数设置为\_D3DCMP 的情况下执行第二次混合传递来模拟反射高光（请参阅 DirectX SDK 中的 D3DCMPFUNC 枚举类型）。文档）。 此第二个传递会执行混合，将内插反射组件添加到第一次传递期间写入的像素;超出最大值的值应为饱和到白色。

### <a name="span-idalpha_blendingspanspan-idalpha_blendingspanalpha-blending"></a><span id="alpha_blending"></span><span id="ALPHA_BLENDING"></span>Alpha 混合

若要公开对 alpha 混合的支持，必须在[**D3DPRIMCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dcaps/ns-d3dcaps-_d3dprimcaps)结构的**dwShadeCaps**成员中为适当的基元类型（线条或三角形）设置以下标志：

-   如果支持平色着色，则必须设置 D3DPSHADECAPS\_ALPHAFLATBLEND。

-   如果 alpha 支持 Gouraud 底纹，则必须设置 D3DPSHADECAPS\_ALPHAGOURAUDBLEND。

如果支持 alpha 混合，则必须通过设置 D3DRENDERSTATE\_ALPHABLENDENABLE render 状态的适当值，启用或禁用 alpha 混合。

Alpha 混合或真实透明度（从3D 空间）是 modulating 传入颜色的过程，该过程是指帧缓冲区中的数据值。 此呈现状态具有可由 D3DRENDERSTATE\_SRCBLEND 和 D3DRENDERSTATE\_DESTBLEND 呈现状态设置的模式。

当混合操作的 alpha 值不可用时，必须假定其为1.0 （不透明）。 这种情况的一个示例是可以与没有 alpha 通道的纹理混合使用。

如果向其写入生成的像素的目标包含 alpha 通道，则必须将任何 alpha 混合操作生成的 alpha 值写入该通道，以允许对透明度进行适当的累积。

### <a name="span-idditheringspanspan-idditheringspandithering"></a><span id="dithering"></span><span id="DITHERING"></span>抖动

如果在特定基元类型（线条或三角形）上支持抖动，则[**D3DPRIMCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dcaps/ns-d3dcaps-_d3dprimcaps)结构的**dwRasterCaps**成员必须设置 D3DPRASTERCAPS\_仿色标志。 此功能必须通过 D3DRENDERSTATE\_DITHERENABLE 呈现状态进行控制。

如果支持抖动，则它可能不会默认为 "关闭" 或 "始终打开"。

### <a name="span-idcolor_keyspanspan-idcolor_keyspancolor-key"></a><span id="color_key"></span><span id="COLOR_KEY"></span>颜色键

颜色键与纹理透明度和 D3DPTEXTURECAPS\_透明度上限相关（请参阅[**D3DPRIMCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dcaps/ns-d3dcaps-_d3dprimcaps)结构的**dwTextureCaps**成员）。

用于创建 2D sprite 的颜色键透明度将对象的某些颜色替换为帧缓冲区中其下的颜色。 驱动程序应使应用程序能够为整个场景启用颜色键，但仅在特定的表面上使用颜色键，并使用附加的颜色键值，而不是打开和关闭每个图面的颜色键。

如果 D3DRENDERSTATE\_COLORKEYENABLE render 状态设置为**TRUE** ，并且纹理图面具有 DDRAWISURF\_HASCKEYSRCBLT 位集，则启用 Colorkeying

如果 D3DRENDERSTATE\_COLORKEYENABLE render 状态设置为**TRUE** ，并且纹理图面具有 DDRAWISURF\_HASCKEYSRCBLT 位集，则启用颜色键。 （有关详细信息，请参阅[**DD\_SURFACE\_本地**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_surface_local)结构的**dwFlags**成员。）应用程序创建一个使用 DDSD\_CKSRCBLT 的纹理图面，然后调用**IDirect3DDevice7：： SetRenderState**方法和 D3DRENDERSTATE\_COLORKEYENABLE 和**TRUE**。 若要发生颜色键，这两种方法都必须为 true，并且必须允许应用程序将呈现状态**设置为 true** ，并且仍有选择性地为帧纹理的一个子集（即，具有 DDRAWISURF\_的颜色键）。HASCKEYSRCBLT 位集）。 驱动程序由驱动程序正确处理此行为。 有关**IDirect3DDevice7：： SetRenderState**的详细信息，请参阅 Direct3D SDK 文档。

 

 






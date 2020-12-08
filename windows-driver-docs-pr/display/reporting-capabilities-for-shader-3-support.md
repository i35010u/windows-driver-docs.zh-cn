---
title: 报告着色器 3 支持功能
description: 报告着色器 3 支持功能
keywords:
- 着色器 WDK DirectX 9.0，着色器3.0 支持
- 顶点着色器 WDK DirectX 9.0，着色器3.0 支持
- 象素着色器 WDK DirectX 9.0，着色器3.0 支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d41cf8e33c79592fd80c0bdab1bb1f22106c37e9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825711"
---
# <a name="reporting-capabilities-for-shader-3-support"></a>报告着色器 3 支持功能


## <span id="ddk_reporting_capabilities_for_shader_3_support_gg"></span><span id="DDK_REPORTING_CAPABILITIES_FOR_SHADER_3_SUPPORT_GG"></span>


支持像素或顶点着色器版本3.0 及更高版本的显示设备的 DirectX 9.0 版本驱动程序必须指出它支持以下功能：

### <a name="span-idvertex_shader_3_0_and_laterspanspan-idvertex_shader_3_0_and_laterspanvertex-shader-30-and-later"></a><span id="vertex_shader_3_0_and_later"></span><span id="VERTEX_SHADER_3_0_AND_LATER"></span>顶点着色器3.0 及更高版本

如果设备支持顶点着色器3.0 及更高版本，则其驱动程序必须将 D3DCAPS9 结构的成员设置为以下值：

<span id="VS20Caps"></span><span id="vs20caps"></span><span id="VS20CAPS"></span>**VS20Caps**  
设置 D3DVSHADERCAPS2 0 结构的以下成员 \_ ：

**DynamicFlowControlDepth** 设置为24。

**NumTemps** 设置为32。

**StaticFlowControlDepth** 设置为4。

**Cap** 设置为 D3DVS20CAPS \_ 断言而位以指示支持断言而。

<span id="GuardBandLeft__GuardBandTop__GuardBandRight__GuardBandBottom"></span><span id="guardbandleft__guardbandtop__guardbandright__guardbandbottom"></span><span id="GUARDBANDLEFT__GUARDBANDTOP__GUARDBANDRIGHT__GUARDBANDBOTTOM"></span>**GuardBandLeft, GuardBandTop, GuardBandRight, GuardBandBottom**  
将每个设置为8K。

<span id="VertexShaderVersion"></span><span id="vertexshaderversion"></span><span id="VERTEXSHADERVERSION"></span>**VertexShaderVersion**  
设置为3.0。

<span id="MaxVertexShaderConst"></span><span id="maxvertexshaderconst"></span><span id="MAXVERTEXSHADERCONST"></span>**MaxVertexShaderConst**  
设置为256。

<span id="MaxVertexShader30InstructionSlots"></span><span id="maxvertexshader30instructionslots"></span><span id="MAXVERTEXSHADER30INSTRUCTIONSLOTS"></span>**MaxVertexShader30InstructionSlots**  
设置为512。

<span id="RasterCaps"></span><span id="rastercaps"></span><span id="RASTERCAPS"></span>**RasterCaps**  
\_为雾化支持设置 D3DPRASTERCAPS FOGVERTEX 位。

<span id="VertexTextureFilterCaps"></span><span id="vertextexturefiltercaps"></span><span id="VERTEXTEXTUREFILTERCAPS"></span>**VertexTextureFilterCaps**  
设置以下筛选器功能：

D3DPTFILTERCAPS \_ MINFPOINT

D3DPTFILTERCAPS \_ MAGFPOINT

<span id="DevCaps2"></span><span id="devcaps2"></span><span id="DEVCAPS2"></span>**DevCaps2**  
设置 D3DDEVCAPS2 \_ VERTEXELEMENTSCANSHARESTREAMOFFSET 位以指示顶点声明中的顶点元素可以共享同一个流偏移量。

<span id="DeclTypes"></span><span id="decltypes"></span><span id="DECLTYPES"></span>**DeclTypes**  
设置以下位以指示设备支持的顶点数据类型：

D3DDTCAPS \_ UBYTE4

D3DDTCAPS \_ UBYTE4N

D3DDTCAPS \_ SHORT2N

D3DDTCAPS \_ SHORT4N

D3DDTCAPS \_ FLOAT16

D3DDTCAPS \_ FLOAT16

### <a name="span-idpixel_shader_3_0_and_laterspanspan-idpixel_shader_3_0_and_laterspanpixel-shader-30-and-later"></a><span id="pixel_shader_3_0_and_later"></span><span id="PIXEL_SHADER_3_0_AND_LATER"></span>像素着色器3.0 和更高版本

如果设备支持像素着色器3.0 及更高版本，则其驱动程序必须将 D3DCAPS9 结构的成员设置为以下值：

<span id="PS20Caps"></span><span id="ps20caps"></span><span id="PS20CAPS"></span>**PS20Caps**  
设置 D3DPSHADERCAPS2 0 结构的以下成员 \_ ：

**DynamicFlowControlDepth** 设置为24。

**NumTemps** 设置为32。

**StaticFlowControlDepth** 设置为4。

**NumInstructionSlots** 设置为512。

**Cap** 设置为以下位：

D3DPS20CAPS \_ ARBITRARYSWIZZLE 以指示支持任意 swizzles。

D3DPS20CAPS \_ GRADIENTINSTRUCTIONS 以指示支持渐变指令。

D3DPS20CAPS \_ 断言而以指示支持断言而。

D3DPS20CAPS \_ NODEPENDENTREADLIMIT 以指示没有依赖的读取限制。

D3DPS20CAPS \_ NOTEXINSTRUCTIONLIMIT，指出纹理和数学指令组合没有限制。

<span id="MaxTextureWidth__MaxTextureHeight"></span><span id="maxtexturewidth__maxtextureheight"></span><span id="MAXTEXTUREWIDTH__MAXTEXTUREHEIGHT"></span>**MaxTextureWidth, MaxTextureHeight**  
每个设置为4K。

<span id="MaxTextureRepeat"></span><span id="maxtexturerepeat"></span><span id="MAXTEXTUREREPEAT"></span>**MaxTextureRepeat**  
设置为8K。

<span id="MaxAnisotropy"></span><span id="maxanisotropy"></span><span id="MAXANISOTROPY"></span>**MaxAnisotropy**  
设置为16。

<span id="PixelShaderVersion"></span><span id="pixelshaderversion"></span><span id="PIXELSHADERVERSION"></span>**PixelShaderVersion**  
设置为3.0。

<span id="MaxPixelShader30InstructionSlots"></span><span id="maxpixelshader30instructionslots"></span><span id="MAXPIXELSHADER30INSTRUCTIONSLOTS"></span>**MaxPixelShader30InstructionSlots**  
设置为512。

<span id="PrimitiveMiscCaps"></span><span id="primitivemisccaps"></span><span id="PRIMITIVEMISCCAPS"></span>**PrimitiveMiscCaps**  
设置以下位：

D3DPMISCCAPS \_ MASKZ

所有精选模式： D3DPMISCCAPS \_ CULLNONE、D3DPMISCCAPS \_ CULLCW、D3DPMISCCAPS \_ CULLCCW。

D3DPMISCCAPS \_ COLORWRITEENABLE

D3DPMISCCAPS \_ CLIPPLANESCALEDPOINTS

D3DPMISCCAPS \_ CLIPTLVERTS

D3DPMISCCAPS \_ BLENDOP

D3DPMISCCAPS \_ FOGINFVF

<span id="RasterCaps"></span><span id="rastercaps"></span><span id="RASTERCAPS"></span>**RasterCaps**  
设置以下位：

D3DPRASTERCAPS \_ MIPMAPLODBIAS

D3DPRASTERCAPS \_ 各向异性

D3DPRASTERCAPS \_ COLORPERSPECTIVE

D3DPRASTERCAPS \_ SCISSORTEST

完全深度支持： D3DPRASTERCAPS \_ SLOPESCALEDEPTHBIAS、D3DPRASTERCAPS \_ DEPTHBIAS

<span id="ZCmpCaps"></span><span id="zcmpcaps"></span><span id="ZCMPCAPS"></span>**ZCmpCaps**  
为模具、深度和 alpha 测试的一组完整比较设置以下位：

D3DPCMPCAPS \_

D3DPCMPCAPS \_

D3DPCMPCAPS \_ 等于

D3DPCMPCAPS \_ LESSEQUAL

D3DPCMPCAPS \_

D3DPCMPCAPS \_ NOTEQUAL

D3DPCMPCAPS \_ GREATEREQUAL

D3DPCMPCAPS \_ ALWAYS：

<span id="SrcBlendCaps__DestBlendCaps"></span><span id="srcblendcaps__destblendcaps"></span><span id="SRCBLENDCAPS__DESTBLENDCAPS"></span>**SrcBlendCaps, DestBlendCaps**  
设置以下源和目标混合模式，除非注明：

D3DPBLENDCAPS \_ 零

D3DPBLENDCAPS \_

D3DPBLENDCAPS \_ SRCCOLOR

D3DPBLENDCAPS \_ INVSRCCOLOR

D3DPBLENDCAPS \_ SRCALPHA

D3DPBLENDCAPS \_ INVSRCALPHA

D3DPBLENDCAPS \_ DESTALPHA

D3DPBLENDCAPS \_ INVDESTALPHA

D3DPBLENDCAPS \_ DESTCOLOR

D3DPBLENDCAPS \_ INVDESTCOLOR

D3DPBLENDCAPS \_ SRCALPHASAT (未设置 **DestBlendCaps**) 

D3DPBLENDCAPS \_ BOTHSRCALPHA (未设置 **DestBlendCaps**) 

D3DPBLENDCAPS \_ BOTHINVSRCALPHA (未设置 **DestBlendCaps**) 

D3DPBLENDCAPS \_ BLENDFACTOR

<span id="TextureCaps"></span><span id="texturecaps"></span><span id="TEXTURECAPS"></span>**TextureCaps**  
设置以下纹理功能：

D3DPTEXTURECAPS \_ 透视

D3DPTEXTURECAPS \_ TEXREPEATNOTSCALEDBYSIZE

D3DPTEXTURECAPS \_ 投影

D3DPTEXTURECAPS \_ 立方体贴图

D3DPTEXTURECAPS \_ VOLUMEMAP

D3DPTEXTURECAPS \_ MIPMAP

D3DPTEXTURECAPS \_ MIPVOLUMEMAP

D3DPTEXTURECAPS \_ MIPCUBEMAP

<span id="TextureFilterCaps__VolumeTextureFilterCaps__CubeTextureFilterCaps"></span><span id="texturefiltercaps__volumetexturefiltercaps__cubetexturefiltercaps"></span><span id="TEXTUREFILTERCAPS__VOLUMETEXTUREFILTERCAPS__CUBETEXTUREFILTERCAPS"></span>**TextureFilterCaps, VolumeTextureFilterCaps, CubeTextureFilterCaps**  
为每个仅设置以下筛选器功能，其中注明：

D3DPTFILTERCAPS \_ MINFPOINT

D3DPTFILTERCAPS \_ MINFLINEAR

\_ **VolumeTextureFilterCaps** 和 **CUBETEXTUREFILTERCAPS**) 不需要 D3DPTFILTERCAPS MINFANISOTROPIC (

D3DPTFILTERCAPS \_ MIPFPOINT

D3DPTFILTERCAPS \_ MIPFLINEAR

D3DPTFILTERCAPS \_ MAGFPOINT

D3DPTFILTERCAPS \_ MAGFLINEAR

<span id="TextureAddressCaps"></span><span id="textureaddresscaps"></span><span id="TEXTUREADDRESSCAPS"></span>**TextureAddressCaps**  
设置以下纹理地址模式以指示顶点和像素阶段的支持：

D3DPTADDRESSCAPS \_ WRAP

D3DPTADDRESSCAPS \_ 镜像

D3DPTADDRESSCAPS \_ 夹具

D3DPTADDRESSCAPS \_ 边框

D3DPTADDRESSCAPS \_ INDEPENDENTUV

D3DPTADDRESSCAPS \_ MIRRORONCE

<span id="StencilCaps"></span><span id="stencilcaps"></span><span id="STENCILCAPS"></span>**StencilCaps**  
设置以下位以指示支持模具操作：

\_保留 D3DSTENCILCAPS

D3DSTENCILCAPS \_ 零

D3DSTENCILCAPS \_ 替换

D3DSTENCILCAPS \_ INCRSAT

D3DSTENCILCAPS \_ DECRSAT

D3DSTENCILCAPS \_ 反转

D3DSTENCILCAPS \_ 增量

D3DSTENCILCAPS \_ DECR

D3DSTENCILCAPS \_ TWOSIDED

<span id="FVFCaps"></span><span id="fvfcaps"></span><span id="FVFCAPS"></span>**FVFCaps**  
设置 D3DFVFCAPS \_ PSIZE 功能，以指示设备支持每个顶点的点大小。

<span id="TextureCaps"></span><span id="texturecaps"></span><span id="TEXTURECAPS"></span>**TextureCaps**  
指示设备支持完全支持或有条件 nonpow 纹理支持。 有关详细信息，请参阅 [着色器2支持的报告功能](reporting-capabilities-for-shader-2-support.md)。

不得 **设置 D3DPTEXTURECAPS** \_ SQUAREONLY 位。 也就是说，不能将设备限制为仅限正方形纹理。

如果设备支持 [同时呈现到多个目标](rendering-to-multiple-targets-simultaneously.md) (也就是说， **NumSimultaneousRTs** 成员设置为大于 1) ，则其驱动程序必须将 D3DCAPS9 结构的成员设置为以下值：

<span id="PrimitiveMiscCaps"></span><span id="primitivemisccaps"></span><span id="PRIMITIVEMISCCAPS"></span>**PrimitiveMiscCaps**  
设置以下位：

D3DPMISCCAPS \_ INDEPENDENTWRITEMASKS

D3DPMISCCAPS \_ MRTINDEPENDENTBITDEPTHS

D3DPMISCCAPS \_ MRTPOSTPIXELSHADERBLENDING

<span id="MaxUserClipPlanes"></span><span id="maxuserclipplanes"></span><span id="MAXUSERCLIPPLANES"></span>**MaxUserClipPlanes**  
如果支持顶点着色器3.0 和更高版本，则将设置为6。

<span id="DeclTypes"></span><span id="decltypes"></span><span id="DECLTYPES"></span>**DeclTypes**  
如果支持顶点着色器3.0 和更高版本，请设置以下位以指示设备支持的顶点格式：

D3DDTCAPS \_ SHORT2N

D3DDTCAPS \_ SHORT4N

D3DDTCAPS \_ UDEC3

D3DDTCAPS \_ DEC3N

 

 






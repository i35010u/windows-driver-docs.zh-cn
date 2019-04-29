---
title: 报告着色器 3 支持功能
description: 报告着色器 3 支持功能
ms.assetid: 89590647-646c-47ec-a46e-e781b1b9f33e
keywords:
- 着色器 WDK DirectX 9.0，着色器 3.0 支持
- 顶点着色器 WDK DirectX 9.0，着色器 3.0 支持
- 像素着色器 WDK DirectX 9.0，着色器 3.0 支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51e57409a4ef41be2a6dc3b33fdfd3cf56e68dad
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383282"
---
# <a name="reporting-capabilities-for-shader-3-support"></a>报告着色器 3 支持功能


## <span id="ddk_reporting_capabilities_for_shader_3_support_gg"></span><span id="DDK_REPORTING_CAPABILITIES_FOR_SHADER_3_SUPPORT_GG"></span>


显示设备支持像素或顶点着色器版本 3.0 及更高版本的 DirectX 9.0 版本驱动程序必须指示它支持以下功能：

### <a name="span-idvertexshader30andlaterspanspan-idvertexshader30andlaterspanvertex-shader-30-and-later"></a><span id="vertex_shader_3_0_and_later"></span><span id="VERTEX_SHADER_3_0_AND_LATER"></span>顶点着色器 3.0 及更高版本

如果设备支持顶点着色器 3.0 及更高版本，其驱动程序必须设置为以下值 D3DCAPS9 结构的成员：

<span id="VS20Caps"></span><span id="vs20caps"></span><span id="VS20CAPS"></span>**VS20Caps**  
设置以下成员 D3DVSHADERCAPS2\_0 结构：

**DynamicFlowControlDepth**设置为 24。

**NumTemps**设置为 32。

**StaticFlowControlDepth**设置为 4。

**Caps**设置为 D3DVS20CAPS\_断言而位，以指示该断言而受支持。

<span id="GuardBandLeft__GuardBandTop__GuardBandRight__GuardBandBottom"></span><span id="guardbandleft__guardbandtop__guardbandright__guardbandbottom"></span><span id="GUARDBANDLEFT__GUARDBANDTOP__GUARDBANDRIGHT__GUARDBANDBOTTOM"></span>**GuardBandLeft，GuardBandTop，GuardBandRight GuardBandBottom**  
设置为 8 K 的每个。

<span id="VertexShaderVersion"></span><span id="vertexshaderversion"></span><span id="VERTEXSHADERVERSION"></span>**VertexShaderVersion**  
将设置为 3.0。

<span id="MaxVertexShaderConst"></span><span id="maxvertexshaderconst"></span><span id="MAXVERTEXSHADERCONST"></span>**MaxVertexShaderConst**  
设置为 256。

<span id="MaxVertexShader30InstructionSlots"></span><span id="maxvertexshader30instructionslots"></span><span id="MAXVERTEXSHADER30INSTRUCTIONSLOTS"></span>**MaxVertexShader30InstructionSlots**  
将设置为 512。

<span id="RasterCaps"></span><span id="rastercaps"></span><span id="RASTERCAPS"></span>**RasterCaps**  
设置 D3DPRASTERCAPS\_雾支持 FOGVERTEX 位。

<span id="VertexTextureFilterCaps"></span><span id="vertextexturefiltercaps"></span><span id="VERTEXTEXTUREFILTERCAPS"></span>**VertexTextureFilterCaps**  
设置以下筛选器功能：

D3DPTFILTERCAPS\_MINFPOINT

D3DPTFILTERCAPS\_MAGFPOINT

<span id="DevCaps2"></span><span id="devcaps2"></span><span id="DEVCAPS2"></span>**DevCaps2**  
设置 D3DDEVCAPS2\_VERTEXELEMENTSCANSHARESTREAMOFFSET 位指示顶点声明中的顶点元素可以共享相同的流偏移量。

<span id="DeclTypes"></span><span id="decltypes"></span><span id="DECLTYPES"></span>**DeclTypes**  
设置以下的位，以指示设备支持的顶点数据类型：

D3DDTCAPS\_UBYTE4

D3DDTCAPS\_UBYTE4N

D3DDTCAPS\_SHORT2N

D3DDTCAPS\_SHORT4N

D3DDTCAPS\_FLOAT16

D3DDTCAPS\_FLOAT16

### <a name="span-idpixelshader30andlaterspanspan-idpixelshader30andlaterspanpixel-shader-30-and-later"></a><span id="pixel_shader_3_0_and_later"></span><span id="PIXEL_SHADER_3_0_AND_LATER"></span>像素着色器 3.0 及更高版本

如果设备支持像素着色器 3.0 及更高版本，其驱动程序必须设置为以下值 D3DCAPS9 结构的成员：

<span id="PS20Caps"></span><span id="ps20caps"></span><span id="PS20CAPS"></span>**PS20Caps**  
设置以下成员 D3DPSHADERCAPS2\_0 结构：

**DynamicFlowControlDepth**设置为 24。

**NumTemps**设置为 32。

**StaticFlowControlDepth**设置为 4。

**NumInstructionSlots**将设置为 512。

**Caps**设置为以下位：

D3DPS20CAPS\_ARBITRARYSWIZZLE 以指示支持任意 swizzles。

D3DPS20CAPS\_GRADIENTINSTRUCTIONS 以指示支持渐变的说明。

D3DPS20CAPS\_断言而以指示该断言而受支持。

D3DPS20CAPS\_NODEPENDENTREADLIMIT 不依赖于只读限制。

D3DPS20CAPS\_NOTEXINSTRUCTIONLIMIT 表示上的纹理和数学指令组合没有限制。

<span id="MaxTextureWidth__MaxTextureHeight"></span><span id="maxtexturewidth__maxtextureheight"></span><span id="MAXTEXTUREWIDTH__MAXTEXTUREHEIGHT"></span>**MaxTextureWidth, MaxTextureHeight**  
设置为 4 千字节。

<span id="MaxTextureRepeat"></span><span id="maxtexturerepeat"></span><span id="MAXTEXTUREREPEAT"></span>**MaxTextureRepeat**  
将设置为 8k。

<span id="MaxAnisotropy"></span><span id="maxanisotropy"></span><span id="MAXANISOTROPY"></span>**MaxAnisotropy**  
设置为 16。

<span id="PixelShaderVersion"></span><span id="pixelshaderversion"></span><span id="PIXELSHADERVERSION"></span>**PixelShaderVersion**  
将设置为 3.0。

<span id="MaxPixelShader30InstructionSlots"></span><span id="maxpixelshader30instructionslots"></span><span id="MAXPIXELSHADER30INSTRUCTIONSLOTS"></span>**MaxPixelShader30InstructionSlots**  
将设置为 512。

<span id="PrimitiveMiscCaps"></span><span id="primitivemisccaps"></span><span id="PRIMITIVEMISCCAPS"></span>**PrimitiveMiscCaps**  
设置以下位：

D3DPMISCCAPS\_MASKZ

所有的剔除模式：D3DPMISCCAPS\_CULLNONE、 D3DPMISCCAPS\_CULLCW、 D3DPMISCCAPS\_CULLCCW。

D3DPMISCCAPS\_COLORWRITEENABLE

D3DPMISCCAPS\_CLIPPLANESCALEDPOINTS

D3DPMISCCAPS\_CLIPTLVERTS

D3DPMISCCAPS\_BLENDOP

D3DPMISCCAPS\_FOGINFVF

<span id="RasterCaps"></span><span id="rastercaps"></span><span id="RASTERCAPS"></span>**RasterCaps**  
设置以下位：

D3DPRASTERCAPS\_MIPMAPLODBIAS

D3DPRASTERCAPS\_各向异性

D3DPRASTERCAPS\_COLORPERSPECTIVE

D3DPRASTERCAPS\_SCISSORTEST

完整的深度支持：D3DPRASTERCAPS\_SLOPESCALEDEPTHBIAS, D3DPRASTERCAPS\_DEPTHBIAS

<span id="ZCmpCaps"></span><span id="zcmpcaps"></span><span id="ZCMPCAPS"></span>**ZCmpCaps**  
为其设置以下位一套完整的模具、 深度和 alpha 测试比较：

D3DPCMPCAPS\_NEVER

D3DPCMPCAPS\_LESS

D3DPCMPCAPS\_EQUAL

D3DPCMPCAPS\_LESSEQUAL

D3DPCMPCAPS\_GREATER

D3DPCMPCAPS\_NOTEQUAL

D3DPCMPCAPS\_GREATEREQUAL

D3DPCMPCAPS\_始终为：

<span id="SrcBlendCaps__DestBlendCaps"></span><span id="srcblendcaps__destblendcaps"></span><span id="SRCBLENDCAPS__DESTBLENDCAPS"></span>**SrcBlendCaps, DestBlendCaps**  
设置以下源和目标混合模式提到的情况除外：

D3DPBLENDCAPS\_ZERO

D3DPBLENDCAPS\_ONE

D3DPBLENDCAPS\_SRCCOLOR

D3DPBLENDCAPS\_INVSRCCOLOR

D3DPBLENDCAPS\_SRCALPHA

D3DPBLENDCAPS\_INVSRCALPHA

D3DPBLENDCAPS\_DESTALPHA

D3DPBLENDCAPS\_INVDESTALPHA

D3DPBLENDCAPS\_DESTCOLOR

D3DPBLENDCAPS\_INVDESTCOLOR

D3DPBLENDCAPS\_SRCALPHASAT (未设置为**DestBlendCaps**)

D3DPBLENDCAPS\_BOTHSRCALPHA (未设置为**DestBlendCaps**)

D3DPBLENDCAPS\_BOTHINVSRCALPHA (未设置为**DestBlendCaps**)

D3DPBLENDCAPS\_BLENDFACTOR

<span id="TextureCaps"></span><span id="texturecaps"></span><span id="TEXTURECAPS"></span>**TextureCaps**  
设置纹理功能如下：

D3DPTEXTURECAPS\_透视

D3DPTEXTURECAPS\_TEXREPEATNOTSCALEDBYSIZE

D3DPTEXTURECAPS\_预计

D3DPTEXTURECAPS\_CUBEMAP

D3DPTEXTURECAPS\_VOLUMEMAP

D3DPTEXTURECAPS\_MIPMAP

D3DPTEXTURECAPS\_MIPVOLUMEMAP

D3DPTEXTURECAPS\_MIPCUBEMAP

<span id="TextureFilterCaps__VolumeTextureFilterCaps__CubeTextureFilterCaps"></span><span id="texturefiltercaps__volumetexturefiltercaps__cubetexturefiltercaps"></span><span id="TEXTUREFILTERCAPS__VOLUMETEXTUREFILTERCAPS__CUBETEXTUREFILTERCAPS"></span>**TextureFilterCaps，VolumeTextureFilterCaps，CubeTextureFilterCaps**  
除非另有说明每个设置以下筛选器功能：

D3DPTFILTERCAPS\_MINFPOINT

D3DPTFILTERCAPS\_MINFLINEAR

D3DPTFILTERCAPS\_MINFANISOTROPIC (对于不是必需**VolumeTextureFilterCaps**并**CubeTextureFilterCaps**)

D3DPTFILTERCAPS\_MIPFPOINT

D3DPTFILTERCAPS\_MIPFLINEAR

D3DPTFILTERCAPS\_MAGFPOINT

D3DPTFILTERCAPS\_MAGFLINEAR

<span id="TextureAddressCaps"></span><span id="textureaddresscaps"></span><span id="TEXTUREADDRESSCAPS"></span>**TextureAddressCaps**  
设置以下纹理地址模式以指示顶点和像素阶段的支持：

D3DPTADDRESSCAPS\_WRAP

D3DPTADDRESSCAPS\_镜像

D3DPTADDRESSCAPS\_次固定

D3DPTADDRESSCAPS\_边框

D3DPTADDRESSCAPS\_INDEPENDENTUV

D3DPTADDRESSCAPS\_MIRRORONCE

<span id="StencilCaps"></span><span id="stencilcaps"></span><span id="STENCILCAPS"></span>**StencilCaps**  
设置以下的位，以指示对模具操作的支持：

D3DSTENCILCAPS\_KEEP

D3DSTENCILCAPS\_ZERO

D3DSTENCILCAPS\_REPLACE

D3DSTENCILCAPS\_INCRSAT

D3DSTENCILCAPS\_DECRSAT

D3DSTENCILCAPS\_反转

D3DSTENCILCAPS\_INCR

D3DSTENCILCAPS\_DECR

D3DSTENCILCAPS\_TWOSIDED

<span id="FVFCaps"></span><span id="fvfcaps"></span><span id="FVFCAPS"></span>**FVFCaps**  
设置 D3DFVFCAPS\_PSIZE 功能，以指示设备是否支持在每个顶点的点大小。

<span id="TextureCaps"></span><span id="texturecaps"></span><span id="TEXTURECAPS"></span>**TextureCaps**  
指示设备支持在完全支持或条件 nonpow 2 纹理支持。 有关详细信息，请参阅[报告功能的着色器 2 支持](reporting-capabilities-for-shader-2-support.md)。

必须**不**设置 D3DPTEXTURECAPS\_SQUAREONLY 位。 也就是说，设备不能被限制为方形的纹理。

如果设备支持[呈现到多个目标同时](rendering-to-multiple-targets-simultaneously.md)(即**NumSimultaneousRTs**成员设置为大于 1)，其驱动程序必须设置为 D3DCAPS9 结构的成员以下值：

<span id="PrimitiveMiscCaps"></span><span id="primitivemisccaps"></span><span id="PRIMITIVEMISCCAPS"></span>**PrimitiveMiscCaps**  
设置以下位：

D3DPMISCCAPS\_INDEPENDENTWRITEMASKS

D3DPMISCCAPS\_MRTINDEPENDENTBITDEPTHS

D3DPMISCCAPS\_MRTPOSTPIXELSHADERBLENDING

<span id="MaxUserClipPlanes"></span><span id="maxuserclipplanes"></span><span id="MAXUSERCLIPPLANES"></span>**MaxUserClipPlanes**  
如果支持顶点着色器 3.0 及更高版本，则设置为 6。

<span id="DeclTypes"></span><span id="decltypes"></span><span id="DECLTYPES"></span>**DeclTypes**  
设置以下的位，以指示设备支持如果顶点着色器 3.0 及更高版本支持的顶点格式：

D3DDTCAPS\_SHORT2N

D3DDTCAPS\_SHORT4N

D3DDTCAPS\_UDEC3

D3DDTCAPS\_DEC3N

 

 






---
title: 必需的 Direct3D 9 功能
ms.assetid: AE8ED273-2329-4E53-9FCD-5A8E863AED83
description: 用户模式驱动程序访问 Direct3D 9 功能所需的功能。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e2763c79c2274658f469ecc3bcc9286187fdb8fb
ms.sourcegitcommit: f8619f20a0903dd64f8641a5266ecad6df5f1d57
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/29/2020
ms.locfileid: "91423900"
---
# <a name="required-direct3d-9-capabilities"></a>必需的 Direct3D 9 功能


若要使应用程序完全访问 Microsoft Direct3D 版本 9 \_ 1、9 \_ 2 和 9 3 的功能 \_ ，用户模式驱动程序必须公开某些硬件功能。 这些功能用用户模式驱动程序的[*GetCaps*](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_getcaps)函数返回的[**D3DCAPS9**](/windows/win32/api/d3d9caps/ns-d3d9caps-d3dcaps9)结构来表示。 若要指示对功能的支持，驱动程序必须将 **D3DCAPS9** 的这些成员设置为所有各自标志值的按位或。

## <a name="span-idminimum_capabilities_for_direct3d_level_9_1spanspan-idminimum_capabilities_for_direct3d_level_9_1spanspan-idminimum_capabilities_for_direct3d_level_9_1spanminimum-capabilities-for-direct3d-level-9_1"></a><span id="Minimum_capabilities_for_Direct3D_level_9_1"></span><span id="minimum_capabilities_for_direct3d_level_9_1"></span><span id="MINIMUM_CAPABILITIES_FOR_DIRECT3D_LEVEL_9_1"></span>Direct3D level 9 1 的最小功能 \_


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><a href="/windows/win32/api/d3d9caps/ns-d3d9caps-d3dcaps9" data-raw-source="[&lt;strong&gt;D3DCAPS9&lt;/strong&gt;](/windows/win32/api/d3d9caps/ns-d3d9caps-_d3dcaps9)"><strong>D3DCAPS9</strong></a> 成员</th>
<th align="left">标志值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>Caps2</strong></td>
<td align="left"><p>D3DCAPS2_DYNAMICTEXTURES</p>
<p>D3DCAPS2_FULLSCREENGAMMA</p></td>
</tr>
<tr class="even">
<td align="left"><strong>PresentationIntervals</strong></td>
<td align="left"><p>D3DPRESENT_INTERVAL_IMMEDIATE</p>
<p>D3DPRESENT_INTERVAL_ONE</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>PrimitiveMiscCaps</strong></td>
<td align="left"><p>D3DPMISCCAPS_COLORWRITEENABLE</p></td>
</tr>
<tr class="even">
<td align="left"><strong>ShadeCaps</strong></td>
<td align="left"><p>D3DPSHADECAPS_ALPHAGOURAUDBLEND</p>
<p>D3DPSHADECAPS_COLORGOURAUDRGB</p>
<p>D3DPSHADECAPS_FOGGOURAUD</p>
<p>D3DPSHADECAPS_SPECULARGOURAUDRGB</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>TextureFilterCaps</strong></td>
<td align="left"><p>D3DPTFILTERCAPS_MINFLINEAR</p>
<p>D3DPTFILTERCAPS_MINFPOINT</p>
<p>D3DPTFILTERCAPS_MAGFLINEAR</p>
<p>D3DPTFILTERCAPS_MAGFPOINT</p></td>
</tr>
<tr class="even">
<td align="left"><strong>TextureCaps</strong>
<p> (参阅 Note。 ) </p></td>
<td align="left"><p>D3DPTEXTURECAPS_ALPHA</p>
<p>D3DPTEXTURECAPS_CUBEMAP</p>
<p>D3DPTEXTURECAPS_MIPMAP</p>
<p>D3DPTEXTURECAPS_PERSPECTIVE</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>TextureAddressCaps</strong></td>
<td align="left"><p>D3DPTADDRESSCAPS_CLAMP</p>
<p>D3DPTADDRESSCAPS_INDEPENDENTUV</p>
<p>D3DPTADDRESSCAPS_MIRROR</p>
<p>D3DPTADDRESSCAPS_WRAP</p></td>
</tr>
<tr class="even">
<td align="left"><strong>TextureOpCaps</strong></td>
<td align="left"><p>D3DTEXOPCAPS_DISABLE</p>
<p>D3DTEXOPCAPS_MODULATE</p>
<p>D3DTEXOPCAPS_SELECTARG1</p>
<p>D3DTEXOPCAPS_SELECTARG2</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>SrcBlendCaps</strong></td>
<td align="left"><p>D3DPBLENDCAPS_INVDESTALPHA</p>
<p>D3DPBLENDCAPS_INVDESTCOLOR</p>
<p>D3DPBLENDCAPS_INVSRCALPHA</p>
<p>D3DPBLENDCAPS_ONE</p>
<p>D3DPBLENDCAPS_SRCALPHA</p>
<p>D3DPBLENDCAPS_ZERO</p></td>
</tr>
<tr class="even">
<td align="left"><strong>DestBlendCaps</strong></td>
<td align="left"><p>D3DPBLENDCAPS_ONE</p>
<p>D3DPBLENDCAPS_INVSRCALPHA</p>
<p>D3DPBLENDCAPS_INVSRCCOLOR</p>
<p>D3DPBLENDCAPS_SRCALPHA</p>
<p>D3DPBLENDCAPS_ZERO</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>StretchRectFilterCaps</strong></td>
<td align="left"><p>D3DPTFILTERCAPS_MAGFLINEAR</p>
<p>D3DPTFILTERCAPS_MAGFPOINT</p>
<p>D3DPTFILTERCAPS_MINFLINEAR</p>
<p>D3DPTFILTERCAPS_MINFPOINT</p></td>
</tr>
<tr class="even">
<td align="left"><strong>ZCmpCaps</strong></td>
<td align="left"><p>D3DPCMPCAPS_ALWAYS</p>
<p>D3DPCMPCAPS_LESSEQUAL</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>RasterCaps</strong></td>
<td align="left"><p>D3DPRASTERCAPS_DEPTHBIAS</p>
<p>D3DPRASTERCAPS_SLOPESCALEDEPTHBIAS</p></td>
</tr>
<tr class="even">
<td align="left"><strong>StencilCaps</strong></td>
<td align="left"><p>D3DSTENCILCAPS_TWOSIDED</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>MaxTextureWidth</strong></td>
<td align="left"><p>2048</p></td>
</tr>
<tr class="even">
<td align="left"><strong>MaxTextureHeight</strong></td>
<td align="left"><p>2048</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>NumSimultaneousRTs</strong></td>
<td align="left"><p>1</p></td>
</tr>
<tr class="even">
<td align="left"><strong>MaxSimultaneousTextures</strong></td>
<td align="left"><p>8</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>MaxTextureBlendStages</strong></td>
<td align="left"><p>8</p></td>
</tr>
<tr class="even">
<td align="left"><strong>PixelShaderVersion</strong></td>
<td align="left"><p>D3DPS_VERSION (2，0) </p></td>
</tr>
<tr class="odd">
<td align="left"><strong>MaxPrimitiveCount</strong></td>
<td align="left"><p>65535</p></td>
</tr>
<tr class="even">
<td align="left"><strong>MaxVertexIndex</strong></td>
<td align="left"><p>65534</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>MaxVolumeExtent</strong></td>
<td align="left"><p>256</p></td>
</tr>
<tr class="even">
<td align="left"><strong>MaxTextureRepeat</strong></td>
<td align="left"><p>必须为零、128或更大。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>MaxAnisotropy</strong></td>
<td align="left"><p>2</p></td>
</tr>
<tr class="even">
<td align="left"><strong>MaxVertexW</strong></td>
<td align="left"><p>0. f</p></td>
</tr>
</tbody>
</table>

 

**注意**  这些要求也适用：
-   驱动程序还必须将 **TextureCaps** 成员设置为值 D3DPTEXTURECAPS \_ NONPOW2CONDITIONAL 和 D3DPTEXTURECAPS \_ POW2，或设置为二者都不是。
-   当驱动程序响应某个事件时，其中 [**D3DDDIARG \_ servicecontext.createquery**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_createquery)。**QueryType** 是 D3DDDIQUERYTYPE \_ 事件，响应时，必须始终将事件的 **布尔** 值设置为 **TRUE** 。 请参阅 [*servicecontext.createquery*](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createquery) 和 **D3DDDIARG \_ servicecontext.createquery**。

 

## <a name="span-idminimum_capabilities_for_direct3d_level_9_2spanspan-idminimum_capabilities_for_direct3d_level_9_2spanspan-idminimum_capabilities_for_direct3d_level_9_2spanminimum-capabilities-for-direct3d-level-9_2"></a><span id="Minimum_capabilities_for_Direct3D_level_9_2"></span><span id="minimum_capabilities_for_direct3d_level_9_2"></span><span id="MINIMUM_CAPABILITIES_FOR_DIRECT3D_LEVEL_9_2"></span>Direct3D 级别 9 2 的最小功能 \_


除了为 Direct3D level 9 1 列出的功能外，这些功能必须设置 \_ 。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><a href="/windows/win32/api/d3d9caps/ns-d3d9caps-d3dcaps9" data-raw-source="[&lt;strong&gt;D3DCAPS9&lt;/strong&gt;](/windows/win32/api/d3d9caps/ns-d3d9caps-_d3dcaps9)"><strong>D3DCAPS9</strong></a> 成员</th>
<th align="left">标志值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>PrimitiveMiscCaps</strong></td>
<td align="left"><p>D3DPMISCCAPS_SEPARATEALPHABLEND</p></td>
</tr>
<tr class="even">
<td align="left"><strong>DevCaps2</strong></td>
<td align="left"><p>D3DDEVCAPS2_VERTEXELEMENTSCANSHARESTREAMOFFSET</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>TextureAddressCaps</strong></td>
<td align="left"><p>D3DPTADDRESSCAPS_MIRRORONCE</p></td>
</tr>
<tr class="even">
<td align="left"><strong>VolumeTextureAddressCaps</strong></td>
<td align="left"><p>D3DPTADDRESSCAPS_MIRRORONCE</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>MaxTextureWidth</strong></td>
<td align="left"><p>2048</p></td>
</tr>
<tr class="even">
<td align="left"><strong>MaxTextureHeight</strong></td>
<td align="left"><p>2048</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>MaxTextureRepeat</strong></td>
<td align="left"><p>必须为零、2048或更大。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>VertexShaderVersion</strong></td>
<td align="left"><p>D3DVS_VERSION (2，0) </p></td>
</tr>
<tr class="odd">
<td align="left"><strong>MaxAnisotropy</strong></td>
<td align="left"><p>16</p></td>
</tr>
<tr class="even">
<td align="left"><strong>MaxPrimitiveCount</strong></td>
<td align="left"><p>1048575</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>MaxVertexIndex</strong></td>
<td align="left"><p>1048575</p></td>
</tr>
<tr class="even">
<td align="left"><strong>MaxVertexW</strong></td>
<td align="left"><p>10000000000</p></td>
</tr>
</tbody>
</table>

 

**注意**  此要求也适用：
-   当驱动程序响应 *z*测试查询时，其中 [**D3DDDIARG \_ servicecontext.createquery**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_createquery)。**QueryType** 是 D3DDDIQUERYTYPE \_ 封闭，在响应时，必须始终将查询的 **UINT** 值设置为非零值。 请参阅 [*servicecontext.createquery*](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createquery) 和 **D3DDDIARG \_ servicecontext.createquery**。

 

## <a name="span-idminimum_capabilities_for_direct3d_level_9_3spanspan-idminimum_capabilities_for_direct3d_level_9_3spanspan-idminimum_capabilities_for_direct3d_level_9_3spanminimum-capabilities-for-direct3d-level-9_3"></a><span id="Minimum_capabilities_for_Direct3D_level_9_3"></span><span id="minimum_capabilities_for_direct3d_level_9_3"></span><span id="MINIMUM_CAPABILITIES_FOR_DIRECT3D_LEVEL_9_3"></span>Direct3D level 9 3 的最小功能 \_


除了为 Direct3D 级别 9 \_ 1 和 9 2 列出的功能外，还必须设置这些功能 \_ 。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><a href="/windows/win32/api/d3d9caps/ns-d3d9caps-d3dcaps9" data-raw-source="[&lt;strong&gt;D3DCAPS9&lt;/strong&gt;](/windows/win32/api/d3d9caps/ns-d3d9caps-_d3dcaps9)"><strong>D3DCAPS9</strong></a> 成员</th>
<th align="left">标志值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>PS20Caps</strong> - PS20Caps &gt;<strong>Cap</strong></td>
<td align="left"><p>D3DPS20CAPS_GRADIENTINSTRUCTIONS</p></td>
</tr>
<tr class="even">
<td align="left"><strong>PrimitiveMiscCaps</strong></td>
<td align="left"><p>D3DPMISCCAPS_INDEPENDENTWRITEMASKS</p>
<p>D3DPMISCCAPS_MRTPOSTPIXELSHADERBLENDING</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>TextureAddressCaps</strong></td>
<td align="left"><p>D3DPTADDRESSCAPS_BORDER</p></td>
</tr>
<tr class="even">
<td align="left"><strong>MaxTextureWidth</strong></td>
<td align="left"><p>4096</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>MaxTextureHeight</strong></td>
<td align="left"><p>4096</p></td>
</tr>
<tr class="even">
<td align="left"><strong>MaxTextureRepeat</strong></td>
<td align="left"><p>必须为零、8192或更大。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>NumSimultaneousRTs</strong></td>
<td align="left"><p>4</p></td>
</tr>
<tr class="even">
<td align="left"><strong>PS20Caps</strong> - PS20Caps &gt;<strong>NumInstructionSlots</strong></td>
<td align="left"><p>512 (像素着色器版本 2b) </p></td>
</tr>
<tr class="odd">
<td align="left"><strong>PS20Caps</strong> - PS20Caps &gt;<strong>NumTemps</strong></td>
<td align="left"><p>32 (像素着色器版本 2b) </p></td>
</tr>
<tr class="even">
<td align="left"><strong>VS20Caps</strong> - VS20Caps &gt;<strong>NumTemps</strong></td>
<td align="left"><p>32 (顶点着色器版本 2a) </p></td>
</tr>
<tr class="odd">
<td align="left"><strong>MaxVertexShaderConst</strong></td>
<td align="left"><p>256 (顶点着色器版本 2a) </p></td>
</tr>
<tr class="even">
<td align="left"><strong>VertexShaderVersion</strong></td>
<td align="left"><p>D3DVS_VERSION (3，0)  (参阅注意。 ) </p></td>
</tr>
</tbody>
</table>

 

**注意** D3DVS **VertexShaderVersion** \_ 版本 (3，0) 的 VertexShaderVersion 值保证实例化支持。 Direct3D 10Level 9 不公开着色器模型3.0。

 


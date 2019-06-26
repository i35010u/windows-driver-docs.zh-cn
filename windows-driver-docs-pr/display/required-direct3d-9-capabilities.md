---
title: 必需的 Direct3D 9 功能
ms.assetid: AE8ED273-2329-4E53-9FCD-5A8E863AED83
description: 为用户模式驱动程序以访问 Direct3D 9 功能所需的功能。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3eef9102eef5761f7f71fa2bccb8c5385002dccc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376613"
---
# <a name="required-direct3d-9-capabilities"></a>必需的 Direct3D 9 功能


应用程序完全访问 Microsoft Direct3D 版本 9 的功能\_1，9\_2 和 9\_3，用户模式驱动程序必须公开某些硬件功能。 这些功能都表示方面[ **D3DCAPS9** ](https://docs.microsoft.com/windows/desktop/api/d3d9caps/ns-d3d9caps-_d3dcaps9)返回的用户模式驱动程序的结构[ *GetCaps* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_getcaps)函数。 若要指示支持的功能，该驱动程序必须设置的这些成员**D3DCAPS9**到按位 OR，所有相应的标志值：

## <a name="span-idminimumcapabilitiesfordirect3dlevel91spanspan-idminimumcapabilitiesfordirect3dlevel91spanspan-idminimumcapabilitiesfordirect3dlevel91spanminimum-capabilities-for-direct3d-level-91"></a><span id="Minimum_capabilities_for_Direct3D_level_9_1"></span><span id="minimum_capabilities_for_direct3d_level_9_1"></span><span id="MINIMUM_CAPABILITIES_FOR_DIRECT3D_LEVEL_9_1"></span>最小为 Direct3D 功能级别 9\_1


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><a href="https://docs.microsoft.com/windows/desktop/api/d3d9caps/ns-d3d9caps-_d3dcaps9" data-raw-source="[&lt;strong&gt;D3DCAPS9&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/d3d9caps/ns-d3d9caps-_d3dcaps9)"><strong>D3DCAPS9</strong> </a>成员</th>
<th align="left">标记值</th>
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
<p>（参见备注。）</p></td>
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
<td align="left"><p>D3DPS_VERSION(2,0)</p></td>
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
<td align="left"><p>必须是零个或 128 或更高版本。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>MaxAnisotropy</strong></td>
<td align="left"><p>2</p></td>
</tr>
<tr class="even">
<td align="left"><strong>MaxVertexW</strong></td>
<td align="left"><p>0.f</p></td>
</tr>
</tbody>
</table>

 

**请注意**这些要求也适用：
-   该驱动程序还必须设置**TextureCaps**成员添加到值为 D3DPTEXTURECAPS\_NONPOW2CONDITIONAL 和 D3DPTEXTURECAPS\_POW2，或对两者都不。
-   当驱动程序对应的事件，其中[ **D3DDDIARG\_CREATEQUERY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_createquery)。**QueryType**是 D3DDDIQUERYTYPE\_事件，它必须始终设置事件的**BOOL**值设为**TRUE**响应时。 请参阅[ *CreateQuery* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createquery)并**D3DDDIARG\_CREATEQUERY**。

 

## <a name="span-idminimumcapabilitiesfordirect3dlevel92spanspan-idminimumcapabilitiesfordirect3dlevel92spanspan-idminimumcapabilitiesfordirect3dlevel92spanminimum-capabilities-for-direct3d-level-92"></a><span id="Minimum_capabilities_for_Direct3D_level_9_2"></span><span id="minimum_capabilities_for_direct3d_level_9_2"></span><span id="MINIMUM_CAPABILITIES_FOR_DIRECT3D_LEVEL_9_2"></span>最小为 Direct3D 功能级别 9\_2


这些功能必须另外设置为所列级别 Direct3D 9\_1。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><a href="https://docs.microsoft.com/windows/desktop/api/d3d9caps/ns-d3d9caps-_d3dcaps9" data-raw-source="[&lt;strong&gt;D3DCAPS9&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/d3d9caps/ns-d3d9caps-_d3dcaps9)"><strong>D3DCAPS9</strong> </a>成员</th>
<th align="left">标记值</th>
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
<td align="left"><p>必须为零或 2048，或更高版本。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>VertexShaderVersion</strong></td>
<td align="left"><p>D3DVS_VERSION(2,0)</p></td>
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
<td align="left"><p>10000000000.f</p></td>
</tr>
</tbody>
</table>

 

**请注意**此要求同样适用：
-   当驱动程序响应*z*-测试查询，其中[ **D3DDDIARG\_CREATEQUERY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_createquery)。**QueryType**是 D3DDDIQUERYTYPE\_封闭，它必须始终设置查询的**UINT**为非零值在响应时的值。 请参阅[ *CreateQuery* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createquery)并**D3DDDIARG\_CREATEQUERY**。

 

## <a name="span-idminimumcapabilitiesfordirect3dlevel93spanspan-idminimumcapabilitiesfordirect3dlevel93spanspan-idminimumcapabilitiesfordirect3dlevel93spanminimum-capabilities-for-direct3d-level-93"></a><span id="Minimum_capabilities_for_Direct3D_level_9_3"></span><span id="minimum_capabilities_for_direct3d_level_9_3"></span><span id="MINIMUM_CAPABILITIES_FOR_DIRECT3D_LEVEL_9_3"></span>最小为 Direct3D 功能级别 9\_3


这些功能必须另外设置为所列级别 Direct3D 9\_1 和 9\_2。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><a href="https://docs.microsoft.com/windows/desktop/api/d3d9caps/ns-d3d9caps-_d3dcaps9" data-raw-source="[&lt;strong&gt;D3DCAPS9&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/d3d9caps/ns-d3d9caps-_d3dcaps9)"><strong>D3DCAPS9</strong> </a>成员</th>
<th align="left">标记值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>PS20Caps</strong>-&gt;<strong>Caps</strong></td>
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
<td align="left"><p>必须为零或 8192，或更高版本。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>NumSimultaneousRTs</strong></td>
<td align="left"><p>4</p></td>
</tr>
<tr class="even">
<td align="left"><strong>PS20Caps</strong>-&gt;<strong>NumInstructionSlots</strong></td>
<td align="left"><p>512 (像素着色器版本 2b)</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>PS20Caps</strong>-&gt;<strong>NumTemps</strong></td>
<td align="left"><p>32 (像素着色器版本 2b)</p></td>
</tr>
<tr class="even">
<td align="left"><strong>VS20Caps</strong>-&gt;<strong>NumTemps</strong></td>
<td align="left"><p>32 (顶点着色器版本 2a)</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>MaxVertexShaderConst</strong></td>
<td align="left"><p>256 (顶点着色器版本 2a)</p></td>
</tr>
<tr class="even">
<td align="left"><strong>VertexShaderVersion</strong></td>
<td align="left"><p>D3DVS_VERSION(3,0) （参见备注。）</p></td>
</tr>
</tbody>
</table>

 

**请注意** **VertexShaderVersion** D3DVS 值\_VERSION(3,0) 保证实例化的支持。 Direct3D 10Level 9 不会公开着色器模型 3.0。

 

 

 






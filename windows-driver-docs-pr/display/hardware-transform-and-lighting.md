---
title: 硬件转换和照明
description: 硬件转换和照明
ms.assetid: b45aa56e-2d8c-412a-b581-a1e2002d4fac
keywords:
- Direct3D WDK Windows 2000 显示器、硬件 tansform 和照明
- 纹理转换 WDK Direct3D
- 转换 WDK Direct3D
- 照明 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f34351f12fc6e90c5fbbcc26b362777e5bacd118
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838900"
---
# <a name="hardware-transform-and-lighting"></a>硬件转换和照明


## <span id="ddk_hardware_transform_and_lighting_gg"></span><span id="DDK_HARDWARE_TRANSFORM_AND_LIGHTING_GG"></span>


几何操作的硬件加速（如照明和转换）已启用对最新直接 X 版本的[**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb) DDI 的修改。 在 API 级别，支持硬件中的顶点操作的设备与仅进行光栅化的设备单独枚举。

已扩展现有大写字母结构以指示可能存在于硬件加速转换设备上的功能。 例如，受支持光源的数量是用[**D3DLIGHTINGCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dcaps/ns-d3dcaps-_d3dlightingcaps)结构的**dwNumLights**成员设置的，该结构与[**D3DDEVICEDESC\_V1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3ddevicedesc_v1)结构一起报告。

下表列出了其他标志：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">旗帜</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>D3DDEVCAPS_CANBLTSYSTONONLOCAL</p></td>
<td align="left"><p>设备支持纹理 blt 从系统内存到非本地视频内存。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DDEVCAPS_DRAWPRIMITIVES2EX</p></td>
<td align="left"><p>驱动程序通过支持扩展的<em>D3dDrawPrimitives2</em>功能符合 DirectX 7.0。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DDEVCAPS_HWRASTERIZATION</p></td>
<td align="left"><p>设备具有用于光栅化的硬件加速。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DDEVCAPS_HWTRANSFORMANDLIGHT</p></td>
<td align="left"><p>设备可以支持硬件转换和硬件照明。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DDEVCAPS_SEPARATETEXTUREMEMORIES</p></td>
<td align="left"><p>设备是从单独的内存池中纹理。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DTRANSFORMCAPS_CLIP</p></td>
<td align="left"><p>在转换时，硬件可能会被剪裁。</p></td>
</tr>
</tbody>
</table>

 

由于硬件几何加速器的特征集可能不同（如支持的光源数量），因此大写字母结构指示此设备执行的几何操作的子集。 零是受支持的光源数量的有效值，指示硬件只进行转换。

只有包含顶点法线的顶点才能正确地亮起;对于不包含法线的顶点，所有照明计算都采用0的点积。

几何管道软件实现所使用的所有密钥状态和数据结构都在 DDI 级别可用。 某些显示卡仅在硬件中实现照明，并在主机处理器上执行转换和剪辑。

以下呈现状态类型仅适用于加速转换和照明的设备：

```cpp
D3DRENDERSTATE_AMBIENT
D3DRENDERSTATE_AMBIENTMATERIALSOURCE
D3DRENDERSTATE_CLIPPING
D3DRENDERSTATE_CLIPPLANEENABLE
D3DRENDERSTATE_COLORVERTEX
D3DRENDERSTATE_DIFFUSEMATERIALSOURCE
D3DRENDERSTATE_EMISSIVEMATERIALSOURCE
D3DRENDERSTATE_EXTENTS
D3DRENDERSTATE_FOGVERTEXMODE
D3DRENDERSTATE_LIGHTING
D3DRENDERSTATE_LOCALVIEWER
D3DRENDERSTATE_NORMALIZENORMALS
D3DRENDERSTATE_SPECULARMATERIALSOURCE
D3DRENDERSTATE_VERTEXBLEND
```

 

 






---
title: 硬件转换和照明
description: 硬件转换和照明
ms.assetid: b45aa56e-2d8c-412a-b581-a1e2002d4fac
keywords:
- Direct3D WDK Windows 2000 显示、 硬件 tansform 和照明
- 纹理转换 WDK Direct3D
- 转换 WDK Direct3D
- 照明 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 916c16e09399ab24b96666131ac5fc9cb32e9cbb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566770"
---
# <a name="hardware-transform-and-lighting"></a>硬件转换和照明


## <span id="ddk_hardware_transform_and_lighting_gg"></span><span id="DDK_HARDWARE_TRANSFORM_AND_LIGHTING_GG"></span>


已启用硬件加速的几何操作，例如光源和转换进行修改[ **D3dDrawPrimitives2** ](https://msdn.microsoft.com/library/windows/hardware/ff544704) DDI 的最新的直接 X 版本。 在 API 级别，设备在硬件支持顶点操作的枚举单独从那些确实仅光栅化。

已扩展现有的 cap 结构以指示可能存在硬件加速转换设备上的功能。 例如，使用设置的受支持的光源数**dwNumLights**的成员[ **D3DLIGHTINGCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff548471)结构报告与的[ **D3DDEVICEDESC\_V1** ](https://msdn.microsoft.com/library/windows/hardware/ff544689)结构。

下表列出了其他标志：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Flag</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>D3DDEVCAPS_CANBLTSYSTONONLOCAL</p></td>
<td align="left"><p>设备支持纹理 blt 从系统内存向非本地的视频内存。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DDEVCAPS_DRAWPRIMITIVES2EX</p></td>
<td align="left"><p>该驱动程序支持扩展是 7.0 兼容的 DirectX <em>D3dDrawPrimitives2</em>功能。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DDEVCAPS_HWRASTERIZATION</p></td>
<td align="left"><p>该设备已光栅化的硬件加速。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DDEVCAPS_HWTRANSFORMANDLIGHT</p></td>
<td align="left"><p>设备可以在硬件支持硬件转换和照明。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DDEVCAPS_SEPARATETEXTUREMEMORIES</p></td>
<td align="left"><p>设备纹理从单独内存池。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DTRANSFORMCAPS_CLIP</p></td>
<td align="left"><p>硬件可以剪切转换时。</p></td>
</tr>
</tbody>
</table>

 

由于的功能集的硬件 geometry 加速器可能不同 （例如光源支持数），cap 结构指示此设备执行的几何操作的子集。 零是有效值光源支持，指示的硬件无法仅转换数。

正确亮起包括正常的顶点的顶点;不包含普通的顶点，所有照明计算中所用的 0 点积。

所有关键状态和数据结构几何管道软件实现使用 DDI 级别都可用。 某些显示卡仅在硬件中实现照明，进行转换和剪辑主机处理器上。

以下呈现类型等仅适用于加速转换和照明的设备的状态：

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

 

 






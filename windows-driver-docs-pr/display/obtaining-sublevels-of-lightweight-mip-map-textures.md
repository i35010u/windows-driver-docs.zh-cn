---
title: 获取轻量 MIP 贴图纹理的子级别
description: 获取轻量 MIP 贴图纹理的子级别
keywords:
- MIP map 纹理 WDK DirectX 9.0，获取子级别
- 轻型 MIP map 纹理 WDK DirectX 9.0，获取子级别
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc1b852aaf9cb0032689f8f7582d47449bc26eca
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828087"
---
# <a name="obtaining-sublevels-of-lightweight-mip-map-textures"></a>获取轻量 MIP 贴图纹理的子级别


## <span id="ddk_obtaining_sublevels_of_lightweight_mip_map_textures_gg"></span><span id="DDK_OBTAINING_SUBLEVELS_OF_LIGHTWEIGHT_MIP_MAP_TEXTURES_GG"></span>


DirectX 9.0 版本驱动程序可以使用 [CPixel 类方法](./cpixel-support-methods-for-lightweight-mip-maps.md) 来获取有关轻型系统内存 MIP map 纹理的子级别的信息--仅存储有关轻型 MIP 地图纹理的顶层的信息。 如果驱动程序必须将轻型系统内存 MIP map 纹理复制到视频内存，则驱动程序可以使用 CPixel 类方法来计算源纹理的大小以及源纹理子级别的偏移量。

驱动程序编写器不需要使用 CPixel 类方法来计算轻型 MIP 地图纹理的子级别位置。 但是，DirectX 9.0 运行时使用 **CPixel** 类方法恢复轻型系统内存 MIP map 纹理的内存布局。 因此，为了确保运行时和驱动程序以相同的方式恢复轻型系统内存 MIP map 纹理的内存布局，驱动程序编写器必须遵循相同的 **CPixel** 类规则才能实现自己的代码。

有关如何实现 **CPixel** 类的信息，请参阅 [pixlib](/samples/browse/)代码示例中的 *hpp*、*象素* 和 *pixlib* 文件。

CPixel 类包含以下方法：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">CPixel 方法</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/display/cpixel-computesurfacesize" data-raw-source="[&lt;strong&gt;ComputeSurfaceSize&lt;/strong&gt;](./cpixel-computesurfacesize.md)"><strong>ComputeSurfaceSize</strong></a></p></td>
<td align="left"><p>确定分配图面所需的内存量。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/display/cpixel-computevolumesize" data-raw-source="[&lt;strong&gt;ComputeVolumeSize&lt;/strong&gt;](./cpixel-computevolumesize.md)"><strong>ComputeVolumeSize</strong></a></p></td>
<td align="left"><p>确定分配卷所需的内存量。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/display/cpixel-computemipmapsize" data-raw-source="[&lt;strong&gt;ComputeMipMapSize&lt;/strong&gt;](./cpixel-computemipmapsize.md)"><strong>ComputeMipMapSize</strong></a></p></td>
<td align="left"><p>确定分配 MIP map 纹理所需的内存量。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/display/cpixel-computemipvolumesize" data-raw-source="[&lt;strong&gt;ComputeMipVolumeSize&lt;/strong&gt;](./cpixel-computemipvolumesize.md)"><strong>ComputeMipVolumeSize</strong></a></p></td>
<td align="left"><p>确定分配 MIP map 纹理卷所需的内存量。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/display/cpixel-computemipmapoffset" data-raw-source="[&lt;strong&gt;ComputeMipMapOffset&lt;/strong&gt;](./cpixel-computemipmapoffset.md)"><strong>ComputeMipMapOffset</strong></a></p></td>
<td align="left"><p>确定 MIP 地图纹理的子偏移量。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/display/cpixel-computemipvolumeoffset" data-raw-source="[&lt;strong&gt;ComputeMipVolumeOffset&lt;/strong&gt;](./cpixel-computemipvolumeoffset.md)"><strong>ComputeMipVolumeOffset</strong></a></p></td>
<td align="left"><p>确定 MIP 地图量纹理的 subvolume 偏移量。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/display/cpixel-computesurfaceoffset" data-raw-source="[&lt;strong&gt;ComputeSurfaceOffset&lt;/strong&gt;](./cpixel-computesurfaceoffset.md)"><strong>ComputeSurfaceOffset</strong></a></p></td>
<td align="left"><p>确定图面的 subrectangular 偏移量。</p></td>
</tr>
</tbody>
</table>


---
title: 获取轻量 MIP 贴图纹理的子级别
description: 获取轻量 MIP 贴图纹理的子级别
ms.assetid: a2781c9a-b4bb-42a9-8ed5-9f62c1d2ee64
keywords:
- MIP 映射纹理 WDK DirectX 9.0，获取子级别
- 轻型 MIP 贴图纹理 WDK DirectX 9.0，获取子级别
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd1ce4b0a5a3e89accb32b2a62695fdd61a9e068
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372781"
---
# <a name="obtaining-sublevels-of-lightweight-mip-map-textures"></a>获取轻量 MIP 贴图纹理的子级别


## <span id="ddk_obtaining_sublevels_of_lightweight_mip_map_textures_gg"></span><span id="DDK_OBTAINING_SUBLEVELS_OF_LIGHTWEIGHT_MIP_MAP_TEXTURES_GG"></span>


DirectX 9.0 版本驱动程序可以使用[CPixel 类方法](https://docs.microsoft.com/windows-hardware/drivers/display/cpixel-support-methods-for-lightweight-mip-maps)以获取有关子级别的轻型的系统内存 MIP 贴图纹理-信息仅有关的信息的轻量 MIP 贴图纹理的最高级别存储。 如果该驱动程序必须将轻型的系统内存 MIP 贴图纹理复制到视频内存，该驱动程序可以使用 CPixel 类方法来计算源纹理的大小和源纹理的子级别的偏移量。

驱动程序编写人员不需要使用 CPixel 类方法来计算轻型 MIP 贴图纹理的子级别的位置。 但是，DirectX 9.0 运行时使用**CPixel**类方法来恢复轻型的系统内存 MIP 贴图纹理的内存布局。 因此，若要确保，运行时和驱动程序的轻型的系统内存 MIP 贴图纹理内存布局恢复相同的方式，驱动程序编写人员必须遵循相同**CPixel**类规则，以实现其自己的代码。

有关如何信息**CPixel**类实现，请参阅*pixel.hpp*， *pixel.cpp*，以及*pixlib.cpp* 中的文件[PixLib](https://go.microsoft.com/fwlink/p/?linkid=256156)代码示例。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/cpixel-computesurfacesize" data-raw-source="[&lt;strong&gt;ComputeSurfaceSize&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/cpixel-computesurfacesize)"><strong>ComputeSurfaceSize</strong></a></p></td>
<td align="left"><p>确定要分配一个面所需的内存量。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/cpixel-computevolumesize" data-raw-source="[&lt;strong&gt;ComputeVolumeSize&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/cpixel-computevolumesize)"><strong>ComputeVolumeSize</strong></a></p></td>
<td align="left"><p>确定要将卷分配所需的内存量。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/cpixel-computemipmapsize" data-raw-source="[&lt;strong&gt;ComputeMipMapSize&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/cpixel-computemipmapsize)"><strong>ComputeMipMapSize</strong></a></p></td>
<td align="left"><p>确定所需分配 MIP 贴图纹理的内存量。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/cpixel-computemipvolumesize" data-raw-source="[&lt;strong&gt;ComputeMipVolumeSize&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/cpixel-computemipvolumesize)"><strong>ComputeMipVolumeSize</strong></a></p></td>
<td align="left"><p>确定将 MIP 贴图纹理卷分配所需的内存量。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/cpixel-computemipmapoffset" data-raw-source="[&lt;strong&gt;ComputeMipMapOffset&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/cpixel-computemipmapoffset)"><strong>ComputeMipMapOffset</strong></a></p></td>
<td align="left"><p>确定 MIP 贴图纹理子级偏移量。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/cpixel-computemipvolumeoffset" data-raw-source="[&lt;strong&gt;ComputeMipVolumeOffset&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/cpixel-computemipvolumeoffset)"><strong>ComputeMipVolumeOffset</strong></a></p></td>
<td align="left"><p>确定 MIP 贴图卷纹理的子宗卷偏移量。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/cpixel-computesurfaceoffset" data-raw-source="[&lt;strong&gt;ComputeSurfaceOffset&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/cpixel-computesurfaceoffset)"><strong>ComputeSurfaceOffset</strong></a></p></td>
<td align="left"><p>确定一个面 subrectangular 偏移的量。</p></td>
</tr>
</tbody>
</table>

 

 

 






---
title: 轻量 MIP 贴图的 CPixel 支持方法
description: 轻量 MIP 贴图的 CPixel 支持方法
ms.assetid: 79204a0c-c3a8-4059-a1be-9febf20a8cbd
keywords:
- 描述 CPixel 接口
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 486b44e50e122a7b3e6ac16b471d366d5516c0eb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566726"
---
# <a name="cpixel-support-methods-for-lightweight-mip-maps"></a>轻量 MIP 贴图的 CPixel 支持方法


## <span id="ddk_cpixel_support_methods_for_lightweight_mip_maps_gg"></span><span id="DDK_CPIXEL_SUPPORT_METHODS_FOR_LIGHTWEIGHT_MIP_MAPS_GG"></span>


本部分介绍为定义的方法**CPixel**类。 这些方法用于恢复的轻型的系统内存 MIP 贴图纹理的布局。 在中定义的方法原型*pixel.hpp*文件。 此文件，其沿着*pixel.cpp*并*pixlib.cpp*最初包括在 Microsoft Windows 驱动程序开发工具包 (DDK) 一起，用于生成*PixLib.lib*支持库。 (在 DDK 前面带有 Windows Driver Kit \[WDK\]。)

有关详细信息*PixLib.lib*库，请参阅[PixLib](https://go.microsoft.com/fwlink/p/?linkid=256156)硬件开发人员中心中的示例。

有关驱动程序以使用以下**CPixel**类的方法，必须包括*pixel.hpp*您的代码文件，并链接到*PixLib.lib*生成您的驱动程序时。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">CPixel 类方法</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="cpixel-computesurfacesize.md" data-raw-source="[&lt;strong&gt;ComputeSurfaceSize&lt;/strong&gt;](cpixel-computesurfacesize.md)"><strong>ComputeSurfaceSize</strong></a></p></td>
<td align="left"><p>确定要分配一个面所需的内存量。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="cpixel-computevolumesize.md" data-raw-source="[&lt;strong&gt;ComputeVolumeSize&lt;/strong&gt;](cpixel-computevolumesize.md)"><strong>ComputeVolumeSize</strong></a></p></td>
<td align="left"><p>确定要将卷分配所需的内存量。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="cpixel-computemipmapsize.md" data-raw-source="[&lt;strong&gt;ComputeMipMapSize&lt;/strong&gt;](cpixel-computemipmapsize.md)"><strong>ComputeMipMapSize</strong></a></p></td>
<td align="left"><p>确定所需分配 MIP 贴图纹理的内存量。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="cpixel-computemipvolumesize.md" data-raw-source="[&lt;strong&gt;ComputeMipVolumeSize&lt;/strong&gt;](cpixel-computemipvolumesize.md)"><strong>ComputeMipVolumeSize</strong></a></p></td>
<td align="left"><p>确定将 MIP 贴图纹理卷分配所需的内存量。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="cpixel-computemipmapoffset.md" data-raw-source="[&lt;strong&gt;ComputeMipMapOffset&lt;/strong&gt;](cpixel-computemipmapoffset.md)"><strong>ComputeMipMapOffset</strong></a></p></td>
<td align="left"><p>确定 MIP 贴图纹理子级偏移量。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="cpixel-computemipvolumeoffset.md" data-raw-source="[&lt;strong&gt;ComputeMipVolumeOffset&lt;/strong&gt;](cpixel-computemipvolumeoffset.md)"><strong>ComputeMipVolumeOffset</strong></a></p></td>
<td align="left"><p>确定 MIP 贴图卷纹理的子宗卷偏移量。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="cpixel-computesurfaceoffset.md" data-raw-source="[&lt;strong&gt;ComputeSurfaceOffset&lt;/strong&gt;](cpixel-computesurfaceoffset.md)"><strong>ComputeSurfaceOffset</strong></a></p></td>
<td align="left"><p>确定一个面 subrectangular 偏移的量。</p></td>
</tr>
</tbody>
</table>

 

 

 






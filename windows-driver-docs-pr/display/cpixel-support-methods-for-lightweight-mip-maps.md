---
title: 轻量 MIP 贴图的 CPixel 支持方法
description: 轻量 MIP 贴图的 CPixel 支持方法
ms.assetid: 79204a0c-c3a8-4059-a1be-9febf20a8cbd
keywords:
- CPixel 接口，描述
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8832c0fc9935416ee37ab2b8614457086a0e84f6
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91733089"
---
# <a name="cpixel-support-methods-for-lightweight-mip-maps"></a>轻量 MIP 贴图的 CPixel 支持方法


## <span id="ddk_cpixel_support_methods_for_lightweight_mip_maps_gg"></span><span id="DDK_CPIXEL_SUPPORT_METHODS_FOR_LIGHTWEIGHT_MIP_MAPS_GG"></span>


本部分介绍为 **CPixel** 类定义的方法。 这些方法用于恢复轻型系统内存 MIP 地图纹理的布局。 方法原型在 *hpp* 文件中定义。 此文件连同 *象素* 和 *pixlib* 最初都包含在 Microsoft Windows 驱动程序开发工具包 (的 DDK) 中，并用于构建 *pixlib* 支持库。  (在 Windows 驱动程序工具包 WDK 之前的 DDK \[ \] 。 ) 

有关 *PixLib* 库的详细信息，请参阅硬件开发人员中心中的 [PixLib](/samples/browse/) 示例。

要使你的驱动程序使用以下**CPixel**类方法，你必须在代码中包含*hpp*文件，并在生成驱动程序时链接到*PixLib。*

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">CPixel 类方法</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="cpixel-computesurfacesize.md" data-raw-source="[&lt;strong&gt;ComputeSurfaceSize&lt;/strong&gt;](cpixel-computesurfacesize.md)"><strong>ComputeSurfaceSize</strong></a></p></td>
<td align="left"><p>确定分配图面所需的内存量。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="cpixel-computevolumesize.md" data-raw-source="[&lt;strong&gt;ComputeVolumeSize&lt;/strong&gt;](cpixel-computevolumesize.md)"><strong>ComputeVolumeSize</strong></a></p></td>
<td align="left"><p>确定分配卷所需的内存量。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="cpixel-computemipmapsize.md" data-raw-source="[&lt;strong&gt;ComputeMipMapSize&lt;/strong&gt;](cpixel-computemipmapsize.md)"><strong>ComputeMipMapSize</strong></a></p></td>
<td align="left"><p>确定分配 MIP map 纹理所需的内存量。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="cpixel-computemipvolumesize.md" data-raw-source="[&lt;strong&gt;ComputeMipVolumeSize&lt;/strong&gt;](cpixel-computemipvolumesize.md)"><strong>ComputeMipVolumeSize</strong></a></p></td>
<td align="left"><p>确定分配 MIP map 纹理卷所需的内存量。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="cpixel-computemipmapoffset.md" data-raw-source="[&lt;strong&gt;ComputeMipMapOffset&lt;/strong&gt;](cpixel-computemipmapoffset.md)"><strong>ComputeMipMapOffset</strong></a></p></td>
<td align="left"><p>确定 MIP 地图纹理的子偏移量。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="cpixel-computemipvolumeoffset.md" data-raw-source="[&lt;strong&gt;ComputeMipVolumeOffset&lt;/strong&gt;](cpixel-computemipvolumeoffset.md)"><strong>ComputeMipVolumeOffset</strong></a></p></td>
<td align="left"><p>确定 MIP 地图量纹理的 subvolume 偏移量。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="cpixel-computesurfaceoffset.md" data-raw-source="[&lt;strong&gt;ComputeSurfaceOffset&lt;/strong&gt;](cpixel-computesurfaceoffset.md)"><strong>ComputeSurfaceOffset</strong></a></p></td>
<td align="left"><p>确定图面的 subrectangular 偏移量。</p></td>
</tr>
</tbody>
</table>

 

 


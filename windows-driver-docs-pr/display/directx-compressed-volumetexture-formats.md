---
title: DirectX 压缩 VolumeTexture 格式
description: DirectX 压缩 VolumeTexture 格式
ms.assetid: 5a655a30-e489-4691-873a-58bece059877
keywords:
- 绘制压缩的纹理 WDK DirectDraw，压缩卷的纹理格式
- DirectDraw 压缩的纹理 WDK Windows 2000 显示，请压缩卷的纹理格式
- 压缩的纹理图面 WDK DirectDraw，压缩的卷的纹理格式
- WDK DirectDraw，压缩的纹理的图面
- 纹理 WDK DirectDraw 压缩
- DXVN WDK DirectDraw
- DXTN WDK DirectDraw
- 切片 WDK DirectDraw
- 卷纹理 WDK DirectDraw
- 容量耗尽呈现 WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b2f614b4fcf6e1d9b2c5af158553897881feae94
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563477"
---
# <a name="directx-compressed-volumetexture-formats"></a>DirectX 压缩 VolumeTexture 格式


## <span id="ddk_directx_compressed_volumetexture_formats_gg"></span><span id="DDK_DIRECTX_COMPRESSED_VOLUMETEXTURE_FORMATS_GG"></span>


卷的纹理映射为数字化的空间，则返回 true 的 3D 区域通过定期生成的映像。 例如，球的火灾进行抽样并"金额"的前面带有火焰中切片可以得到解决。 在这种情况下，前面带有火焰量表示一组在图像中的每个像素的 alpha、 红色、 绿色和蓝色成分的值。 由一系列的这些段表示整个前面带有火焰。

然后再转到 DirectX 卷呈现的详细信息，务必一些术语解释清楚。 有两种常见的方法在计算机图形中用于表示卷数据集。 一个是示例在每个位置的映像和存储相应的 ARGB 值。 例如，前面带有火焰的数据可以存储为 256 X 256 X 256 三维数组。 这需要大约 64 MB 在数组中存储每个位置处的 32 位值。 （某些应用程序，如医疗图像处理，可能需要如此大量的数据。）但是，"切片"到 4 个或 8 slabs 前面带有火焰可以很好的近似值。 每个碎片存储 256 X 256 元素，其中每个元素都表示碎片中的数据的区域。

如果我们假设是合理的大小 256 X 256 X 4 的数组，然后存储在每个位置的 32 位值需要仅有 1 MB 的存储 （小于如果压缩数据）。 讨论这两种不同方法的原因是，如果你想在位于前面带有火焰处于隐藏状态，则每个位置处存储的数据值为不同的映像中的任何内容。 在完整 256 X 256 X 256 数据集的任何一个元素可能会导致大约 1/256 的最后一个 alpha 和颜色。 在切片的方法中，元素可以从 0 到最后一个 alpha 和用于该像素颜色任意位置提供。 问题是采样的，有时"voxel"一词用来描述这两种类型。 从 DirectX 8 开始，切片方法 （通常称为"卷纹理"） 是受支持的唯一方法。 其理念是合理的大小来缩短卷集数据。 使用纹理绘制硬件到一些小改动，DirectX 图形 API 可以公开高性能容量耗尽呈现。

到目前为止，本部分的大部分都侧重于 DXT*N*压缩图面上的格式。 这些格式适用于 2D 纹理。 它们是效率较低，但是，当您在使用卷数据集，由于卷数据集存储在单独的图面，需要额外的硬件周期，才能访问。 若要解决此问题，DirectX 8 支持一的组图面上卷的格式。

其理念是获取卷切片并对其进行压缩使用 DXT*N*。 然后，而不是按顺序将已完成的图面存储在内存中，DXT*N*数据块进行重新排序。 重新排序是完成的以便小 4 X 4 纹素阻止窗体数据多维数据集。 它们可以是 4 X 4 X 1、 4 X 4 X 2、 4 X 4 X 3 或 4 X 4 X 4。 请注意，4 X 4 X 1 排序是完全通过 DXT5 DXT1 中使用的相同。 重要的一点是：

卷面是使用 DXT 压缩的数据切片*N* ，然后重新排序为三维位置的数据的帐户。 Fourcc 的 DXV1，...，DXV5 引用这些重新排序后的数据结构 (或只是 DXV*N*来描述一般情况下)。 请注意，DXV1 数据结构将保留一组重新排序 DXT1 图面，DXV2 将开展一系列 DXT2 图面中，依次类推。

### <a name="span-iddxvndetailsspanspan-iddxvndetailsspandxvn-details"></a><span id="dxvn_details"></span><span id="DXVN_DETAILS"></span>DXV*N*详细信息

DXV*N*图面中的 1 级深度排列方式存储包含一个组的 4 × 4 DXT*N* subblocks (实际上它是只需 DXT*N*面)。 DXV*N* 4 x 4 x 2 块格式结构包含两个 4 x 4 DXT*N* subblocks 中每两个相邻的数据切片。 使用此方法，DXV*N* 4 x 4 x 4 块格式结构包含四个 4 x 4 DXT*N* subblocks 从 4 个数据切片。 在所有情况下*N*中 DXV*N*用于匹配到相应 DXT*N*用于压缩类型。 DXT*N*块可以存储为 64 位 （颜色和 1 位 alpha 或使用的 alpha 更多信息的 128 位）。 因此 DXV*N* subblocks 具有的类型可能的相同大小*N*。也就是说，DXT1 和 DXV1 使用 64 位 subblocks，同时 DXT2，...，DXT5 和 DXV2，...，DXV5 使用 128 位 subblocks。

给定的纹素坐标 *（u、 v、 p）* 其中*u* {0，1，...，*宽度*-1}， *v* {0，1，...，*高度*-1}，并*p* {0、 1、...、*深度*-1}，以下可用于计算的压缩的块和包含该纹素的内存中的 subblock 相应的地址。 如上所述，subblock 格式都符合现有 DXT*N*格式：

```cpp
subblock_size = 8 (for DXT1)
subblock_size = 16 (for DXT2,...,DXT5)
block_size = MIN(p, 4) * subblock_size
horiz_stride = (width + 3) >> 2
planar_stride = ( (height + 3) >> 2) * horiz_stride
block_byte_address = block_size *
    ( (p >> 2) * planar_stride + (v >> 2) * horiz_stride + (u >> 2) )
subblock_byte_address = block_byte_address + ((p & 3) * subblock_size)
```

 

 






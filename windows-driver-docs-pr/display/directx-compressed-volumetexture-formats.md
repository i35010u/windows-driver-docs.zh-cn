---
title: DirectX 压缩 VolumeTexture 格式
description: DirectX 压缩 VolumeTexture 格式
keywords:
- 绘制压缩纹理 WDK DirectDraw，压缩量纹理格式
- DirectDraw 压缩纹理 WDK Windows 2000 显示，压缩的卷纹理格式
- 压缩的纹理面 WDK DirectDraw，压缩的卷纹理格式
- 表面 WDK DirectDraw，压缩纹理
- 纹理 WDK DirectDraw，压缩
- DXVN WDK DirectDraw
- DXTN WDK DirectDraw
- 切片 WDK DirectDraw
- 卷纹理 WDK DirectDraw
- 容量耗尽呈现 WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b4a029f8f762bcb63e53a95439212f48b6e73ba
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809343"
---
# <a name="directx-compressed-volumetexture-formats"></a>DirectX 压缩 VolumeTexture 格式


## <span id="ddk_directx_compressed_volumetexture_formats_gg"></span><span id="DDK_DIRECTX_COMPRESSED_VOLUMETEXTURE_FORMATS_GG"></span>


卷纹理地图是通过真正的3D 区域定期生成的数字化图像。 例如，可以对防火球进行采样，并且可以考虑切片中的火焰的 "数量"。 从这种意义上来说，火焰量表示图像中每个像素的 alpha、红色、绿色和蓝色分量的一组值。 整个火焰由一系列这些切片表示。

在深入了解 DirectX 卷呈现的详细信息之前，请务必阐明一些术语。 计算机图形中使用了两种常用方法来表示卷数据集。 一种是在每个位置对图像采样，并存储适当的 ARGB 值。 例如，火焰的数据可以存储为 256 X 256 X 256 3 维数组。 这需要大约64MB 才能在数组中的每个位置存储32位值。  (某些应用程序（例如医疗图像）可能需要使用这种数据量。 ) 不过，"切分" 火焰进入4或8碎片可以产生非常好的近似值。 每个楼板都存储 256 X 256 元素，其中每个元素都代表一个数据区域。

如果我们假设大小为 256 X 256 X 4 的数组是合理的，则在每个位置存储一个32位值只需 (较少的存储空间来) 压缩数据。 讨论这两种不同方法的原因是，如果要隐藏火焰后面的图像中的任何内容，则每个位置存储的数据值都是不同的。 在完整的 256 X 256 X 256 数据集中，任何一个元素可能会涉及最终 alpha 和颜色的1/256。 在切片方法中，元素可以从0到用于该像素的最终 alpha 和颜色的任何位置提供。 问题在于有时，术语 "voxel" 用于描述这两种类型的采样。 从 DirectX 8 开始，切片方法 (通常称为 "批量纹理" ) 是唯一受支持的方法。 其思路是将卷数据集减小到合理的大小。 对于纹理硬件的一些细微修改，DirectX 图形 API 可以公开高性能容量耗尽呈现。

到目前为止，本部分的大部分内容重点介绍了 DXT *N* 压缩的 surface 格式。 这些格式适用于2D 纹理。 不过，当你使用卷数据集时，这些数据集效率较低，因为卷数据集存储在需要额外的硬件循环才能访问的不同表面中。 为了解决此问题，DirectX 8 支持一组卷面的格式。

其思路是使用 DXT *N* 获取卷切片并对其进行压缩。 然后，不将已完成的图面按顺序存储在内存中，而是将 DXT *N* 数据块重新排序。 重新排序完成后，small 4X4 纹素块窗体数据多维数据集。 它们可以是4X4X1、4X4X2、4X4X3 或4X4X4。 请注意，4X4X1 顺序与 DXT1 中通过 DXT5 使用的顺序完全相同。 重要的一点是：

卷面是使用 DXT *N* 压缩的数据切片，然后重新排序以考虑3d 位置数据。 这些重新排序的数据结构由 Fourcc 的 DXV1,..., DXV5 (或只是 DXV *N* 来描述) 的常规事例。 请注意，DXV1 数据结构会保留一组重新排序的 DXT1 图面，DXV2 将保留一组 DXT2 图面等。

### <a name="span-iddxvn_detailsspanspan-iddxvn_detailsspandxvn-details"></a><span id="dxvn_details"></span><span id="DXVN_DETAILS"></span>DXV *N* 详细信息

以1为深度的布局存储的 DXV *N* 表面包含一组 4X4 DXT *N* subblocks (事实上，它只是一个 DXT *N* surface) 。 DXV *N* 4x4x2 块格式结构包含两个 4X4 DXT *N* subblocks，其中一条来自两个相邻的数据切片。 使用此方法时，DXV *N* 4x4x4 块格式结构包含从4个数据切片获取的四个 4X4 DXT *N* subblocks。 在所有情况下，DXV *n* 中的 *n* 用于将其与用于压缩的相应 DXT *N* 类型进行匹配。 DXT *N* 块可以存储为64位 (颜色和1位 alpha，或) 的附加 alpha 信息的128位。 因此，DXV *N* subblocks 的大小可能会基于类型 *N*。也就是说，DXT1 和 DXV1 使用64位 subblocks，而 DXT2,.., DXT5 和 DXV2,.., DXV5 使用128位 subblocks。

给定一个纹素坐标 *(u，v，p)* ， *其中 u* {0，1,...,*width*-1}， *v* {0，1，...， *height*-1}， *p* {0，1，...， *depth*-1}，以下可用于计算压缩块的相应地址和包含该纹素的 subblock 内存。 如前所述，subblock 格式匹配现有的 DXT *N* 格式：

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

 

 






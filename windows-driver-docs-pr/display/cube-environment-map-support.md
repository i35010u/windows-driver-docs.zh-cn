---
title: 立体环境贴图支持
description: 立体环境贴图支持
ms.assetid: 41666b17-39b0-4022-925f-538455e41f3a
keywords:
- 映射多维数据集环境
- 环境映射 WDK Direct3D
- 多维数据集环境映射 WDK Direct3D
- 照明 WDK Direct3D
- WDK Direct3D 的反射效果
- 360 度环境 WDK Direct3D
- 映射 WDK Direct3D 的实时环境
- 循环映射 WDK Direct3D
- 球面映射 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 48bd48c18dd1c1933dd58ddb5fe8ae79c32f4526
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370172"
---
# <a name="cube-environment-map-support"></a>立体环境贴图支持


## <span id="ddk_cube_environment_map_support_gg"></span><span id="DDK_CUBE_ENVIRONMENT_MAP_SUPPORT_GG"></span>


在 Direct3D 中的多纹理支持允许使用环境映射的光照量和光照反射。 但是，圆形等单映射 360 度解决方案或球面映射不强大，足以在真实时间中广泛使用。 有关实时生成和寻址的 360 度环境最适合的解决方案是布置隔断映射中，六个纹理 （人脸） 组成。 指向具有 90 度的视野适当的方向照相机可以生成每张人脸。 每个顶点向量 （正常、 反射或折射） 都是提供到光栅化硬件，然后遍历多边形，并计算使用立方体贴图的人脸的内插的向量的交集。 如果应用程序或 API 生成了多维数据集环境映射，该驱动程序不要求有关的转换矩阵的信息或的坐标的空间中定义的每个顶点向量。 这是因为向量仅用于解决环境映射，在逻辑上是相同的坐标空间中。

循环映射的寻址涉及向量标准化;寻址的球面映射需要使用三角函数。 单映射环境的所有类型都是非线性： 循环映射是极其失真和 anisotropic 接近其外围球面映射具有接近其两极大时会发生失真。 这样，就需要重新创建环境映射，每次视点的更改导致的中央视图区域会显得失真。

布置隔断环境映射，通过指向具有 90 度的视野六个不同的方向，在真实或模拟照相机是免费的这些缺点。 它们可以更快地生成，但需要不太频繁更新，具有较少时会发生失真，并且可以通过使用类似于已使用的角度来看更正纹理映射等式进行寻址。

一般情况下，多维数据集映射是为复杂的光照量和光照反射提供实时环境映射的最佳选择。

多维数据集映射允许传递给驱动程序使用[ **D3dDrawPrimitives2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)呈现状态机制。 [FVF](fvf--flexible-vertex-format-.md)纹理坐标，FVF 代码 01 传递该纹理坐标集。

在世界坐标; 中定义多维数据集映射也就是说，其世界转换矩阵为单位矩阵。 多维数据集映射可以似乎是在不同的空间中，如果对相应的纹理坐标索引使用纹理转换。 这些纹理坐标索引将查找人脸四个，在直接 + z 人脸。 默认情况下，Y 是向上。 来源 （u、 v） 纹素网格在每张人脸，左上角是以允许按指针摄像机从多维数据集的中心而无需任何其他转换所面临的创建。

**DirectDrawCreateEx**一个标志，指示多维数据集映射是要创建的采用。 尽管驱动程序可能会根据需要填充，不需要在 API 级别，分配一些人脸。 图面上的描述符具有六个位，该值指示应用程序能够使用人脸包含一组标志。 人脸时都与已实现**IDirectDrawSurface7::GetAttachedSurface**方法， **NULL**跳过的人脸。 每张人脸的维度都可通过其图面上的描述符，人脸 bitcode 字段指示它是哪些人脸。 有关详细信息**DirectDrawCreateEx**并**IDirectDrawSurface7::GetAttachedSurface**，请参阅 DirectDraw SDK 文档。

从返回的指针**DirectDrawCreate**是实际指向第一个非**NULL**多维数据集中的人脸。 可以通过采用面上的 bitcode 获取的人脸标识符。 这是传递给指针**IDirect3DDevice7::SetTexture** （Direct3D SDK 文档中所述） 的方法使此映射可在多个纹理管道。

如果任何应用层协议旨在向呈现，必须使用 D3DPTEXTURECAPS 创建立方体贴图\_立方体贴图 cap 标志设置。

假定未通过调用创建的任何人脸的图面上描述符中指定的颜色填充**dwEmptyFaceColor**成员。 (请参阅[ **DDSURFACEDESC2** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550340(v=vs.85))结构。)

**请注意**  当前限制：所有多维数据集表面必须大小相同，并且必须是正方形。 多维数据集的人脸可以 MIP 映射。 去除任何色彩与多维数据集映射纹理支持。 与其他纹理支持 alpha 通道和 alpha 的调色板。

 

 

 






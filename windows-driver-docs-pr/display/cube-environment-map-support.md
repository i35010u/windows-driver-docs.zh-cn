---
title: 立体环境贴图支持
description: 立体环境贴图支持
ms.assetid: 41666b17-39b0-4022-925f-538455e41f3a
keywords:
- 映射多维数据集环境
- 环境映射 WDK Direct3D
- 多维数据集环境映射 WDK Direct3D
- 照明 WDK Direct3D
- 反射 WDK Direct3D
- 360度环境 WDK Direct3D
- 实时环境映射 WDK Direct3D
- 循环映射 WDK Direct3D
- 球形映射 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc8d286ae6923610237eb8e6417c74752a4b05e8
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066500"
---
# <a name="cube-environment-map-support"></a>立体环境贴图支持


## <span id="ddk_cube_environment_map_support_gg"></span><span id="DDK_CUBE_ENVIRONMENT_MAP_SUPPORT_GG"></span>


Direct3D 中的多种纹理支持允许将环境映射用于照明和反射。 不过，单地图360级解决方案（例如圆形或球状地图）不够强大，无法被实时广泛使用。 用于实时生成和寻址360度环境的最适合的解决方案是 cubical 的地图，其中包含六个纹理 (面部) 。 每个面部都可以通过在相应方向上指向90度的相机，来生成。 按顶点向量 (normal、反射或折射) 提供给光栅化硬件，然后将这些矢量循环访问多边形，并计算内插向量与 cube 地图表面的交集。 如果应用程序或 API 生成多维数据集环境映射，则驱动程序不需要有关转换矩阵的信息，也不需要在其中定义每个顶点矢量的坐标空间。 这是因为，向量仅用于对在逻辑上位于同一坐标空间中的环境映射进行寻址。

圆形地图的寻址涉及矢量标准化;球形地图的寻址要求使用三角函数。 所有类型的单地图环境都是非线性的：圆形地图非常扭曲，并在其绕附近进行 这样，每次视点变化时，都需要重新创建环境映射，以使中心视图区域变为扭曲。

Cubical 环境地图是指在六个不同方向上使用90度的实部或模拟的摄像机，它们没有这些缺点。 它们可以更快地生成，但需要较少地进行更新，具有较少的扭曲，并可通过使用类似于已用于透视正确纹理映射的公式进行寻址。

通常，多维数据集映射是为复杂的照明和反射提供实时环境映射的最佳选择。

使用 [**D3dDrawPrimitives2**](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb) render 状态机制，可以将多维数据集映射传递给驱动程序。 [FVF](fvf--flexible-vertex-format-.md) 纹理坐标随该纹理坐标集的 FVF 代码01一起传递。

多维数据集映射在世界坐标中定义;也就是说，其世界变换矩阵为恒等矩阵。 如果对对应的纹理坐标索引使用纹理转换，则多维数据集映射可能会显示在不同的空间中。 这些纹理坐标索引将直接查找正面为四，+ z。 默认情况下，Y 处于启动状态。  (u，v) 纹素网格的原点位于每个表面的左上角，以允许在不进行任何其他转换的情况下，通过将相机从立方体中心指向。

**DirectDrawCreateEx** 采用标志来指示要创建的多维数据集映射。 有些人不需要在 API 级别分配，尽管驱动程序可以根据需要进行填充。 Surface 描述符包含包含六位的位域，表示应用程序预期要使用的面部。 当用 **IDirectDrawSurface7：： GetAttachedSurface** 方法进行面部处理时，将跳过 **空** 面部。 每个面的尺寸都可从其曲面描述符中获得，面部 bitcode 字段指示其正面。 有关 **DirectDrawCreateEx** 和 **IDirectDrawSurface7：： GetAttachedSurface**的详细信息，请参阅 DirectDraw SDK 文档。

从 **DirectDrawCreate** 返回的指针实际上是一个指针，指向多维数据集中的第一个非**NULL** 面。 可以通过拍摄图面的 bitcode 来获取面部标识符。 这是传递到 Direct3D SDK 文档) 中 (所述的 **IDirect3DDevice7：： SetTexture** 方法的指针，使此映射可用于多纹理管道。

如果打算将任何图面呈现到，则必须在 \_ 设置 D3DPTEXTURECAPS 立方体贴图 cap 标志的情况下创建多维数据集映射。

不是通过调用创建的任何面都假设使用 surface 描述符的 **dwEmptyFaceColor** 成员中指定的颜色进行填充。  (参阅 [**DDSURFACEDESC2**](/previous-versions/windows/hardware/drivers/ff550340(v=vs.85)) 结构。 ) 

**注意**   当前限制：所有 cube 面都必须相同，并且必须是正方形。 多维数据集面可以是 MIP 映射的。 多维数据集映射纹理不支持任何颜色键控。 与其他纹理一样，支持 alpha 通道和 alpha 调色板。

 

 


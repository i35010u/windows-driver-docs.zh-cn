---
title: 纹理坐标转换
description: 纹理坐标转换
keywords:
- 坐标转换 WDK Direct3D
- 纹理转换 WDK Direct3D
- 转换 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 38c7c28362bbbd31dd9aee298a480157b8b94440
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838939"
---
# <a name="texture-coordinate-transformations"></a>纹理坐标转换


## <span id="ddk_texture_coordinate_transformations_gg"></span><span id="DDK_TEXTURE_COORDINATE_TRANSFORMATIONS_GG"></span>


为最新的直接 X 版本启用纹理坐标转换。

纹理转换是顶点级转换操作。 这些操作可通过任何转换和启用照明的 HAL 驱动程序以及任何 HAL 设备类型执行。

通过定义与每个纹理阶段关联的4X4 矩阵来启用纹理转换。 几何管道软件实现所使用的所有密钥状态和数据结构都在 DDI 级别可用。

使用纹理转换，可以移动纹理坐标，相对于绘制它们的顶点。 纹理转换说明纹理坐标如何移动纹理地图。 每次应用纹理转换时，矩阵都会更改纹理的坐标。 在这些转换中使用标准世界矩阵。

在 API 级别，Direct3D SDK) 文档中的 **IDirect3DDevice7：： SetTransform** 方法 (描述了与当前绑定到 * i * **-** _th_ 纹理阶段的纹理相关联的纹理转换矩阵。 在呈现期间，此矩阵应应用于纹理的纹理坐标。 请注意，可以在不同的阶段使用同一顶点级别的纹理坐标集，这可能会应用不同的纹理。

纹理转换的操作由 Direct3D SDK 文档) 使用 D3DTSS TEXTURETRANSFORMFLAGS 标志 (中所述的 **IDirect3DDevice7：： SetTextureStageState** 方法控制 \_ 。

DirectX SDK 文档中所述的 D3DTEXTURETRANSFORMFLAGS 枚举类型用于控制由纹理坐标转换操作生成的纹理坐标集的维度，并控制是否应对其应用任何透视划分。

D3DTTFF \_ DISABLE 表示纹理坐标直接传递到硬件。

D3DTTFF \_ COUNT *n* 标志的数字表示将存在多少纹理坐标。 请注意，如果使用了投影纹理，则这不一定等于纹理的尺寸。

如果使用了投影纹理，则 \_ 将 D3DTTFF 投影标志设置为指示纹理坐标将除以纹理坐标集) 元素的最后一个 (*th* 计数。 因此，对于2D 投影纹理，此计数为三个，因为前两个元素除以第三个元素，因此，两个浮点数用于2D 纹理查找。 也就是说，D3DTTFF \_ COUNT2 和 D3DTTFF \_ COUNT3 |D3DTTFF \_ 投影指的是2d 纹理。

对于 nonprojected 纹理：

-   D3DTTFF \_ COUNT1 指示光栅区应有一维纹理坐标。

-   D3DTTFF \_ COUNT2 指示光栅图应需要2d 纹理坐标。

-   D3DTTFF \_ COUNT3 指示光栅图应需要3d 纹理坐标。

-   D3DTTFF \_ COUNT4 指示光栅化应期待4d 纹理坐标。

第一个字节对纹理坐标的计数进行编码，纹理坐标应在特定阶段由纹理使用。 如果将此值设置为零，则不会应用任何纹理转换，即使它是由 **IDirect3DDevice7：： SetTransform** 方法定义的。 这是从 "纹理坐标转换" 阶段输出的数字。

传递给纹理转换的纹理坐标的数目由 Direct3D API [FVF](fvf--flexible-vertex-format-.md) 代码定义。

默认情况下 \_ ，D3DTSS TEXTURETRANSFORMFLAGS 默认为 \_ 禁用 D3DTFF，未 \_ 设置 D3DTTFF 投影标志。 纹理转换矩阵默认为4X4 恒等矩阵。

在 nontransform HAL 设备上 (也就是说，需要对主机处理器进行转换操作) 的输出顶点会提供给驱动程序，该驱动程序具有可能不同于 API 级别指定的 FVF 代码。 不支持硬件加速转换和照明的设备仍可进行投影纹理，因此驱动程序必须仍响应 D3DTSS \_ TEXTURETRANSFORMFLAGS。

 

 






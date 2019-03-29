---
title: 纹理坐标转换
description: 纹理坐标转换
ms.assetid: d0857496-a7ce-4e9f-89d9-03c73d6f59e3
keywords:
- 坐标转换 WDK Direct3D
- 纹理转换 WDK Direct3D
- 转换 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bbc2f66a0d2580f74ebbe2b67def773e4886585c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564028"
---
# <a name="texture-coordinate-transformations"></a>纹理坐标转换


## <span id="ddk_texture_coordinate_transformations_gg"></span><span id="DDK_TEXTURE_COORDINATE_TRANSFORMATIONS_GG"></span>


启用纹理坐标转换为最新的直接 X 版本。

纹理转换是顶点级别转换操作。 按任何转换和照明启用 HAL 驱动程序和任何 HAL 设备类型，可以执行这些操作。

通过定义与每个纹理阶段相关联的 4 X 4 矩阵来启用纹理转换。 使用几何管道的软件实现的关键状态和数据结构的所有在 DDI 级别均可用。

使用纹理转换，纹理坐标可以移动，相对于它们所来自的顶点。 纹理转换描述如何将纹理坐标转移纹理贴图中。 每次应用纹理转换时，矩阵将更改的纹理坐标。 这些转换中使用标准世界矩阵。

在 API 级别**IDirect3DDevice7::SetTransform** （Direct3D SDK 文档中所述） 的方法定义了与当前绑定到的纹理的纹理转换矩阵*我***-*** th*纹理阶段。 此矩阵应在呈现期间应用于该纹理的纹理坐标。 请注意，可以在具有单独的纹理转换矩阵，可以应用不同的纹理的不同阶段使用相同的顶点级别的纹理坐标集。

纹理转换的操作受**IDirect3DDevice7::SetTextureStageState** （Direct3D SDK 文档中所述） 的方法使用 D3DTSS\_TEXTURETRANSFORMFLAGS 标志。

DirectX SDK 文档中所述的 D3DTEXTURETRANSFORMFLAGS 枚举类型用于控制生成纹理坐标转换操作，并控制是否有任何的纹理坐标集的维度透视部门应应用于它。

D3DTTFF\_禁用指示，纹理坐标直接传递到硬件。

D3DTTFF 数\_计数*n*标志指示纹理坐标数量将会显示。 请注意，这不会不一定等同于维度的纹理本身，是否使用投影的纹理。

如果使用投影的纹理，D3DTTFF\_预计标志设置为指示是否要作为被除数由最后一个纹理坐标 (计数*th*) 的纹理坐标集的元素。 因此，对于 2D 预计纹理，计数是三种模型，因为前两个元素除以第三，从而导致 2D 纹理查找两个浮点值。 也就是说，这两个 D3DTTFF\_数 2 和 D3DTTFF\_COUNT3 |D3DTTFF\_预计指 2D 纹理。

对于 nonprojected 纹理：

-   D3DTTFF\_COUNT1 指示光栅器应该获得 1d 纹理坐标。

-   D3DTTFF\_数 2 指示光栅器应该获得 2D 纹理坐标。

-   D3DTTFF\_COUNT3 指示光栅器应该获得三维纹理坐标。

-   D3DTTFF\_COUNT4 指示光栅器应该获得 4d 纹理坐标。

第一个字节进行编码的纹理坐标预期要在某个特定阶段使用的纹理的计数。 此项设置为零将导致任何纹理转换，即使已通过定义要应用**IDirect3DDevice7::SetTransform**方法。 这是数，它是从纹理坐标转换阶段的输出。

传递到纹理转换纹理坐标的数由 Direct3D API 定义[FVF](fvf--flexible-vertex-format-.md)代码。

D3DTSS\_TEXTURETRANSFORMFLAGS 默认为 D3DTFF\_已禁用并没有 D3DTTFF\_预计标志设置。 纹理转换矩阵默认为 4 X 4 标识矩阵。

Nontransform 照明 HAL 在设备上 （即，那些需要对主机处理器的转换操作），与可能不同于在 API 级别指定的相应 DDI 级别 FVF 代码驱动程序提供了输出顶点。 不支持硬件加速转换和照明的设备仍可能会执行投影的纹理，并因此驱动程序必须仍然响应 D3DTSS\_TEXTURETRANSFORMFLAGS。

 

 






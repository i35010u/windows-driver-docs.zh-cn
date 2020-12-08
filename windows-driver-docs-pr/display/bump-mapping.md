---
title: 凹凸贴图
description: 凹凸贴图
keywords:
- Direct3D WDK Windows 2000 显示，凹凸映射
- 凹凸映射 WDK Direct3D
- surface wrinkles WDK Direct3D
- surface dimples WDK Direct3D
- wrinkles WDK Direct3D
- dimples WDK Direct3D
- 纹理管理 WDK Direct3D，凹凸映射
- 每像素纹理 WDK Direct3D
- 模拟 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e517cff6b344d94cf2a108b5f020ecd24328bfe
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810411"
---
# <a name="bump-mapping"></a>凹凸贴图


## <span id="ddk_bump_mapping_gg"></span><span id="DDK_BUMP_MAPPING_GG"></span>


使用凹凸映射，可以在表面上显示起皱或 dimpled，而无需对这些 depressions 几何进行建模。 它涉及到 perturbing 根据二维 "凹凸地图" 中提供的信息来看表面法线。 这将导致局部反射模型，其中强度通常是表面法线的一个函数，用于在平滑表面上生成局部变体。 此欺骗仅在 silhouetted 时才有明显，因为在这种情况下，perturbations 在边缘上不再可见。 也就是说，侧面影像后跟模型的行，因此不会 perturbed。 这似乎向图面添加纹理，而不是 modulating 平面的颜色。

因为 Direct3D 的凹凸映射是通过在呈现阶段中纹理地纹理完成的，而不 perturbing 几何，所以它会绕过出现的建模问题。 如果对象为多边形，则网格必须足够长，以便从纹理映射接收 perturbations。 如果该纹理是一个选项，则这是一个缺点。

可以将 Direct3D 中的凹凸映射描述为每像素纹理坐标 perturbation 和镜面环境地图。 Rasterizers 提供有关凹凸地图的轮廓的信息（以增量值为依据），在下一个纹理阶段，系统会将其应用到环境地图的 "您的" 和 "v" 纹理坐标。 增量值以凹凸贴图图面的像素格式进行编码，并通过 D3DTEXTURESTAGESTATETYPE 枚举类型与多纹理混合集成。 有关详细信息，请参阅 DirectX SDK 文档。

此方法允许将场景的照明环境表示在图像环境地图中， () 的扩散或反射效果。 它允许在这种地图中可表示的任意数字、形状、颜色或强度分布。 可以在静态情况下提前创建这些映射，或者使用 blts 动态地为更改灯光源进行更新。

派生自冯氏底纹的传统凹凸贴图方案仅限于恒定颜色和固定偏离曲线的球面光源。 这些功能不需要每像素环境映射的其他纹理寻址功能，并且可以很好地用于漫射光源效果，但无法生成 photorealism 所需的直观结构化反射高光。 将来，通过将环境映射计算直接集成到 Direct3D geometry 管道中，可以更方便使用这种方法。

凹凸映射通常在照片级呈现器中提供。 它可用于大幅增加表面细节效果，而不会将曲面分割到大量小三角形。 与反射效果结合使用时，凹凸地图可以模拟反光面，如湿石头或 pavement。 当三维加速器支持时，可以实时执行此类效果，从而允许动态光源更改。

使用凹凸地图格式创建 DirectDrawSurface 对象时，该纹理被视为 *凹凸地图*。 此对象可使用绑定到纹理阶段的任意纹理绑定到 Direct3D 设备。 通过设置 D3DTOP BUMPENVMAP，可以设置一种程控纹理混合阶段来执行凹凸映射操作 \_ 。 此凹凸地图纹理使用此阶段的纹理坐标标识符指定的挠性顶点格式的纹理坐标，将自身定位在呈现的对象上。 它还遵循指定纹理阶段的控制筛选、包装等。

此纹理中的凹凸值 perturbs 以下纹理使用的纹理坐标，应将该纹理坐标视为镜面或漫射环境图。

### <a name="span-idemulationspanspan-idemulationspanemulation"></a><span id="emulation"></span><span id="EMULATION"></span>枚举

此方法可在支持8位调色板纹理模式的任何硬件上进行模拟。 限制是，环境映射 (在紧随凹凸纹理映射之后的纹理上，) 必须具有恰好为16X16 纹素的分辨率，并且没有筛选。 这由 D3DTEXOPCAPS \_ MAXBUMPENVMAP16X16 标志指示。 其他部分对干扰的环境映射大小没有限制。

启用凹凸映射时，多纹理混合操作 D3DTOP \_ BUMPENVMAP 和 D3DTOP \_ BUMPENVMAPPREMODULATE。 后一项操作是凹凸映射和光泽映射的组合，允许在与凹凸地图数据相同的图面中对反射反射强度进行编码。

在每个阶段，现在提供了四种附加纹理状态：

D3DTSS \_ BUMPENVMAT00

D3DTSS \_ BUMPENVMAT01

D3DTSS \_ BUMPENVMAT10

D3DTSS \_ BUMPENVMAT11

 

 






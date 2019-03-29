---
title: 凹凸贴图
description: 凹凸贴图
ms.assetid: 38c7da06-cfe6-4285-8958-3d1eb22b1bcd
keywords:
- Direct3D WDK Windows 2000 显示，凹凸映射
- 遇到映射 WDK Direct3D
- 图面褶皱 WDK Direct3D
- 图面 dimples WDK Direct3D
- 褶皱 WDK Direct3D
- dimples WDK Direct3D
- 纹理管理 WDK Direct3D 凹凸映射
- 每像素的纹理绘制 WDK Direct3D
- 仿真 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c255f5acce20eeab961da2a3abd343efd6a6a08b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565988"
---
# <a name="bump-mapping"></a>凹凸贴图


## <span id="ddk_bump_mapping_gg"></span><span id="DDK_BUMP_MAPPING_GG"></span>


遇到映射可确保面以显示卷曲或 dimpled 而无需进行几何模型这些凹陷。 它涉及 perturbing 根据信息中的二维表面的法线的角度"凹凸映射"。 这将导致本地反射模型，其中强度是主要的表面法线，以生成平滑的图面上的本地变体的函数。 该圈套是仅当 silhouetted，很明显，因为在这种情况下扰动将不再在边缘中可见。 也就是说，轮廓遵循模型的行，因此不 perturbed。 这看起来将纹理添加到图面上，而不是调制平整表面的颜色。

为 Direct3D 的凹凸贴图由在呈现阶段纹理图面，而无需 perturbing 几何图形，因为它会绕过建模本会出现的问题。 如果对象是多边形，网格必须足够精细以接收从纹理贴图扰动。 如果纹理，则为一个选项，这是一个缺点。

在 Direct3D 中凹凸映射可以被描述为每个像素的漫射和反射量环境映射的纹理坐标 perturbation。 光栅器提供有关轮廓的增量值，它们适用于您的系统和环境的 v 纹理坐标映射中的下一步的纹理阶段方面凹凸映射的信息。 增量值凹凸映射图面上的像素格式进行编码，并且与通过 D3DTEXTURESTAGESTATETYPE 枚举类型的多个纹理值混合处理集成。 有关详细信息，请参阅 DirectX SDK 文档。

此技术使场景而无法表示图像的环境映射 （无论是用于漫射或反射效果） 中的光照环境。 它允许系统正常运行的任何数、 形状、 颜色或可在此类地图中表示的强度分发。 可以为静态的情况下，预先创建或更改使用 blts 光源，动态更新这些映射。

派生自 Phong 着色的传统的凹凸贴图方案被限制为常量颜色和固定的衰减曲线的球面光源。 这些不需要额外纹理寻址的每个像素环境映射的功能和可以适合漫射光照效果，但不能生成所需的照相直观地结构化反射高光。 将来，将通过直接到 Direct3D 几何管道环境映射计算的集成商使用此类技术。

图像逼真的呈现器中，通常提供凹凸映射。 它可以用于显著提高表面细节效果，而不分割到大量的小三角形的面。 当用于反射效果，凹凸图可以模拟反射还粗略的图面，等湿的颗或 pavement。 支持三维加速器，可以实时，允许动态光源更改中执行这种效果。

具有凹凸映射格式创建 DirectDrawSurface 对象，该纹理被视为*凹凸映射*。 此对象可以绑定到使用任何绑定到纹理贴图层的纹理的 Direct3D 设备。 可以设置通过编程方式设置的纹理值混合处理阶段来执行凹凸映射操作通过设置 D3DTOP\_BUMPENVMAP。 此凹凸贴图纹理使用此阶段的纹理坐标标识符指定的灵活顶点格式纹理的坐标将自身定位在呈现的对象。 它也会遵守指定的纹理阶段控制筛选、 自动换行，等等。

在此纹理的凹凸值 perturbs 由紧跟其后的纹理，应被视为反射或漫射环境映射的纹理坐标。

### <a name="span-idemulationspanspan-idemulationspanemulation"></a><span id="emulation"></span><span id="EMULATION"></span>仿真

支持 8 位调色板纹理模式的任何硬件上，可以模拟这种方法。 限制是，所用环境映射 （紧跟凹凸纹理贴图的纹理） 必须具有完全 16 X 16 纹素和未筛选的分辨率。 这将由 D3DTEXOPCAPS\_MAXBUMPENVMAP16X16 标志。 其他部分具有凹凸映射可以干扰环境映射的大小没有限制。

凹凸映射启用了多个纹理混合操作 D3DTOP\_BUMPENVMAP 和 D3DTOP\_BUMPENVMAPPREMODULATE。 后一种操作是凹凸贴图和光泽映射，反射高光反射强度凹凸地图数据作为相同的图面中要编码的组合。

现在，有四个其他纹理状态提供在每个阶段：

D3DTSS\_BUMPENVMAT00

D3DTSS\_BUMPENVMAT01

D3DTSS\_BUMPENVMAT10

D3DTSS\_BUMPENVMAT11

 

 






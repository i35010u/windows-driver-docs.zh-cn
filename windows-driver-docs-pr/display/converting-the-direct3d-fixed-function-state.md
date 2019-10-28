---
title: 转换 Direct3D 固定函数状态
description: 转换 Direct3D 固定函数状态
ms.assetid: bc93d65e-ac16-470d-8c52-db8b1cc74456
keywords:
- 用户模式显示驱动程序 WDK Windows Vista，转换 Direct3D fixed 函数状态
- fixed 函数状态转换 WDK 显示
- 转换 Direct3D fixed 函数状态
- 转换器 WDK Windows Vista Direct3D
- 像素着色器转换器 WDK 显示
- 顶点着色器转换器 WDK 显示
- 着色器转换器 WDK 显示
- 纹理阶段状态 WDK 显示
- 呈现状态 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7378da680c6ec175886db74c2833668b3adb17f2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839790"
---
# <a name="converting-the-direct3d-fixed-function-state"></a>转换 Direct3D 固定函数状态


如果用户模式显示驱动程序支持每个着色器类型的版本2.0 或更高版本，则 Microsoft Direct3D 运行时会将 Direct3D 固定函数状态转换为顶点或像素着色器版本2.0。 但是，运行时不会转换着色器版本。 例如，如果应用程序使用顶点或像素着色器版本1.1，则版本1.1 会转换为用户模式显示驱动程序，而不管驱动程序是否支持着色器版本2.0 或更高版本。 可变顶点格式（FVF）代码用于固定函数处理。

### <a name="span-idconverter_features_for_directx_versionsspanspan-idconverter_features_for_directx_versionsspanconverter-features-for-directx-versions"></a><span id="converter_features_for_directx_versions"></span><span id="CONVERTER_FEATURES_FOR_DIRECTX_VERSIONS"></span>DirectX 版本的转换器功能

固定函数顶点和像素着色器转换器的工作方式取决于所用的 Microsoft DirectX 版本：

-   DirectX 9。0

    Fixed 函数顶点和像素着色器转换器可用于 Windows Vista 显示器驱动程序模型。

    默认情况下，将启用转换器。

    使用固定函数顶点或像素着色器转换器时，将禁用纯设备。 当应用程序请求纯设备时，Direct3D 运行时将创建 HAL 设备。

    运行时支持混合顶点处理。

    软件顶点处理始终使用固定函数顶点着色器转换器。

    当驱动程序支持顶点着色器版本2.0 或更高版本时，硬件顶点处理使用固定函数顶点着色器转换器。

    当驱动程序支持像素着色器版本2.0 或更高版本时，硬件顶点处理使用固定函数像素着色器转换器。

    在混合顶点处理模式下，当为硬件启用固定函数顶点着色器转换器时，float 常量的数量将设置为硬件可支持的值。

-   DirectX 8.0 及更早版本

    Fixed 函数顶点和像素着色器转换器只能与 Windows Vista 显示器驱动程序模型一起使用。

    默认情况下，将启用转换器。

    软件顶点处理不支持固定函数顶点着色器转换器。

    当驱动程序支持顶点着色器版本2.0 或更高版本时，硬件顶点处理使用固定函数顶点着色器转换器。

    当驱动程序支持像素着色器版本2.0 或更高版本时，硬件顶点处理使用固定函数像素着色器转换器。

    **请注意**   directx 8.0 之前的 directx 版本，则在*Ddraw*中实现了用于着色器映射代码的固定函数。

     

### <a name="span-idunused_user_mode_display_driver_functionsspanspan-idunused_user_mode_display_driver_functionsspanunused-user-mode-display-driver-functions"></a><span id="unused_user_mode_display_driver_functions"></span><span id="UNUSED_USER_MODE_DISPLAY_DRIVER_FUNCTIONS"></span>未使用的用户模式显示驱动程序函数

当启用固定函数顶点着色器转换器时，Direct3D 运行时不调用以下[用户模式显示驱动程序函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)：

-   [**MultiplyTransform**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_multiplytransform)

-   [**SetTransform**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_settransform)

-   [**SetMaterial**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_setmaterial)

-   [**SetLight**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_setlight)

-   [**CreateLight**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createlight)

-   [**DestroyLight**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_destroylight)

### <a name="span-idunused_render_statesspanspan-idunused_render_statesspanunused-render-states"></a><span id="unused_render_states"></span><span id="UNUSED_RENDER_STATES"></span>未使用的呈现状态

当启用固定函数顶点着色器转换器时，Direct3D 运行时（或者，如果通过错误传递，驱动程序可能会忽略）以下呈现状态：

-   D3DRS\_VERTEXBLEND

-   D3DRS\_INDEXEDVERTEXBLENDENABLE

-   D3DRS\_TWEENFACTOR

-   D3DRS\_FOGVERTEXMODE

-   D3DRS\_照明

-   D3DRS\_环境

-   D3DRS\_COLORVERTEX

-   D3DRS\_LOCALVIEWER

-   D3DRS\_DIFFUSEMATERIALSOURCE

-   D3DRS\_SPECULARMATERIALSOURCE

-   D3DRS\_AMBIENTMATERIALSOURCE

-   D3DRS\_EMISSIVEMATERIALSOURCE

-   D3DRS\_POINTSCALEENABLE

-   D3DRS\_POINTSCALE\_

-   D3DRS\_POINTSCALE\_B

-   D3DRS\_POINTSCALE\_C

-   D3DRS\_NORMALIZENORMALS

### <a name="span-idignored_texture_stage_statesspanspan-idignored_texture_stage_statesspanignored-texture-stage-states"></a><span id="ignored_texture_stage_states"></span><span id="IGNORED_TEXTURE_STAGE_STATES"></span>忽略的纹理阶段状态

Direct3D 运行时将所有纹理阶段状态传递给驱动程序。 启用固定函数像素着色器转换器时，驱动程序应忽略以下纹理阶段状态：

-   D3DTSS\_COLOROP

-   D3DTSS\_COLORARG1

-   D3DTSS\_COLORARG2

-   D3DTSS\_ALPHAOP

-   D3DTSS\_ALPHAARG1

-   D3DTSS\_ALPHAARG2

-   D3DTSS\_BUMPENVMAT00

-   D3DTSS\_BUMPENVMAT01

-   D3DTSS\_BUMPENVMAT10

-   D3DTSS\_BUMPENVMAT11

-   D3DTSS\_BUMPENVLSCALE

-   D3DTSS\_BUMPENVLOFFSET

-   D3DTSS\_COLORARG0

-   D3DTSS\_ALPHAARG0

-   D3DTSS\_RESULTARG

-   D3DTSS\_常量

 

 






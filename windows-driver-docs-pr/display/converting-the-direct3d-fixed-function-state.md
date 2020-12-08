---
title: 转换 Direct3D 固定函数状态
description: 转换 Direct3D 固定函数状态
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
ms.openlocfilehash: 5c7eb97ae5bb8db0abc1f5c5055ca517829d6e3c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810113"
---
# <a name="converting-the-direct3d-fixed-function-state"></a>转换 Direct3D 固定函数状态


如果用户模式显示驱动程序支持每个着色器类型的版本2.0 或更高版本，则 Microsoft Direct3D 运行时会将 Direct3D 固定函数状态转换为顶点或像素着色器版本2.0。 但是，运行时不会转换着色器版本。 例如，如果应用程序使用顶点或像素着色器版本1.1，则版本1.1 会转换为用户模式显示驱动程序，而不管驱动程序是否支持着色器版本2.0 或更高版本。 可变顶点格式 (FVF) 代码用于固定函数处理。

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

    **注意**   对于 DirectX 8.0 之前的 DirectX 版本，将在 *Ddraw.dll* 中实现着色器映射代码的固定函数。

     

### <a name="span-idunused_user_mode_display_driver_functionsspanspan-idunused_user_mode_display_driver_functionsspanunused-user-mode-display-driver-functions"></a><span id="unused_user_mode_display_driver_functions"></span><span id="UNUSED_USER_MODE_DISPLAY_DRIVER_FUNCTIONS"></span>未使用的 User-Mode 显示驱动程序函数

当启用固定函数顶点着色器转换器时，Direct3D 运行时不调用以下 [用户模式显示驱动程序函数](/windows-hardware/drivers/ddi/index) ：

-   [**MultiplyTransform**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_multiplytransform)

-   [**SetTransform**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_settransform)

-   [**SetMaterial**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_setmaterial)

-   [**SetLight**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_setlight)

-   [**CreateLight**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createlight)

-   [**DestroyLight**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_destroylight)

### <a name="span-idunused_render_statesspanspan-idunused_render_statesspanunused-render-states"></a><span id="unused_render_states"></span><span id="UNUSED_RENDER_STATES"></span>未使用的呈现状态

当启用固定函数顶点着色器转换器时，如果) 通过错误传递，则该驱动程序将不会通过 Direct3D 运行时 (传递以下呈现状态：

-   D3DRS \_ VERTEXBLEND

-   D3DRS \_ INDEXEDVERTEXBLENDENABLE

-   D3DRS \_ TWEENFACTOR

-   D3DRS \_ FOGVERTEXMODE

-   D3DRS \_ 照明

-   D3DRS \_ 环境

-   D3DRS \_ COLORVERTEX

-   D3DRS \_ LOCALVIEWER

-   D3DRS \_ DIFFUSEMATERIALSOURCE

-   D3DRS \_ SPECULARMATERIALSOURCE

-   D3DRS \_ AMBIENTMATERIALSOURCE

-   D3DRS \_ EMISSIVEMATERIALSOURCE

-   D3DRS \_ POINTSCALEENABLE

-   D3DRS \_ POINTSCALE \_

-   D3DRS \_ POINTSCALE \_ B

-   D3DRS \_ POINTSCALE \_ C

-   D3DRS \_ NORMALIZENORMALS

### <a name="span-idignored_texture_stage_statesspanspan-idignored_texture_stage_statesspanignored-texture-stage-states"></a><span id="ignored_texture_stage_states"></span><span id="IGNORED_TEXTURE_STAGE_STATES"></span>忽略的纹理阶段状态

Direct3D 运行时将所有纹理阶段状态传递给驱动程序。 启用固定函数像素着色器转换器时，驱动程序应忽略以下纹理阶段状态：

-   D3DTSS \_ COLOROP

-   D3DTSS \_ COLORARG1

-   D3DTSS \_ COLORARG2

-   D3DTSS \_ ALPHAOP

-   D3DTSS \_ ALPHAARG1

-   D3DTSS \_ ALPHAARG2

-   D3DTSS \_ BUMPENVMAT00

-   D3DTSS \_ BUMPENVMAT01

-   D3DTSS \_ BUMPENVMAT10

-   D3DTSS \_ BUMPENVMAT11

-   D3DTSS \_ BUMPENVLSCALE

-   D3DTSS \_ BUMPENVLOFFSET

-   D3DTSS \_ COLORARG0

-   D3DTSS \_ ALPHAARG0

-   D3DTSS \_ RESULTARG

-   D3DTSS \_ 常量

 


---
title: 将 Direct3D 固定函数状态转换
description: 将 Direct3D 固定函数状态转换
ms.assetid: bc93d65e-ac16-470d-8c52-db8b1cc74456
keywords:
- 用户模式显示驱动程序 WDK Windows Vista，Direct3D 固定函数状态进行相互转换
- 显示固定函数状态转换 WDK
- 转换 Direct3D 固定函数状态
- 转换器 WDK Windows Vista Direct3D
- 显示像素着色器转换器 WDK
- 顶点着色器转换器 WDK 显示
- 着色器转换器 WDK 显示
- 纹理阶段状态 WDK 显示
- 呈现 WDK 显示的状态
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2eb742e9c11b271d408abd2f310936f62b5ebf22
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541193"
---
# <a name="converting-the-direct3d-fixed-function-state"></a>将 Direct3D 固定函数状态转换


Microsoft Direct3D 运行时将 Direct3D 固定函数状态转换为顶点或像素着色器版本 2.0 中，如果用户模式显示驱动程序支持为每个着色器类型的版本 2.0 或更高版本。 但是，在运行时不转换着色器版本。 例如，如果应用程序使用顶点或像素着色器版本 1.1，则版本 1.1 中传递未转换到用户模式显示驱动程序，无论该驱动程序是否支持着色器版本 2.0 或更高版本。 与固定函数处理使用灵活的顶点格式 (FVF) 代码。

### <a name="span-idconverterfeaturesfordirectxversionsspanspan-idconverterfeaturesfordirectxversionsspanconverter-features-for-directx-versions"></a><span id="converter_features_for_directx_versions"></span><span id="CONVERTER_FEATURES_FOR_DIRECTX_VERSIONS"></span>DirectX 版本的转换器功能

如何修复函数顶点和像素着色器转换器工作取决于使用的 Microsoft DirectX 的版本：

-   DirectX 9.0

    Windows Vista 显示器驱动程序模型可以处理固定函数顶点和像素着色器转换器。

    默认情况下启用的转换器。

    使用固定函数顶点或像素着色器转换器时，纯设备已被禁用。 当应用程序请求纯设备时，Direct3D 运行时创建的 HAL 设备。

    运行时支持混合的顶点处理。

    软件顶点处理始终使用固定函数顶点着色器转换器。

    当驱动程序支持顶点着色器版本 2.0 或更高版本时，硬件顶点处理使用固定函数顶点着色器转换器。

    当驱动程序支持像素着色器版本 2.0 或更高版本时，硬件顶点处理使用固定功能像素着色器转换器。

    混合的顶点处理模式有关的硬件，启用固定函数顶点着色器转换器浮点常量数设置到硬件能够支持。

-   DirectX 8.0 及更早版本

    Windows Vista 显示器驱动程序模型仅可以处理固定函数顶点和像素着色器转换器。

    默认情况下启用的转换器。

    不支持软件顶点处理固定函数顶点着色器转换器。

    当驱动程序支持顶点着色器版本 2.0 或更高版本时，硬件顶点处理使用固定函数顶点着色器转换器。

    当驱动程序支持像素着色器版本 2.0 或更高版本时，硬件顶点处理使用固定功能像素着色器转换器。

    **请注意**  着色器映射代码的固定的函数中的 DirectX 版本的 DirectX 8.0 之前，实现*Ddraw.dll*。

     

### <a name="span-idunusedusermodedisplaydriverfunctionsspanspan-idunusedusermodedisplaydriverfunctionsspanunused-user-mode-display-driver-functions"></a><span id="unused_user_mode_display_driver_functions"></span><span id="UNUSED_USER_MODE_DISPLAY_DRIVER_FUNCTIONS"></span>未使用的用户模式显示驱动程序函数

以下[用户模式显示驱动程序函数](https://msdn.microsoft.com/library/windows/hardware/ff570118)启用固定函数顶点着色器转换器时不调用 Direct3D 运行时：

-   [**MultiplyTransform**](https://msdn.microsoft.com/library/windows/hardware/ff568516)

-   [**SetTransform**](https://msdn.microsoft.com/library/windows/hardware/ff569687)

-   [**SetMaterial**](https://msdn.microsoft.com/library/windows/hardware/ff569540)

-   [**SetLight**](https://msdn.microsoft.com/library/windows/hardware/ff569539)

-   [**CreateLight**](https://msdn.microsoft.com/library/windows/hardware/ff540658)

-   [**DestroyLight**](https://msdn.microsoft.com/library/windows/hardware/ff552778)

### <a name="span-idunusedrenderstatesspanspan-idunusedrenderstatesspanunused-render-states"></a><span id="unused_render_states"></span><span id="UNUSED_RENDER_STATES"></span>未使用的呈现状态

以下的呈现状态 Direct3D 运行时不会传递 （或者，如果错误地传递可以忽略由驱动程序） 时启用固定函数顶点着色器转换器：

-   D3DRS\_VERTEXBLEND

-   D3DRS\_INDEXEDVERTEXBLENDENABLE

-   D3DRS\_TWEENFACTOR

-   D3DRS\_FOGVERTEXMODE

-   D3DRS\_照明

-   D3DRS\_AMBIENT

-   D3DRS\_COLORVERTEX

-   D3DRS\_LOCALVIEWER

-   D3DRS\_DIFFUSEMATERIALSOURCE

-   D3DRS\_SPECULARMATERIALSOURCE

-   D3DRS\_AMBIENTMATERIALSOURCE

-   D3DRS\_EMISSIVEMATERIALSOURCE

-   D3DRS\_POINTSCALEENABLE

-   D3DRS\_POINTSCALE\_A

-   D3DRS\_POINTSCALE\_B

-   D3DRS\_POINTSCALE\_C

-   D3DRS\_NORMALIZENORMALS

### <a name="span-idignoredtexturestagestatesspanspan-idignoredtexturestagestatesspanignored-texture-stage-states"></a><span id="ignored_texture_stage_states"></span><span id="IGNORED_TEXTURE_STAGE_STATES"></span>已忽略的纹理阶段状态

Direct3D 运行时将传递所有纹理阶段状态到驱动程序。 启用固定功能像素着色器转换器时，则驱动程序应忽略以下的纹理阶段状态：

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

 

 






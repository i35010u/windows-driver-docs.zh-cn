---
title: 用户模式显示驱动程序
description: 用户模式显示驱动程序
ms.assetid: cb4e8fb9-a2f0-43b2-ae9e-ccffa850ccd7
keywords:
- 显示驱动程序模型 WDK Windows Vista，用户模式显示驱动程序
- Windows Vista 显示器驱动程序模型 WDK，用户模式显示驱动程序
- 用户模式显示驱动程序 WDK Windows Vista，关于用户模式显示驱动程序
- 用户模式显示驱动程序 WDK Windows Vista
- Direct3D WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9cb3555b1ab291e53e3c3521eb4b82c9ecec2151
ms.sourcegitcommit: ee3e2259aafc844cc43cce62299a72649cf89212
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2020
ms.locfileid: "91353592"
---
# <a name="user-mode-display-drivers"></a>用户模式显示驱动程序


## <span id="ddk_user_mode_display_drivers_gg"></span><span id="DDK_USER_MODE_DISPLAY_DRIVERS_GG"></span>

图形硬件供应商必须为其显示适配器编写用户模式显示驱动程序。 用户模式显示驱动程序是一个动态链接库， (DLL) 由 Microsoft Direct3D 运行时加载。 用户模式显示驱动程序至少必须支持 [Direct3D 版本 9 DDI](/windows-hardware/drivers/ddi/d3dumddi/index)。 用户模式显示驱动程序还可以支持 [Direct3D 版本 10 DDI](/windows-hardware/drivers/ddi/d3d10umddi/)。 用户模式显示驱动程序可包含一个 DLL，该 DLL 支持 Direct3D 版本 9 DDI 和 Direct3D 版本 10 DDI，也可以包含两个单独的 Dll，一个用于版本9，另一个用于 Direct3D DDI 的第10版。 以下主题讨论用户模式显示驱动程序的各个方面：

[返回从运行时函数收到的错误代码](returning-error-codes-received-from-runtime-functions.md)

[处理 E \_ INVALIDARG 返回值](handling-the-e-invalidarg-return-value.md)

[处理着色器代码](processing-shader-codes.md)

[转换 Direct3D 固定函数状态](converting-the-direct3d-fixed-function-state.md)

[复制深度模具值](copying-depth-stencil-values.md)

[验证索引值](validating-index-values.md)

[支持多个处理器](supporting-multiple-processors.md)

[处理多个锁](handling-multiple-locks.md)

[DirectX 视频加速 2.0](directx-video-acceleration-2-0.md)

[支持 Direct3D 版本 10](supporting-direct3d-version-10.md)

[支持 Direct3D 版本 10.1](supporting-direct3d-version-10-1.md)

[支持 Direct3D 版本 11](supporting-direct3d-version-11.md)

[处理高清视频](processing-high-definition-video.md)

[保护视频内容](protecting-video-content.md)

[验证覆盖支持](verifying-overlay-support.md)

[支持 OpenGL 增强](supporting-opengl-enhancements.md)

[管理多个 GPU 方案的资源](managing-resources-for-multiple-gpu-scenarios.md)

 


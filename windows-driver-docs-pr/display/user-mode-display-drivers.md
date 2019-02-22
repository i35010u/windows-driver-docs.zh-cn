---
title: 用户模式显示驱动程序
description: 用户模式显示驱动程序
ms.assetid: cb4e8fb9-a2f0-43b2-ae9e-ccffa850ccd7
keywords:
- 显示驱动程序模型 WDK Windows Vista 中，用户模式显示驱动程序
- Windows Vista 显示器驱动程序模型 WDK，用户模式显示驱动程序
- 用户模式显示驱动程序 WDK Windows Vista、 有关用户模式显示驱动程序
- 用户模式显示驱动程序 WDK Windows Vista
- Direct3D WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00dd1da159a813e24e99989f98bf053d3d46e5c9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554210"
---
# <a name="user-mode-display-drivers"></a>用户模式显示驱动程序


## <span id="ddk_user_mode_display_drivers_gg"></span><span id="DDK_USER_MODE_DISPLAY_DRIVERS_GG"></span>


图形硬件供应商必须为其显示适配器编写用户模式显示驱动程序。 用户模式显示驱动程序是 Microsoft Direct3D 运行时加载的动态链接库 (DLL)。 必须至少支持用户模式显示驱动程序[Direct3D 版本 9 DDI](https://msdn.microsoft.com/library/windows/hardware/ff552927)。 此外可以支持用户模式显示驱动程序[Direct3D 版本 10 DDI](https://msdn.microsoft.com/library/windows/hardware/ff552909)。 用户模式显示驱动程序可以包含一个支持这两个 Direct3D 9 DDI 和 Direct3D 版本 10 DDI，也可以包含两个单独的 Dll，一个用于版本 9，另一个用于 Direct3D DDI 10 版本的 DLL。 以下主题讨论用户模式显示驱动程序的各个方面：

[返回运行时函数从收到的错误代码](returning-error-codes-received-from-runtime-functions.md)

[处理电子\_INVALIDARG 返回值](handling-the-e-invalidarg-return-value.md)

[处理着色器代码](processing-shader-codes.md)

[将 Direct3D 固定函数状态转换](converting-the-direct3d-fixed-function-state.md)

[将深度模具的值复制](copying-depth-stencil-values.md)

[验证索引值](validating-index-values.md)

[支持多个处理器](supporting-multiple-processors.md)

[处理多个锁](handling-multiple-locks.md)

[DirectX 视频加速 2.0](directx-video-acceleration-2-0.md)

[支持 Direct3D 版本 10](supporting-direct3d-version-10.md)

[支持 Direct3D 版本 10.1](supporting-direct3d-version-10-1.md)

[支持 Direct3D 版本 11](supporting-direct3d-version-11.md)

[处理高清晰视频](processing-high-definition-video.md)

[保护视频内容](protecting-video-content.md)

[验证覆盖的支持](verifying-overlay-support.md)

[支持 OpenGL 的增强功能](supporting-opengl-enhancements.md)

[管理资源的多个 GPU 方案](managing-resources-for-multiple-gpu-scenarios.md)

 

 






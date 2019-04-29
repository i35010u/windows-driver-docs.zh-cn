---
title: Windows 7 显示驱动程序 (WDDM 1.1) 的新增功能
description: Windows 7 显示驱动程序 (WDDM 1.1) 的新增功能
ms.assetid: 516A9C56-7ABC-49F4-8E92-3B6C3DB78CF6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d08fc2da06f6b9296128b24fc1c51afe7d9eec0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391183"
---
# <a name="whats-new-for-windows-7-display-drivers-wddm-11"></a>Windows 7 显示驱动程序 (WDDM 1.1) 的新增功能


Windows Driver Kit (WDK) 一起发布与 Windows 7 包括用于用户模式显示驱动程序和内核模式显示微型端口驱动程序的新功能。 它还包括安装针对 Windows 7 和新 Microsoft Win32 Api 的信息可在 Windows 7 中的控制桌面显示安装程序进行了优化的显示器驱动程序的要求的更新。

### <a name="span-idnewwindows7featuresforusermodedisplaydriversspanspan-idnewwindows7featuresforusermodedisplaydriversspannew-windows-7-features-for-user-mode-display-drivers"></a><span id="new_windows_7_features_for_user_mode_display_drivers"></span><span id="NEW_WINDOWS_7_FEATURES_FOR_USER_MODE_DISPLAY_DRIVERS"></span>用户模式显示驱动程序的新 Windows 7 功能

用户模式显示驱动程序的新 Windows 7 功能包括：

[处理高清晰视频](processing-high-definition-video.md)

[保护视频内容](protecting-video-content.md)

[验证覆盖的支持](verifying-overlay-support.md)

[支持 Direct3D 版本 11](supporting-direct3d-version-11.md)

[支持 OpenGL 的增强功能](supporting-opengl-enhancements.md)

[管理资源的多个 GPU 方案](managing-resources-for-multiple-gpu-scenarios.md)

Windows 7 还提供了 Microsoft Direct3D 版本 10.1 扩展的格式感知功能。 有关扩展的格式感知的详细信息，请参阅[支持扩展格式感知](supporting-extended-format-awareness.md)。

### <a name="span-idconnectingandconfiguringdisplaysspanspan-idconnectingandconfiguringdisplaysspanconnecting-and-configuring-displays"></a><span id="connecting_and_configuring_displays"></span><span id="CONNECTING_AND_CONFIGURING_DISPLAYS"></span>连接和配置显示

有关新的 Win32 Api，用于控制桌面显示安装程序的信息，请参阅[连接和配置显示](connecting-and-configuring-displays.md)。

### <a name="span-idnewwindows7featuresforkernelmodedisplayminiportdriversspanspan-idnewwindows7featuresforkernelmodedisplayminiportdriversspannew-windows-7-features-for-kernel-mode-display-miniport-drivers"></a><span id="new_windows_7_features_for_kernel_mode_display_miniport_drivers"></span><span id="NEW_WINDOWS_7_FEATURES_FOR_KERNEL_MODE_DISPLAY_MINIPORT_DRIVERS"></span>内核模式显示微型端口驱动程序的新 Windows 7 功能

你可以开发内核模式显示微型端口驱动程序在 Windows 7 上运行具有以下功能：

[连接和配置显示-DDIs](ccd-ddis.md)

[GDI 硬件加速](gdi-hardware-acceleration.md)

### <a name="span-idnewinfrequirementsspanspan-idnewinfrequirementsspannew-inf-requirements"></a><span id="new_inf_requirements"></span><span id="NEW_INF_REQUIREMENTS"></span>新的 INF 要求

显示器驱动程序，写入到 Windows Vista 显示器驱动程序模型和模型的 Windows 7 功能进行了优化的 INF 文件需要多个更新。 有关这些更新的信息，请参阅[安装显示驱动程序进行了优化适用于 Windows 7 和更高版本](installing-display-drivers-optimized-for-windows-7-and-later.md)。

### <a name="span-idgpuviewspanspan-idgpuviewspangpuview"></a><span id="gpuview"></span><span id="GPUVIEW"></span>GPUView

Windows 7 操作系统的版本还引入了 GPUView (GPUView.exe)，这是新的开发工具，用于监视性能的图形处理单元 (GPU)。 有关 GPUView 详细信息，请参阅[使用 GPUView](using-gpuview.md)。

 

 






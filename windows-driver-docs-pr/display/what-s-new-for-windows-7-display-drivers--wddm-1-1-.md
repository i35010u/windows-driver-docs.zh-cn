---
title: Windows 7 显示驱动程序 (WDDM 1.1) 的新增功能
description: Windows 7 显示驱动程序 (WDDM 1.1) 的新增功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 937942f9e1d2dca7797918aad47c501d123a2512
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826037"
---
# <a name="whats-new-for-windows-7-display-drivers-wddm-11"></a>Windows 7 显示驱动程序 (WDDM 1.1) 的新增功能


Windows 7 附带的 Windows 驱动程序工具包 (WDK) 包含用户模式显示驱动程序和内核模式显示微型端口驱动程序的新增功能。 它还包括对安装适用于 Windows 7 的显示驱动程序的要求的更新，以及有关 Windows 7 中提供的用于控制桌面显示器设置的新 Microsoft Win32 Api 的信息。

### <a name="span-idnew_windows_7_features_for_user_mode_display_driversspanspan-idnew_windows_7_features_for_user_mode_display_driversspannew-windows-7-features-for-user-mode-display-drivers"></a><span id="new_windows_7_features_for_user_mode_display_drivers"></span><span id="NEW_WINDOWS_7_FEATURES_FOR_USER_MODE_DISPLAY_DRIVERS"></span>用于 User-Mode 显示驱动程序的新 Windows 7 功能

用户模式显示驱动程序的新 Windows 7 功能包括：

[处理高清视频](processing-high-definition-video.md)

[保护视频内容](protecting-video-content.md)

[验证覆盖支持](verifying-overlay-support.md)

[支持 Direct3D 版本 11](supporting-direct3d-version-11.md)

[支持 OpenGL 增强](supporting-opengl-enhancements.md)

[管理多个 GPU 方案的资源](managing-resources-for-multiple-gpu-scenarios.md)

Windows 7 还提供对 Microsoft Direct3D 版本10.1 的扩展格式感知。 有关扩展格式识别的详细信息，请参阅 [支持扩展格式感知](supporting-extended-format-awareness.md)。

### <a name="span-idconnecting_and_configuring_displaysspanspan-idconnecting_and_configuring_displaysspanconnecting-and-configuring-displays"></a><span id="connecting_and_configuring_displays"></span><span id="CONNECTING_AND_CONFIGURING_DISPLAYS"></span>连接和配置显示

有关控制桌面显示器设置的新 Win32 Api 的信息，请参阅 [连接和配置显示](connecting-and-configuring-displays.md)。

### <a name="span-idnew_windows_7_features_for_kernel_mode_display_miniport_driversspanspan-idnew_windows_7_features_for_kernel_mode_display_miniport_driversspannew-windows-7-features-for-kernel-mode-display-miniport-drivers"></a><span id="new_windows_7_features_for_kernel_mode_display_miniport_drivers"></span><span id="NEW_WINDOWS_7_FEATURES_FOR_KERNEL_MODE_DISPLAY_MINIPORT_DRIVERS"></span>用于 Kernel-Mode 显示微型端口驱动程序的新 Windows 7 功能

你可以开发内核模式显示微型端口驱动程序，以便在 Windows 7 上运行，具有以下功能：

[连接和配置显示-DDIs](ccd-ddis.md)

[GDI 硬件加速](gdi-hardware-acceleration.md)

### <a name="span-idnew_inf_requirementsspanspan-idnew_inf_requirementsspannew-inf-requirements"></a><span id="new_inf_requirements"></span><span id="NEW_INF_REQUIREMENTS"></span>新 INF 要求

对于写入 Windows Vista 显示器驱动程序模型的显示驱动程序的 INF 文件，如果对该模型的 Windows 7 功能进行了优化，则需要进行多次更新。 有关这些更新的详细信息，请参阅 [安装针对 Windows 7 和更高版本优化的显示驱动程序](installing-display-drivers-optimized-for-windows-7-and-later.md)。

### <a name="span-idgpuviewspanspan-idgpuviewspangpuview"></a><span id="gpuview"></span><span id="GPUVIEW"></span>GPUView

Windows 7 操作系统的版本还引入了 GPUView ( # A0) ，这是一个新的开发工具，用于监视图形处理单元 (GPU) 的性能。 有关 GPUView 的详细信息，请参阅 [使用 GPUView](using-gpuview.md)。

 

 






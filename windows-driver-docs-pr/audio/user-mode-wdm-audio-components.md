---
title: 用户模式 WDM 音频组件
description: 用户模式 WDM 音频组件
keywords:
- 用户模式组件 WDK 音频
- Winmm.dll 系统组件 WDK 音频
- WDMAud 系统驱动程序 WDK 音频
- DirectSound 系统组件 WDK 音频
- DirectMusic 系统组件 WDK 音频
- Windows 音频服务 WDK 音频
- waveOut API WDK 音频
- 音频服务 WDK
- WDMAud 系统驱动程序
- 'WDMAud 系统驱动程序，用户模式 (WDMAud. winspool.drv) '
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cbf156007d929cef26fd07f58fce971de9cc8003
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798833"
---
# <a name="user-mode-wdm-audio-components"></a>用户模式 WDM 音频组件


## <span id="user_mode_wdm_audio_components"></span><span id="USER_MODE_WDM_AUDIO_COMPONENTS"></span>


用户模式 Microsoft Windows 驱动模型 (WDM) 音频组件如下：

-   Winmm.dll 系统组件

-   WDMAud 系统驱动程序

-   DirectSound 系统组件

-   DirectMusic 系统组件

-   Windows 音频服务

### <a name="span-idwinmm_system_componentspanspan-idwinmm_system_componentspanwinmm-system-component"></a><span id="winmm_system_component"></span><span id="WINMM_SYSTEM_COMPONENT"></span>Winmm.dll 系统组件

Winmm.dll 系统组件 ( # A0 及其16位对应项，Mmsystem.dll) 实现 Microsoft Windows 多媒体 Api 波浪 *xxx*、midi *xxx*、混音器 *xxx* 和 aux *xxx* (参阅 Microsoft Windows SDK 文档) 。 Winmm.dll 组件使用 WDMAud 系统驱动程序将 Winmm.dll API 调用转换为内核流式处理 i/o 请求。

### <a name="span-idwdmaud_system_driverspanspan-idwdmaud_system_driverspanwdmaud-system-driver"></a><span id="wdmaud_system_driver"></span><span id="WDMAUD_SYSTEM_DRIVER"></span>WDMAud 系统驱动程序

用户模式 WDMAud 系统驱动程序 (Wdmaud. winspool.drv) 与内核模式 WDMAud 系统驱动程序 ( # A0) 配对。 同时，WDMAud 系统驱动程序在 Winmm.dll API 调用和内核流式处理 i/o 请求之间进行转换。 内核模式模式 WDMAud 驱动程序是 SysAudio 系统驱动程序的客户端。

### <a name="span-iddirectsound_system_componentspanspan-iddirectsound_system_componentspandirectsound-system-component"></a><span id="directsound_system_component"></span><span id="DIRECTSOUND_SYSTEM_COMPONENT"></span>DirectSound 系统组件

 ( # A0) 的 DirectSound 系统组件支持 DirectSound API (参阅 Microsoft Windows SDK 文档) 。 DirectSound 组件是 SysAudio 驱动程序的客户端。 如果硬件混合可用，SysAudio 驱动程序会将 DirectSound 硬件缓冲区直接连接到呈现设备。 否则，SysAudio 驱动程序会将 DirectSound 软件缓冲区连接到 KMixer 系统驱动程序。 有关详细信息，请参阅 [使用 DirectSound Software 和硬件缓冲区呈现波形内容](rendering-wave-content-using-directsound-software-and-hardware-buffers.md)。

### <a name="span-iddirectmusic_system_componentspanspan-iddirectmusic_system_componentspandirectmusic-system-component"></a><span id="directmusic_system_component"></span><span id="DIRECTMUSIC_SYSTEM_COMPONENT"></span>DirectMusic 系统组件

 ( # A0) 的 DirectMusic 系统组件支持 DirectMusic API (参阅 Microsoft Windows SDK 文档) 。 此组件将对 DirectMusic API 的调用转换为 WDM 音频设备的 i/o 请求。 DirectMusic 组件是 SysAudio 系统驱动程序的客户端。

### <a name="span-idwindows_audio_servicesspanspan-idwindows_audio_servicesspanwindows-audio-services"></a><span id="windows_audio_services"></span><span id="WINDOWS_AUDIO_SERVICES"></span>Windows 音频服务

在 Windows XP 和更高版本中，Windows 音频服务组件 ( # A0) 管理基于 Windows 的程序的音频设备。 停止 Windows 音频服务可防止音频设备和效果正常运行。 如果禁用了音频服务，则任何其他服务 (包括直接依赖于它们) 的 WDM 音频驱动程序都将无法启动。 在 Windows XP 和更高版本的 Home Edition、Professional 和 Server 版本中，音频服务默认配置为自动启动。 但是，在高级服务器、数据中心和 Windows Server 2003 和更高版本的 Web 服务器版本中，音频服务在默认情况下处于禁用状态。 禁用音频服务时，安装音频设备不会启用它们--只有在管理员显式配置了音频服务时才会自动运行。 有关启动和停止 Windows 服务的信息，请参阅 " **服务** " 对话框中的 "帮助" 文件 (在 " **管理工具** ") 下的 Windows "控制面板" 中查看。

 

 





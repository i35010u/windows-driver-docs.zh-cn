---
title: 用户模式下 WDM 音频组件
description: 用户模式下 WDM 音频组件
ms.assetid: 067944fb-6854-4ae8-81ca-9b8f2eed939e
keywords:
- 用户模式组件 WDK 音频
- WinMM 系统组件 WDK 音频
- WDMAud 系统驱动程序 WDK 音频
- DirectSound 系统组件 WDK 音频
- DirectMusic 系统组件 WDK 音频
- Windows 音频服务 WDK 音频
- waveOut API WDK 音频
- 音频服务 WDK
- WDMAud 系统驱动程序
- WDMAud 系统驱动程序，用户模式 (wdmaud.drv)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21bdb025f98a292fc81252fb4051d0bbb4492113
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532947"
---
# <a name="user-mode-wdm-audio-components"></a>用户模式下 WDM 音频组件


## <span id="user_mode_wdm_audio_components"></span><span id="USER_MODE_WDM_AUDIO_COMPONENTS"></span>


用户模式下的 Microsoft Windows 驱动程序模型 (WDM) 音频组件包括：

-   WinMM 系统组件

-   WDMAud 系统驱动程序

-   DirectSound 系统组件

-   DirectMusic 系统组件

-   Windows Audio Services

### <a name="span-idwinmmsystemcomponentspanspan-idwinmmsystemcomponentspanwinmm-system-component"></a><span id="winmm_system_component"></span><span id="WINMM_SYSTEM_COMPONENT"></span>WinMM 系统组件

WinMM 系统组件 （Winmm.dll 和对应的 16 位，Mmsystem.dll） 实现 Microsoft Windows 多媒体 Api wave*Xxx*，midi*Xxx*，mixer*Xxx*，和 aux*Xxx* （请参阅 Microsoft Windows SDK 文档）。 WinMM 组件使用 WDMAud 系统驱动程序转换到内核流式处理 I/O 请求的 WinMM API 调用。

### <a name="span-idwdmaudsystemdriverspanspan-idwdmaudsystemdriverspanwdmaud-system-driver"></a><span id="wdmaud_system_driver"></span><span id="WDMAUD_SYSTEM_DRIVER"></span>WDMAud 系统驱动程序

用户模式下 WDMAud 系统驱动程序 (Wdmaud.drv) 与内核模式 WDMAud 系统驱动程序 (Wdmaud.sys) 配对。 在一起，WDMAud 系统驱动程序 WinMM API 调用和内核流式处理 I/O 请求之间进行转换。 内核模式模式 WDMAud 驱动程序是 SysAudio 系统驱动程序的客户端。

### <a name="span-iddirectsoundsystemcomponentspanspan-iddirectsoundsystemcomponentspandirectsound-system-component"></a><span id="directsound_system_component"></span><span id="DIRECTSOUND_SYSTEM_COMPONENT"></span>DirectSound 系统组件

DirectSound 系统组件 (Dsound.dll) 支持 DirectSound API （请参阅 Microsoft Windows SDK 文档）。 DirectSound 组件是 SysAudio 驱动程序的客户端。 如果混合使用硬件不可用，SysAudio 驱动程序 DirectSound 硬件缓冲区直接连接到渲染设备。 否则，SysAudio 驱动程序连接 DirectSound 软件缓冲区到 KMixer 系统驱动程序。 有关详细信息，请参阅[呈现批内容使用 DirectSound 软件和硬件缓冲区](rendering-wave-content-using-directsound-software-and-hardware-buffers.md)。

### <a name="span-iddirectmusicsystemcomponentspanspan-iddirectmusicsystemcomponentspandirectmusic-system-component"></a><span id="directmusic_system_component"></span><span id="DIRECTMUSIC_SYSTEM_COMPONENT"></span>DirectMusic 系统组件

DirectMusic 系统组件 (DMusic.dll) 支持 DirectMusic API （请参阅 Microsoft Windows SDK 文档）。 此组件将转换到对 WDM 音频设备的 I/O 请求对 DirectMusic API 的调用。 DirectMusic 组件是 SysAudio 系统驱动程序的客户端。

### <a name="span-idwindowsaudioservicesspanspan-idwindowsaudioservicesspanwindows-audio-services"></a><span id="windows_audio_services"></span><span id="WINDOWS_AUDIO_SERVICES"></span>Windows Audio Services

在 Windows XP 及更高版本，Windows 音频服务组件 (Audiosrv.dll) 管理音频设备的基于 Windows 的程序。 停止 Windows 音频服务会阻止音频设备和效果能够正常运行。 如果禁用音频服务，任何其他服务 （包括 WDM 音频驱动程序） 显式依赖于它们将无法启动。 Home Edition、 Professional 和服务器版本的 Windows XP 及更高版本，在音频服务是默认配置为自动启动。 但是，在 Advanced Server、 数据中心和 Web 服务器版本的 Windows Server 2003 及更高版本中，音频服务默认情况下禁用。 音频服务禁用时，安装将音频设备不会启用它们--启用音频服务，以管理员身份显式将它们配置为执行此操作时，才自动运行。 有关启动和停止 Windows 服务的信息，请参阅中的帮助文件**Services**对话框中 (在 Windows 控制面板下中查找**管理工具**)。

 

 





---
title: 使用 DirectSound 软件和硬件缓冲区呈现 Wave 内容
description: 使用 DirectSound 软件和硬件缓冲区呈现 Wave 内容
keywords:
- DirectSound WDK 音频，内容呈现
- 显示音频内容呈现 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 71ede4f55fee0a728b0a68487c42594cbf955aae
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800727"
---
# <a name="rendering-wave-content-using-directsound-software-and-hardware-buffers"></a>使用 DirectSound 软件和硬件缓冲区呈现 Wave 内容


## <span id="ddk_rendering_wave_content_using_directsound_software_and_hardware_buf"></span><span id="DDK_RENDERING_WAVE_CONTENT_USING_DIRECTSOUND_SOFTWARE_AND_HARDWARE_BUF"></span>


下图显示了 DirectSound 软件和硬件缓冲区呈现的 Microsoft Windows 驱动模型 (WDM) 组件的配置。

![演示如何使用 directsound 软件和硬件缓冲区呈现波形内容的示意图](images/hwbuf.png)

有关 WDM 音频组件的说明，请参阅以下内容：

[DirectSound 系统组件](user-mode-wdm-audio-components.md#directsound_system_component)

[SysAudio 系统驱动程序](kernel-mode-wdm-audio-components.md#sysaudio_system_driver)

[KMixer 系统驱动程序](kernel-mode-wdm-audio-components.md#kmixer_system_driver)

[端口类适配器驱动程序和 PortCls 系统驱动程序](kernel-mode-wdm-audio-components.md#port_class_adapter_driver_and_portcls_system_driver)

[USBAudio 类系统驱动程序](kernel-mode-wdm-audio-components.md#usbaudio_class_system_driver)

 

 





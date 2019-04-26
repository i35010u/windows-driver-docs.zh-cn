---
title: 使用 DirectSound 软件和硬件缓冲区呈现 Wave 内容
description: 使用 DirectSound 软件和硬件缓冲区呈现 Wave 内容
ms.assetid: df92dac3-2580-4910-8a55-bd9e9f82eb1f
keywords:
- DirectSound WDK 音频，则内容呈现
- 批内容的渲染 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 082c62d647746a0fa4362046473ec40754e10c20
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328715"
---
# <a name="rendering-wave-content-using-directsound-software-and-hardware-buffers"></a>使用 DirectSound 软件和硬件缓冲区呈现 Wave 内容


## <span id="ddk_rendering_wave_content_using_directsound_software_and_hardware_buf"></span><span id="DDK_RENDERING_WAVE_CONTENT_USING_DIRECTSOUND_SOFTWARE_AND_HARDWARE_BUF"></span>


下图显示了将缓冲区呈现给 DirectSound 软件和硬件的 Microsoft Windows 驱动程序模型 (WDM) 组件的配置。

![演示如何使用 directsound 软件和硬件缓冲区的呈现批内容的关系图](images/hwbuf.png)

请参阅以下有关 WDM 音频组件的说明：

[DirectSound 系统组件](user-mode-wdm-audio-components.md#directsound_system_component)

[SysAudio System Driver](kernel-mode-wdm-audio-components.md#sysaudio_system_driver)

[KMixer 系统驱动程序](kernel-mode-wdm-audio-components.md#kmixer_system_driver)

[端口类适配器驱动程序和 PortCls 系统驱动程序](kernel-mode-wdm-audio-components.md#port_class_adapter_driver_and_portcls_system_driver)

[USBAudio 类系统驱动程序](kernel-mode-wdm-audio-components.md#usbaudio_class_system_driver)

 

 





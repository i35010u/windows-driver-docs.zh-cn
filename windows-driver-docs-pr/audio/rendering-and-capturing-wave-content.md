---
title: 呈现和捕获批内容
description: 呈现和捕获批内容
ms.assetid: 575499a9-e572-4ccc-bcee-8f2843310b05
keywords:
- 批呈现 WDK 音频
- 批捕获 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d4466631153a102d59b373eebc2cba6984a7c59
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522854"
---
# <a name="rendering-and-capturing-wave-content"></a>呈现和捕获批内容


## <span id="rendering_and_capturing_wave_content"></span><span id="RENDERING_AND_CAPTURING_WAVE_CONTENT"></span>


下图显示了 Microsoft Windows 驱动程序模型 (WDM) 的呈现和捕获批内容的音频组件的配置。

![说明呈现和捕获批内容的关系图](images/wave.png)

请参阅以下有关 WDM 音频组件的说明：

[DirectSound 系统组件](user-mode-wdm-audio-components.md#directsound_system_component)

[WDMAud 系统驱动程序](user-mode-wdm-audio-components.md#wdmaud_system_driver)

[SBEmul 系统驱动程序](kernel-mode-wdm-audio-components.md#sbemul_system_driver)

[SysAudio System Driver](kernel-mode-wdm-audio-components.md#sysaudio_system_driver)

[KMixer 系统驱动程序](kernel-mode-wdm-audio-components.md#kmixer_system_driver)

[Redbook 系统驱动程序](kernel-mode-wdm-audio-components.md#redbook_system_driver)

[拆分器系统驱动程序](kernel-mode-wdm-audio-components.md#splitter_system_driver)

[端口类适配器驱动程序和 PortCls 系统驱动程序](kernel-mode-wdm-audio-components.md#port_class_adapter_driver_and_portcls_system_driver)

[USBAudio 类系统驱动程序](kernel-mode-wdm-audio-components.md#usbaudio_class_system_driver)

请参阅以下有关配置的端口类适配器驱动程序和 USBAudio 驱动程序的详细信息：

[呈现，使用端口类音频适配器捕获音频内容](rendering-and-capturing-audio-content-by-using-a-port-class-audio-adap.md)

[呈现和捕获音频内容使用 USBAudio 驱动程序](rendering-and-capturing-audio-content-by-using-the-usbaudio-driver.md)

 

 





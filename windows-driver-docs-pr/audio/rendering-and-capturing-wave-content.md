---
title: 呈现和捕获 Wave 内容
description: 呈现和捕获 Wave 内容
keywords:
- 波形渲染 WDK 音频
- 波形捕获 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf9cd00075bd6f753cd3655e266e1a0665a679e7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800759"
---
# <a name="rendering-and-capturing-wave-content"></a>呈现和捕获 Wave 内容


## <span id="rendering_and_capturing_wave_content"></span><span id="RENDERING_AND_CAPTURING_WAVE_CONTENT"></span>


下图显示了 Microsoft Windows 驱动模型 (WDM) 音频组件的配置，这些组件可呈现和捕获波内容。

![演示如何呈现和捕获波形内容的关系图](images/wave.png)

有关 WDM 音频组件的说明，请参阅以下内容：

[DirectSound 系统组件](user-mode-wdm-audio-components.md#directsound_system_component)

[WDMAud 系统驱动程序](user-mode-wdm-audio-components.md#wdmaud_system_driver)

[SBEmul 系统驱动程序](kernel-mode-wdm-audio-components.md#sbemul_system_driver)

[SysAudio 系统驱动程序](kernel-mode-wdm-audio-components.md#sysaudio_system_driver)

[KMixer 系统驱动程序](kernel-mode-wdm-audio-components.md#kmixer_system_driver)

[Redbook 系统驱动程序](kernel-mode-wdm-audio-components.md#redbook_system_driver)

[拆分系统驱动程序](kernel-mode-wdm-audio-components.md#splitter_system_driver)

[端口类适配器驱动程序和 PortCls 系统驱动程序](kernel-mode-wdm-audio-components.md#port_class_adapter_driver_and_portcls_system_driver)

[USBAudio 类系统驱动程序](kernel-mode-wdm-audio-components.md#usbaudio_class_system_driver)

有关端口类适配器驱动程序和 USBAudio 驱动程序的配置的详细信息，请参阅以下内容：

[使用端口类音频适配器呈现和捕获音频内容](rendering-and-capturing-audio-content-by-using-a-port-class-audio-adap.md)

[使用 USBAudio 驱动程序呈现和捕获音频内容](rendering-and-capturing-audio-content-by-using-the-usbaudio-driver.md)

 

 





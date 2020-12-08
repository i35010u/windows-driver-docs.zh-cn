---
title: 呈现和捕获 MIDI 内容
description: 呈现和捕获 MIDI 内容
keywords:
- MIDI 内容呈现 WDK 音频
- MIDI 内容捕获 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6aff9b070738fca47271f32a8712abc8ab40edc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800725"
---
# <a name="rendering-and-capturing-midi-content"></a>呈现和捕获 MIDI 内容


## <span id="rendering_and_capturing_midi_content"></span><span id="RENDERING_AND_CAPTURING_MIDI_CONTENT"></span>


下图显示了系统提供的 Microsoft Windows 驱动模型 (WDM) 音频组件之间的关系，这些组件支持呈现和捕获 MIDI 内容。

![演示如何呈现和捕获 midi 内容的示意图](images/midi.png)

请参阅以下内容，了解 Microsoft Windows 驱动模型 (WDM) 音频组件：

[DirectMusic 系统组件](user-mode-wdm-audio-components.md#directmusic_system_component)

[WDMAud 系统驱动程序](user-mode-wdm-audio-components.md#wdmaud_system_driver)

[SBEmul 系统驱动程序](kernel-mode-wdm-audio-components.md#sbemul_system_driver)

[SysAudio 系统驱动程序](kernel-mode-wdm-audio-components.md#sysaudio_system_driver)

[KMixer 系统驱动程序](kernel-mode-wdm-audio-components.md#kmixer_system_driver)

[SWMidi 系统驱动程序](kernel-mode-wdm-audio-components.md#swmidi_system_driver)

[DMusic 系统驱动程序](kernel-mode-wdm-audio-components.md#dmusic_system_driver)

[端口类适配器驱动程序和 PortCls 系统驱动程序](kernel-mode-wdm-audio-components.md#port_class_adapter_driver_and_portcls_system_driver)

[USBAudio 类系统驱动程序](kernel-mode-wdm-audio-components.md#usbaudio_class_system_driver)

有关端口类适配器驱动程序和 USBAudio 驱动程序的配置的详细信息，请参阅以下内容：

[使用端口类音频适配器呈现和捕获音频内容](rendering-and-capturing-audio-content-by-using-a-port-class-audio-adap.md)

[使用 USBAudio 驱动程序呈现和捕获音频内容](rendering-and-capturing-audio-content-by-using-the-usbaudio-driver.md)

 

 





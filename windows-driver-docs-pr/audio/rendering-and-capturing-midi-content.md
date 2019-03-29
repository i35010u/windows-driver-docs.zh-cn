---
title: 呈现和捕获 MIDI 内容
description: 呈现和捕获 MIDI 内容
ms.assetid: 32eff06a-f3e8-471c-8fe6-b7cee208b90c
keywords:
- MIDI 内容呈现 WDK 音频
- MIDI 内容捕获 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5dcdd1f0270492e47e0e9d583387bd797133f0ee
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568675"
---
# <a name="rendering-and-capturing-midi-content"></a>呈现和捕获 MIDI 内容


## <span id="rendering_and_capturing_midi_content"></span><span id="RENDERING_AND_CAPTURING_MIDI_CONTENT"></span>


下图显示组件之间的关系系统提供 Microsoft Windows 驱动程序模型 (WDM) 音频支持呈现和捕获 MIDI 的内容。

![说明呈现和捕获 midi 内容的关系图](images/midi.png)

查看有关 Microsoft Windows 驱动程序模型 (WDM) 音频组件的说明以下信息：

[DirectMusic 系统组件](user-mode-wdm-audio-components.md#directmusic_system_component)

[WDMAud 系统驱动程序](user-mode-wdm-audio-components.md#wdmaud_system_driver)

[SBEmul 系统驱动程序](kernel-mode-wdm-audio-components.md#sbemul_system_driver)

[SysAudio System Driver](kernel-mode-wdm-audio-components.md#sysaudio_system_driver)

[KMixer 系统驱动程序](kernel-mode-wdm-audio-components.md#kmixer_system_driver)

[SWMidi 系统驱动程序](kernel-mode-wdm-audio-components.md#swmidi_system_driver)

[DMusic 系统驱动程序](kernel-mode-wdm-audio-components.md#dmusic_system_driver)

[端口类适配器驱动程序和 PortCls 系统驱动程序](kernel-mode-wdm-audio-components.md#port_class_adapter_driver_and_portcls_system_driver)

[USBAudio 类系统驱动程序](kernel-mode-wdm-audio-components.md#usbaudio_class_system_driver)

请参阅以下有关配置的端口类适配器驱动程序和 USBAudio 驱动程序的详细信息：

[呈现，使用端口类音频适配器捕获音频内容](rendering-and-capturing-audio-content-by-using-a-port-class-audio-adap.md)

[呈现和捕获音频内容使用 USBAudio 驱动程序](rendering-and-capturing-audio-content-by-using-the-usbaudio-driver.md)

 

 





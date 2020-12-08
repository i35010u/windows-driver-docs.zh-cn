---
title: 使用 USBAudio 驱动程序呈现和捕获音频内容
description: 使用 USBAudio 驱动程序呈现和捕获音频内容
keywords:
- USBAudio 类系统驱动程序 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1fbfb2088b5ad84ca977675850c9e7cb88842ad
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800731"
---
# <a name="rendering-and-capturing-audio-content-by-using-the-usbaudio-driver"></a>使用 USBAudio 驱动程序呈现和捕获音频内容


## <span id="ddk_rendering_and_capturing_audio_content_by_using_the_usbaudio_driver"></span><span id="DDK_RENDERING_AND_CAPTURING_AUDIO_CONTENT_BY_USING_THE_USBAUDIO_DRIVER"></span>


下图显示了如何配置 [USBAudio 类系统驱动程序](kernel-mode-wdm-audio-components.md#usbaudio_class_system_driver) 以呈现和捕获音频内容。 在此图中，USBAudio 驱动程序 sprouts 针脚来表示 USB 音频设备上的终端。 音频组件（如 KMixer、WDMAud 和 DirectSound）连接到这些 pin 以呈现输出流或捕获输入流。

![演示如何使用 usbaudio 驱动程序呈现和捕获音频内容的示意图](images/usbaud.png)

请参阅以下内容，了解 Microsoft Windows 驱动模型 (WDM) 音频组件：

[DirectSound 系统组件](user-mode-wdm-audio-components.md#directsound_system_component)

[WDMAud 系统驱动程序](user-mode-wdm-audio-components.md#wdmaud_system_driver)

[SBEmul 系统驱动程序](kernel-mode-wdm-audio-components.md#sbemul_system_driver)

[KMixer 系统驱动程序](kernel-mode-wdm-audio-components.md#kmixer_system_driver)

[Redbook 系统驱动程序](kernel-mode-wdm-audio-components.md#redbook_system_driver)

[拆分系统驱动程序](kernel-mode-wdm-audio-components.md#splitter_system_driver)

[SWMidi 系统驱动程序](kernel-mode-wdm-audio-components.md#swmidi_system_driver)

[DMusic 系统驱动程序](kernel-mode-wdm-audio-components.md#dmusic_system_driver)

有关 USBAudio 驱动程序上方筛选器图形的详细信息，请参阅以下内容：

[呈现和捕获 Wave 内容](rendering-and-capturing-wave-content.md)

[呈现和捕获 MIDI 内容](rendering-and-capturing-midi-content.md)

 

 





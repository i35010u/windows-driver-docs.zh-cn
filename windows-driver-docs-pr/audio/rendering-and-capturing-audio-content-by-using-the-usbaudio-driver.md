---
title: 使用 USBAudio 驱动程序呈现和捕获音频内容
description: 使用 USBAudio 驱动程序呈现和捕获音频内容
ms.assetid: 92a6ad18-75ba-4382-a6d1-42f28133a158
keywords:
- USBAudio 类系统驱动程序 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41fbe4fc3a3688d89af2f3898732d45728d21908
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328739"
---
# <a name="rendering-and-capturing-audio-content-by-using-the-usbaudio-driver"></a>使用 USBAudio 驱动程序呈现和捕获音频内容


## <span id="ddk_rendering_and_capturing_audio_content_by_using_the_usbaudio_driver"></span><span id="DDK_RENDERING_AND_CAPTURING_AUDIO_CONTENT_BY_USING_THE_USBAUDIO_DRIVER"></span>


下图显示了如何[USBAudio 类系统驱动程序](kernel-mode-wdm-audio-components.md#usbaudio_class_system_driver)配置来呈现和捕获音频内容。 在此图中，USBAudio 驱动程序 sprouts 插针，以表示 USB 音频设备上的终端。 如 KMixer、 WDMAud 和 DirectSound 音频组件连接到这些插针，以呈现输出流或捕获输入的流。

![说明呈现和捕获音频内容使用 usbaudio 驱动程序的关系图](images/usbaud.png)

查看有关 Microsoft Windows 驱动程序模型 (WDM) 音频组件的说明以下信息：

[DirectSound 系统组件](user-mode-wdm-audio-components.md#directsound_system_component)

[WDMAud 系统驱动程序](user-mode-wdm-audio-components.md#wdmaud_system_driver)

[SBEmul 系统驱动程序](kernel-mode-wdm-audio-components.md#sbemul_system_driver)

[KMixer 系统驱动程序](kernel-mode-wdm-audio-components.md#kmixer_system_driver)

[Redbook 系统驱动程序](kernel-mode-wdm-audio-components.md#redbook_system_driver)

[拆分器系统驱动程序](kernel-mode-wdm-audio-components.md#splitter_system_driver)

[SWMidi 系统驱动程序](kernel-mode-wdm-audio-components.md#swmidi_system_driver)

[DMusic 系统驱动程序](kernel-mode-wdm-audio-components.md#dmusic_system_driver)

请参阅以下有关位于上方 USBAudio 驱动程序筛选器关系图的详细信息：

[呈现和捕获批内容](rendering-and-capturing-wave-content.md)

[呈现和捕获 MIDI 内容](rendering-and-capturing-midi-content.md)

 

 





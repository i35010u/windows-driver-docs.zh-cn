---
title: 针对旧音频接口的驱动程序支持
description: 针对旧音频接口的驱动程序支持
ms.assetid: c1b81c58-de05-45e7-94ab-5d174d51dfd6
keywords:
- WDM 音频驱动程序 WDK，旧接口
- 音频驱动程序 WDK，旧接口
- 旧的音频接口 WDK 音频
- 接口 WDK 音频
- 音频的微型端口驱动程序 WDK，旧接口
- 微型端口驱动程序 WDK 音频的旧接口
- Windows 多媒体支持 WDK 音频
- 多媒体 WDK 音频
- 微型端口接口 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19855d6fcb8bbfd7f99248e87689f87639fce4dd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333734"
---
# <a name="driver-support-for-legacy-audio-interfaces"></a>针对旧音频接口的驱动程序支持


## <span id="driver_support_for_legacy_audio_interfaces"></span><span id="DRIVER_SUPPORT_FOR_LEGACY_AUDIO_INTERFACES"></span>


WDM 音频系统提供的旧版 Windows 多媒体功能通过访问音频设备的应用程序的驱动程序支持。 这些函数包括以下特定于音频的 Api:

-   aux

-   Mixer

-   midiIn

-   midiOut

-   waveIn

-   waveOut

有关这些 Api 的信息，请参阅 Microsoft Windows SDK 文档。 提供对旧版音频功能驱动程序支持的系统组件的说明，请参阅[WDM 音频组件](wdm-audio-components.md)。

本部分讨论音频微型端口驱动程序可以实现更好地支持 Windows 多媒体函数向应用程序公开的音频功能的功能。 这些功能包括批流捕获和呈现、 MIDI 录制和合成，以及混音器控件。 此外，本部分介绍一些传统应用程序可用于检索有关音频设备驱动程序特定信息的特定于音频的 Api 扩展。

本部分讨论以下主题：

[流式处理音频 Mixer API 转换到拓扑的内核](kernel-streaming-topology-to-audio-mixer-api-translation.md)

[WDM 音频扩展到旧版 Windows 多媒体 Api](wdm-audio-extensions-to-legacy-windows-multimedia-apis.md)

 

 





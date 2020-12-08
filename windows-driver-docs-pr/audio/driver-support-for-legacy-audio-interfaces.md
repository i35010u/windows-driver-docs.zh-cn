---
title: 针对旧音频接口的驱动程序支持
description: 针对旧音频接口的驱动程序支持
keywords:
- WDM 音频驱动程序 WDK，旧接口
- 音频驱动程序 WDK，旧接口
- 传统音频接口 WDK 音频
- 接口 WDK 音频
- 音频微型端口驱动程序 WDK，旧接口
- 微型端口驱动程序 WDK 音频，旧版接口
- Windows 多媒体支持 WDK 音频
- 多媒体 WDK 音频
- 微型端口接口 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1cf73fe59a20d91593dc331078c27c9cd7dc8b2f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786565"
---
# <a name="driver-support-for-legacy-audio-interfaces"></a>针对旧音频接口的驱动程序支持


## <span id="driver_support_for_legacy_audio_interfaces"></span><span id="DRIVER_SUPPORT_FOR_LEGACY_AUDIO_INTERFACES"></span>


WDM 音频系统通过旧的 Windows 多媒体功能为访问音频设备的应用程序提供驱动程序支持。 这些函数包括下列特定于音频的 Api：

-   助

-   混音

-   midiIn

-   midiOut

-   waveIn

-   waveOut

有关这些 Api 的信息，请参阅 Microsoft Windows SDK 文档。 有关为旧版音频功能提供驱动程序支持的系统组件的说明，请参阅 [WDM 音频组件](wdm-audio-components.md)。

本部分讨论音频微型端口驱动程序可以实现的功能，以便更好地支持 Windows 多媒体功能向应用程序公开的音频功能。 这些功能包括波形流捕获和渲染、MIDI 录音和合成以及混音器控制。 此外，本部分还介绍了应用程序可用于检索有关音频设备的特定于驱动程序的信息的旧版特定于音频的 Api 的多个扩展。

本部分介绍以下主题：

[从内核流式处理拓扑到音频混音器 API 的转换](kernel-streaming-topology-to-audio-mixer-api-translation.md)

[针对旧版 Windows 多媒体 API 的 WDM 音频扩展](wdm-audio-extensions-to-legacy-windows-multimedia-apis.md)

 

 





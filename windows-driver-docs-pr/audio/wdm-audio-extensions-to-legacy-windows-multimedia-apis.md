---
title: 针对旧版 Windows 多媒体 API 的 WDM 音频扩展
description: 针对旧版 Windows 多媒体 API 的 WDM 音频扩展
ms.assetid: a1009b7f-3720-454f-a128-ae148f781edc
keywords:
- WDM 音频扩展 WDK
- 扩展音频功能 WDK 音频
- WDM 音频驱动程序 WDK，扩展
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d4a762c5cd338c025ce92a4d39b96880f2eca57
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206651"
---
# <a name="wdm-audio-extensions-to-legacy-windows-multimedia-apis"></a>针对旧版 Windows 多媒体 API 的 WDM 音频扩展


## <span id="wdm_audio_extensions_to_legacy_windows_multimedia_apis"></span><span id="WDM_AUDIO_EXTENSIONS_TO_LEGACY_WINDOWS_MULTIMEDIA_APIS"></span>


最新版本的 Windows 已将 Windows 多媒体 Api aux、midiIn、midiOut、混音器、waveIn 和 waveOut 中的音频功能进行了扩展，以输出有关 WDM 音频驱动程序的状态和功能的信息。

[**AuxGetDevCaps**](/previous-versions/dd756712(v=vs.85))、 [**midiInGetDevCaps**](/previous-versions/dd798453(v=vs.85))、 [**midiOutGetDevCaps**](/previous-versions/dd798469(v=vs.85))、 [**mixerGetDevCaps**](/previous-versions/dd757300(v=vs.85))、 [**waveInGetDevCaps**](/previous-versions/dd743841(v=vs.85))和[**waveOutGetDevCaps**](/previous-versions/dd743857(v=vs.85))函数可以检索唯一标识音频设备的特定于驱动程序的信息。

Windows 多媒体函数 [**waveInMessage**](/previous-versions/dd743846(v=vs.85))、 [**waveOutMessage**](/previous-versions/dd743865(v=vs.85))、 [**midiInMessage**](/previous-versions/dd798457(v=vs.85))、 [**MIDIOUTMESSAGE**](/previous-versions/dd798475(v=vs.85))和 [**mixerMessage**](/previous-versions/dd757307(v=vs.85)) 可以检索波形、MIDI 或混音设备的设备接口名称。 此外， **waveOutMessage**、 **midiOutMessage**和 **waveInMessage** 函数可分别检索首选音频设备的设备 id，以进行波形 i/o、MIDI 和语音通信。

以下是本节中要讨论的主题：

[从 WDM 音频驱动程序扩展的功能](extended-capabilities-from-a-wdm-audio-driver.md)

[系统截获的设备消息](system-intercepted-device-messages.md)

[访问首选的设备 ID](accessing-the-preferred-device-id.md)

[首选的语音通信设备 ID](preferred-voice-communications-device-id.md)

[获取设备接口名称](obtaining-a-device-interface-name.md)

[音乐技术 GUID](music-technology-guids.md)

 


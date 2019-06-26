---
title: 针对旧版 Windows 多媒体 API 的 WDM 音频扩展
description: 针对旧版 Windows 多媒体 API 的 WDM 音频扩展
ms.assetid: a1009b7f-3720-454f-a128-ae148f781edc
keywords:
- WDM 音频扩展 WDK
- 扩展的音频功能 WDK 音频
- WDM 音频驱动程序 WDK，扩展
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 186c5cb6efd3921128dee681bb94520e69fa3606
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354104"
---
# <a name="wdm-audio-extensions-to-legacy-windows-multimedia-apis"></a>针对旧版 Windows 多媒体 API 的 WDM 音频扩展


## <span id="wdm_audio_extensions_to_legacy_windows_multimedia_apis"></span><span id="WDM_AUDIO_EXTENSIONS_TO_LEGACY_WINDOWS_MULTIMEDIA_APIS"></span>


最新版本的 Windows 扩展音频和中的功能 Windows 多媒体 Api aux、 midiIn、 midiOut、 mixer、 waveIn，waveOut 要输出的状态和 WDM 音频驱动程序的功能有关的信息。

[ **AuxGetDevCaps**](https://docs.microsoft.com/previous-versions/dd756712(v=vs.85))， [ **midiInGetDevCaps**](https://docs.microsoft.com/previous-versions/dd798453(v=vs.85))， [ **midiOutGetDevCaps**](https://docs.microsoft.com/previous-versions/dd798469(v=vs.85))， [ **mixerGetDevCaps**](https://docs.microsoft.com/previous-versions/dd757300(v=vs.85))， [ **waveInGetDevCaps**](https://docs.microsoft.com/previous-versions/dd743841(v=vs.85))，并[ **waveOutGetDevCaps** ](https://docs.microsoft.com/previous-versions/dd743857(v=vs.85))函数可以检索的唯一标识音频设备驱动程序特定的信息。

Windows 多媒体函数[ **waveInMessage**](https://docs.microsoft.com/previous-versions/dd743846(v=vs.85))， [ **waveOutMessage**](https://docs.microsoft.com/previous-versions/dd743865(v=vs.85))， [ **midiInMessage**](https://docs.microsoft.com/previous-versions/dd798457(v=vs.85))， [ **midiOutMessage**](https://docs.microsoft.com/previous-versions/dd798475(v=vs.85))，以及[ **mixerMessage** ](https://docs.microsoft.com/previous-versions/dd757307(v=vs.85))可以检索批、 MIDI 或混音器设备的设备接口名称。 此外， **waveOutMessage**， **midiOutMessage**，并**waveInMessage**函数可以检索设备的批 I/O，MIDI，首选音频设备 Id 和分别语音通信。

本部分讨论了以下主题：

[从 WDM 音频驱动程序的扩展的功能](extended-capabilities-from-a-wdm-audio-driver.md)

[系统截获设备的消息](system-intercepted-device-messages.md)

[访问首选的设备 ID](accessing-the-preferred-device-id.md)

[首选的语音通信设备 ID](preferred-voice-communications-device-id.md)

[获取设备接口名称](obtaining-a-device-interface-name.md)

[音乐技术 Guid](music-technology-guids.md)

 

 





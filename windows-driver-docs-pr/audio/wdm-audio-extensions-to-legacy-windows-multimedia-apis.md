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
ms.openlocfilehash: 14860d7795db633e22ce113c4ad67738e86c7cb3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328471"
---
# <a name="wdm-audio-extensions-to-legacy-windows-multimedia-apis"></a>针对旧版 Windows 多媒体 API 的 WDM 音频扩展


## <span id="wdm_audio_extensions_to_legacy_windows_multimedia_apis"></span><span id="WDM_AUDIO_EXTENSIONS_TO_LEGACY_WINDOWS_MULTIMEDIA_APIS"></span>


最新版本的 Windows 扩展音频和中的功能 Windows 多媒体 Api aux、 midiIn、 midiOut、 mixer、 waveIn，waveOut 要输出的状态和 WDM 音频驱动程序的功能有关的信息。

[ **AuxGetDevCaps**](https://msdn.microsoft.com/library/windows/desktop/dd756712)， [ **midiInGetDevCaps**](https://msdn.microsoft.com/library/windows/desktop/dd798453)， [ **midiOutGetDevCaps**](https://msdn.microsoft.com/library/windows/desktop/dd798469)， [ **mixerGetDevCaps**](https://msdn.microsoft.com/library/windows/desktop/dd757300)， [ **waveInGetDevCaps**](https://msdn.microsoft.com/library/windows/desktop/dd743841)，并[ **waveOutGetDevCaps** ](https://msdn.microsoft.com/library/windows/desktop/dd743857)函数可以检索的唯一标识音频设备驱动程序特定的信息。

Windows 多媒体函数[ **waveInMessage**](https://msdn.microsoft.com/library/windows/desktop/dd743846)， [ **waveOutMessage**](https://msdn.microsoft.com/library/windows/desktop/dd743865)， [ **midiInMessage**](https://msdn.microsoft.com/library/windows/desktop/dd798457)， [ **midiOutMessage**](https://msdn.microsoft.com/library/windows/desktop/dd798475)，以及[ **mixerMessage** ](https://msdn.microsoft.com/library/windows/desktop/dd757307)可以检索批、 MIDI 或混音器设备的设备接口名称。 此外， **waveOutMessage**， **midiOutMessage**，并**waveInMessage**函数可以检索设备的批 I/O，MIDI，首选音频设备 Id 和分别语音通信。

本部分讨论了以下主题：

[从 WDM 音频驱动程序的扩展的功能](extended-capabilities-from-a-wdm-audio-driver.md)

[系统截获设备的消息](system-intercepted-device-messages.md)

[访问首选的设备 ID](accessing-the-preferred-device-id.md)

[首选的语音通信设备 ID](preferred-voice-communications-device-id.md)

[获取设备接口名称](obtaining-a-device-interface-name.md)

[音乐技术 Guid](music-technology-guids.md)

 

 





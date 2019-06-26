---
title: 音频数据格式
description: 音频数据格式
ms.assetid: e16c10ea-0193-4cf4-91a3-4f8d4a0d5cf6
keywords:
- 数据格式 WDK 音频
- WDK 音频数据的格式
- WDK 的音频数据格式
- 批流 WDK 音频
- 数字格式 WDK 音频
- WDK 音频进行流式处理格式
- KS 数据格式 WDK 音频
- KSDATAFORMAT 结构
- WDM 音频数据格式 WDK
- 格式 WDK 音频
- 数据格式以 WDK 音频，有关音频数据格式
ms.date: 02/15/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f6d9fff6d993d9fba7a671ec41f014d9d6391b5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355735"
---
# <a name="audio-data-formats"></a>音频数据格式


## <span id="audio_data_formats"></span><span id="AUDIO_DATA_FORMATS"></span>


若要指定 wave 音频流的数据格式[ **KSDATAFORMAT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksdataformat)结构通过以下任一方法后立即[ **WAVEFORMATEX** ](https://docs.microsoft.com/windows/desktop/api/mmreg/ns-mmreg-twaveformatex)或[ **KSDSOUND\_BUFFERDESC** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksdsound_bufferdesc)结构，并且**说明符**KSDATAFORMAT 成员相应地设置为以下值之一两个值：

-   KSDATAFORMAT\_SPECIFIER\_WAVEFORMATEX

    指示数据格式属于 waveIn 或 waveOut 应用程序正在使用的波次流。 在这种情况下，如果 KSDATAFORMAT 结构*FormatSize*是不够大，数据格式说明符遵循 KSDATAFORMAT 结构是一种 WAVEFORMATEX 结构。

-   KSDATAFORMAT\_SPECIFIER\_DSOUND

    指示数据格式属于 DirectSound 应用程序正在使用的波次流。 在这种情况下，数据格式说明符遵循 KSDATAFORMAT 结构是 KSDSOUND\_BUFFERDESC 结构，其中包含嵌入的 WAVEFORMATEX 结构。

[ **KSDATAFORMAT\_WAVEFORMATEX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksdataformat_waveformatex)结构封装 KSDATAFORMAT 结构和其后的 WAVEFORMATEX 结构。 同样， [ **KSDATAFORMAT\_DSOUND** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksdataformat_dsound)结构封装 KSDATAFORMAT 结构和 DSOUND\_BUFFERDESC 结构，它可以跟踪该域控制器。

对于任一 KSDATAFORMAT\_WAVEFORMATEX 或 KSDATAFORMAT\_DSOUND，结构中的最后一项是嵌入的 WAVEFORMATEX 结构; 对于 KSDATAFORMAT\_DSOUND，WAVEFORMATEX 结构中包含嵌入 DSOUND\_BUFFERDESC 结构。 在任一情况下，WAVEFORMATEX 结构可能的开头[ **WAVEFORMATEXTENSIBLE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-waveformatextensible)结构，在这种情况下**wFormatTag**设置 WAVEFORMATEX 的成员为值 WAVE\_格式\_可扩展。 有关详细信息，请参阅[可扩展波形格式描述符](extensible-wave-format-descriptors.md)。

若要指定 MIDI 流或 DirectMusic 流的数据格式，KSDATAFORMAT 结构是不够的;它不被跟任何其他信息。

有关批和 DirectSound 数据格式的示例，请参阅[PCM Stream 数据格式](pcm-stream-data-format.md)并[DirectSound Stream 数据格式](directsound-stream-data-format.md)。 有关 MIDI 和 DirectMusic 数据格式的示例，请参阅[MIDI Stream 数据格式](midi-stream-data-format.md)并[DirectMusic Stream 数据格式](directmusic-stream-data-format.md)。

 

 





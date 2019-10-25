---
title: 音频数据格式
description: 音频数据格式
ms.assetid: e16c10ea-0193-4cf4-91a3-4f8d4a0d5cf6
keywords:
- 数据格式化 WDK 音频
- 格式化 WDK 音频、数据
- 音频数据格式 WDK
- 波形流 WDK 音频
- 数字格式 WDK 音频
- 流格式化 WDK 音频
- KS 数据格式 WDK 音频
- KSDATAFORMAT 结构
- WDM 音频数据格式 WDK
- 格式化 WDK 音频
- 数据格式化 WDK 音频，关于音频数据格式
ms.date: 02/15/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff9d0612bcd7149b8c0159ce25d3c547107bd452
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831910"
---
# <a name="audio-data-formats"></a>音频数据格式


## <span id="audio_data_formats"></span><span id="AUDIO_DATA_FORMATS"></span>


若要指定波形音频流的数据格式， [**KSDATAFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)结构会立即后跟[**WAVEFORMATEX**](https://docs.microsoft.com/windows/desktop/api/mmreg/ns-mmreg-twaveformatex)或[**KSDSOUND\_BUFFERDESC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdsound_bufferdesc)结构，KSDATAFORMAT 的**说明符**成员是相应地设置为以下两个值之一：

-   KSDATAFORMAT\_WAVEFORMATEX\_说明符

    指示数据格式属于 waveIn 或 waveOut 应用程序正在使用的波形流。 在这种情况下，如果 KSDATAFORMAT 结构的*FormatSize*足够大，则 KSDATAFORMAT 结构后的数据格式说明符是 WAVEFORMATEX 结构。

-   KSDATAFORMAT\_DSOUND\_说明符

    指示数据格式属于 DirectSound 应用程序正在使用的波形流。 在这种情况下，KSDATAFORMAT 结构后面的数据格式说明符是一个 KSDSOUND\_BUFFERDESC 结构，其中包含一个嵌入的 WAVEFORMATEX 结构。

[**KSDATAFORMAT\_WAVEFORMATEX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdataformat_waveformatex)结构封装 KSDATAFORMAT 结构和它后面的 WAVEFORMATEX 结构。 同样， [**KSDATAFORMAT\_DSOUND**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdataformat_dsound)结构封装 KSDATAFORMAT 结构和它后面的 DSOUND\_BUFFERDESC 结构。

对于 KSDATAFORMAT\_WAVEFORMATEX 或 KSDATAFORMAT\_DSOUND，结构中的最后一项是嵌入的 WAVEFORMATEX 结构;对于 KSDATAFORMAT\_DSOUND，WAVEFORMATEX 结构包含在嵌入的 DSOUND\_BUFFERDESC 结构中。 在这两种情况下，WAVEFORMATEX 结构可能是[**WAVEFORMATEXTENSIBLE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-waveformatextensible)结构的开头，在这种情况下，WAVEFORMATEX 的**wFormatTag**成员设置为\_可扩展的\_格式。 有关详细信息，请参阅[可扩展波形格式说明符](extensible-wave-format-descriptors.md)。

若要为 MIDI 流或 DirectMusic 流指定数据格式，KSDATAFORMAT 结构就足够了;它后面没有任何其他信息。

有关 wave 和 DirectSound 数据格式的示例，请参阅[PCM Stream Data format](pcm-stream-data-format.md)和[DirectSound stream data format](directsound-stream-data-format.md)。 有关 MIDI 和 DirectMusic 数据格式的示例，请参阅[Midi 流数据格式](midi-stream-data-format.md)和[DirectMusic 流数据格式](directmusic-stream-data-format.md)。

 

 





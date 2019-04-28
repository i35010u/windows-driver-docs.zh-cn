---
title: 音频数据范围
description: 音频数据范围
ms.assetid: 690fafda-fb35-43da-9de1-6cbc3bf8eb6c
keywords:
- 数据范围 WDK 音频
- 范围值 WDK 音频
- KS 数据范围 WDK 音频
- 音频数据范围 WDK
- KSDATARANGE 结构
- WDM 音频数据范围 WDK
- 数据范围 WDK 音频，有关音频数据范围
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0cf3a6224dc23d6251a7e9aa67cc817e0cff7432
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331555"
---
# <a name="audio-data-ranges"></a>音频数据范围


## <span id="audio_data_ranges"></span><span id="AUDIO_DATA_RANGES"></span>


每个 pin KS 筛选器上的声明的数据进行格式设置支持。 Pin 工厂公开此数组形式的数据范围的信息。 与前面所述的格式说明符，不同数据范围描述一系列数据格式。 例如，批 pin 的数据范围指定样本大小、 频率和 pin 支持的通道的范围。

微型端口驱动程序实例化 pin，它将配置 pin 来处理它从 pin 的数据区域中选择的特定数据格式的流。 这项工作是通过微型端口驱动程序的数据交叉处理程序，它选择音频数据格式，以便可以将它们连接起来共有两个 pin。 有关详细信息，请参阅[交集数据处理程序](data-intersection-handlers.md)。

有关使用属性请求来查询其数据范围和选择数据交集的音频 pin 信息，请参阅[Pin 数据范围和交集属性](pin-data-range-and-intersection-properties.md)。

若要指定批 pin，数据范围[ **KSDATARANGE** ](https://msdn.microsoft.com/library/windows/hardware/ff561658)结构后跟描述的一系列示例大小、 频率和 pin 支持的通道的信息。 此信息，包括 KSDATARANGE 结构本身，封装在[ **KSDATARANGE\_音频**](https://msdn.microsoft.com/library/windows/hardware/ff537096)结构。

若要指定 MIDI 或 DirectMusic pin 的数据范围，KSDATARANGE 结构后跟其他信息，包括通道和可以在同一时间播放的说明的最大数目。 此信息，以及 KSDATARANGE 结构本身，封装在[ **KSDATARANGE\_音乐**](https://msdn.microsoft.com/library/windows/hardware/ff537097)结构。

本文档提供了几个示例的数据范围的使用 KSDATARANGE\_音频和 KSDATARANGE\_音乐结构：

-   有关示例声明的批和 DirectSound 数据范围，请参阅[PCM Stream 数据范围](pcm-stream-data-range.md)并[DirectSound Stream 数据范围](directsound-stream-data-range.md)。

-   有关示例声明的 MIDI 和 DirectMusic 数据范围，请参阅[MIDI Stream 数据范围](midi-stream-data-range.md)并[DirectMusic Stream 数据范围](directmusic-stream-data-range.md)。

-   有关示例声明的数据范围，对于非 PCM 格式，请参阅[指定 ac-3 数据范围](specifying-ac-3-data-ranges.md)并[并且指定 WMA Pro 数据范围](specifying-wma-pro-data-ranges.md)。

 

 





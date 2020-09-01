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
- 数据范围 WDK 音频，关于音频数据范围
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f15c48d688ac9422f34e7a169ccdfd388c2f0a9c
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208357"
---
# <a name="audio-data-ranges"></a>音频数据范围


## <span id="audio_data_ranges"></span><span id="AUDIO_DATA_RANGES"></span>


KS 筛选器上的每个 pin 都声明它支持的数据格式。 Pin 工厂将此信息作为数据范围的数组公开。 不同于前面所述的格式说明符，数据范围介绍了一系列数据格式。 例如，波形 pin 的数据范围指定 pin 支持的样本大小、频率和通道的范围。

当微型端口驱动程序实例化 pin 时，它会将 pin 配置为使用它从 pin 的数据范围选择的特定数据格式处理流。 此工作是通过微型端口驱动程序的数据交集处理程序来完成的，该处理程序选择两个 pin 共用的音频数据格式，以便可以进行连接。 有关详细信息，请参阅 [数据交集处理程序](data-intersection-handlers.md)。

有关使用属性请求来查询音频 pin 的数据范围并选择数据交集的信息，请参阅 [固定数据范围和交集属性](pin-data-range-and-intersection-properties.md)。

为了指定波形 pin 的数据范围， [**KSDATARANGE**](/previous-versions/ff561658(v=vs.85)) 结构后跟信息，该信息描述了 pin 支持的样本大小、频率和通道的范围。 此信息（包括 KSDATARANGE 结构本身）封装在 [**KSDATARANGE \_ 音频**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdatarange_audio) 结构中。

若要为 MIDI 或 DirectMusic pin 指定数据范围，KSDATARANGE 结构后跟附加信息，包括可同时播放的通道和最大数目。 此信息与 KSDATARANGE 结构本身一起封装在 [**KSDATARANGE \_ 音乐**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdatarange_music) 结构中。

本文档提供了几个使用 KSDATARANGE \_ 音频和 KSDATARANGE 音乐结构的数据范围示例 \_ ：

-   有关 wave 和 DirectSound 数据范围的示例声明，请参阅 [PCM 流数据范围](pcm-stream-data-range.md) 和 [DirectSound 流数据范围](directsound-stream-data-range.md)。

-   有关 MIDI 和 DirectMusic 数据范围的示例声明，请参阅 [Midi 流数据范围](midi-stream-data-range.md) 和 [DirectMusic 流数据范围](directmusic-stream-data-range.md)。

-   有关非 PCM 格式的数据范围的示例声明，请参阅 [指定 AC 3 数据范围](specifying-ac-3-data-ranges.md) 和 [指定 WMA Pro 数据范围](specifying-wma-pro-data-ranges.md)。

 


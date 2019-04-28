---
title: 指定引脚数据范围
description: 指定引脚数据范围
ms.assetid: bef74cd1-d2be-402d-be7f-acc7d8cbf392
keywords:
- pin WDK 音频，数据范围
- WDM 音频驱动程序 WDK，pin 数据范围
- 音频驱动程序 WDK，pin 数据范围
- 数据范围 WDK 音频 pin
- 可配置 pin WDK 音频驱动程序
- 格式 WDK 音频，pin 数据范围
- 交集 WDK 音频驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 079a7f348257d6aa9f6c77d1e940d8f94efdd389
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328619"
---
# <a name="specifying-pin-data-ranges"></a>指定引脚数据范围


定义表示数据路径和控制你的设备中的节点的拓扑之后, 的下一步是定义[数据范围](audio-data-ranges.md)对于每个可配置的插针。 可以创建、 配置和连接到的批或软件控制下的 MIDI 流可配置的 pin。 与此相反，物理连接或桥 pin 存在隐式和既不能创建也不能在软件控制下配置。

连接之前可配置 pin 作为接收器或批或 MIDI 流源，必须配置 pin 来处理流的数据格式。 通常情况下，pin 可以配置为接受多个流格式之一。 例如，PCM wave 输出插针可能会接受 PCM 流参数的以下范围：

-   11.025 kHz、 22.05 kHz、 44.1 kHz 和 48khz 的采样速率

-   8、 16、 24 和 32 位的示例大小

-   任意数目的 1 到 8 之间的信道

对于每种类型的可配置的 pin，微型端口驱动程序描述 pin 可以处理各种流数据格式。 可以为数组的数据范围说明符指定这些参数范围，如下面的代码示例中所示。

```cpp
static KSDATARANGE_AUDIO PinDataRangesPcm[] =
{
    {
        {
            sizeof(KSDATARANGE_AUDIO),
            0,
            0,
            0,
            STATICGUIDOF(KSDATAFORMAT_TYPE_AUDIO),
            STATICGUIDOF(KSDATAFORMAT_SUBTYPE_PCM),
            STATICGUIDOF(KSDATAFORMAT_SPECIFIER_WAVEFORMATEX)
        },
        8,       // Maximum number of channels
        8,       // Minimum number of bits-per-sample
        32,      // Maximum number of bits-per-channel
        11025,   // Minimum rate
        48000    // Maximum rate
    }
};
```

请注意，`PinDataRangesPcm`前面的示例中的数组包含类型的单个数据范围描述符[ **KSDATARANGE\_音频**](https://msdn.microsoft.com/library/windows/hardware/ff537096)。 一般来说，数据范围数组可以包含任意数量的描述符。 例如，AC-3-over-S/PDIF 和 WMA Pro-反复-S/PDIF 格式可能支持非 PCM wave 输出插针。 这两种格式的每个单独的数据范围说明符指定。 因此，固定的数据范围数组将包含至少两个 KSDATARANGE\_音频结构。

支持使用 DirectMusic 或 Windows 多媒体 midiIn 的应用程序中的音乐流格式的可配置 pin*Xxx*和 midiOut*Xxx*函数使用类型的数据范围描述符[ **KSDATARANGE\_音乐**](https://msdn.microsoft.com/library/windows/hardware/ff537097)。

端口驱动程序从微型端口驱动程序中获得的数据范围信息，并使用此信息，如有可能，用于处理请求的每个 pin 可以支持的数据格式的信息。 对于简单的 PCM 数据范围的 pin，端口驱动程序是能够处理该 pin 的交集请求。 在交集请求中，客户端提供一的组表示流的可能的数据格式的数据范围。 如果可能，端口驱动程序的交集处理程序还会在其 pin 的数据范围内的请求中提取来自数据区域的特定数据格式。 这种格式表示数据区域的两个集的交集。 因此，客户端和 pin 可以处理此格式的流。 对于更复杂的数据范围，微型端口驱动程序可以提供自己的交集处理程序，它将端口驱动程序然后使用其自身的、 默认处理程序。 微型端口驱动程序的交集处理程序可允许可能很难到端口驱动程序将表示为一组数据区域的任何格式要求。 有关详细信息，请参阅[交集数据处理程序](data-intersection-handlers.md)。 在标题为的白皮书提供了其他信息*多声道音频数据和 WAVE 文件*处[音频技术](https://go.microsoft.com/fwlink/p/?linkid=8751)网站。

 

 





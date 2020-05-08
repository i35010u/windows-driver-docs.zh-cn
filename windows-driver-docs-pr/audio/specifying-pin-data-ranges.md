---
title: 指定引脚数据范围
description: 指定引脚数据范围
ms.assetid: bef74cd1-d2be-402d-be7f-acc7d8cbf392
keywords:
- 锁定 WDK 音频，数据范围
- WDM 音频驱动程序 WDK，固定数据范围
- 音频驱动程序 WDK，固定数据范围
- 数据范围 WDK 音频、pin
- 可配置的 pin 音频驱动程序
- 格式化 WDK 音频，固定数据范围
- 与 WDK 音频驱动程序的交集
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 251ab44242d47cde57eb08ac81636b17e7ef746c
ms.sourcegitcommit: 98930ca95b9adbb6e5e472f89e91ab084e67e31d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2020
ms.locfileid: "82925512"
---
# <a name="specifying-pin-data-ranges"></a>指定引脚数据范围


定义拓扑以表示设备中的数据路径和控制节点后，下一步就是为每个可配置的 pin 定义[数据范围](audio-data-ranges.md)。 可以在软件控制下创建和配置可配置的 pin，并将其连接到波形或 MIDI 流。 相反，物理连接或桥接 pin 是隐式存在的，不能在软件控制下创建或配置。

在将可配置的 pin 连接为波形或 MIDI 流的接收器或源之前，必须将 pin 配置为处理流的数据格式。 通常，可以将 pin 配置为接受多种流格式之一。 例如，PCM 波形输出 pin 可能会接受以下范围的 PCM 流参数：

-   采样速率为 11.025 kHz，22.05 kHz，44.1 kHz，48 kHz

-   8、16、24和32位的示例大小

-   任意数量的通道，从1到8

对于每种类型的可配置 pin，微型端口驱动程序描述了 pin 可处理的各种流数据格式。 可以将这些参数范围指定为数据范围说明符的数组，如下面的代码示例中所示。

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

请注意， `PinDataRangesPcm`前面的示例中的数组包含类型为[**KSDATARANGE\_AUDIO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdatarange_audio)的单个数据范围说明符。 通常，数据范围数组可以包含任意数量的描述符。 例如，非 PCM 波形输出 pin 可能同时支持 AC-3 over S/PDIF 和 WMA Pro/PDIF 格式。 这两种格式中的每一种都是通过单独的数据范围说明符来指定的。 因此，pin 的数据范围数组包含至少两个 KSDATARANGE\_音频结构。

支持从使用 DirectMusic 的应用程序或 Windows 多媒体 midiIn*xxx*和 midiOut*Xxx*函数的应用程序中使用音乐流格式的可配置 Pin 使用类型为[**KSDATARANGE\_音乐**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdatarange_music)的数据范围说明符。

端口驱动程序从微型端口驱动程序获取数据范围信息，并使用此信息来处理请求，以获取有关每个 pin 所能支持的数据格式的信息。 对于具有简单 PCM 数据范围的 pin，端口驱动程序能够处理该 pin 的交集请求。 在交集请求中，客户端提供一组表示流的可能数据格式的数据范围。 如果可能，端口驱动程序的交集处理程序将从请求中的数据范围中选择特定的数据格式，该数据范围也位于其 pin 的数据范围内。 此格式表示两组数据范围的交集。 因此，客户端和 pin 都可以使用此格式处理流。 对于更复杂的数据范围，微型端口驱动程序可以提供自己的交集处理程序，端口驱动程序将使用该处理程序而不是自己的默认处理程序。 微型端口驱动程序的交集处理程序可允许任何格式要求，这些要求可能难于将端口驱动程序表示为数据范围的数组。 有关详细信息，请参阅[数据交集处理程序](data-intersection-handlers.md)和[多通道音频数据和波形文件](https://docs.microsoft.com/previous-versions/windows/hardware/design/dn653308(v=vs.85))。

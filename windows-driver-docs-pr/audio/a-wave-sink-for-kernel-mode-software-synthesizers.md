---
title: 适用于内核模式软件合成器的 Wave 接收器
description: 适用于内核模式软件合成器的 Wave 接收器
ms.assetid: 37ba9ad5-8b35-4252-a6fd-46dead924294
keywords:
- 批接收器 WDK 音频，内核模式软件合成器
- MIDI 传输 WDK 音频
- 批接收器 WDK 音频，MIDI 传输
- 合成器 WDK 音频，MIDI 传输
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0be821517300d4b56681d5fa8706c819aba4a372
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355794"
---
# <a name="a-wave-sink-for-kernel-mode-software-synthesizers"></a>适用于内核模式软件合成器的 Wave 接收器


## <span id="a_wave_sink_for_kernel_mode_software_synthesizers"></span><span id="A_WAVE_SINK_FOR_KERNEL_MODE_SOFTWARE_SYNTHESIZERS"></span>


中所述[合成和批接收器](synthesizers-and-wave-sinks.md)，Dmu 端口驱动程序实现在内核模式下运行软件合成器的批接收器。 合成器的微型端口驱动程序公开[ISynthSinkDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-isynthsinkdmus)端口驱动程序的接口。 端口驱动程序的批接收器使用此接口来读取由合成器生成的批数据。

若要充分利用 Dmu 端口驱动程序的批接收器 Dmu 微型端口驱动程序应定义具有两种类型的 pin 的 DirectMusic 筛选器：

-   DirectMusic 输入插针或 MIDI 输入插针。 此 pin 是包含 MIDI 消息的呈现流的接收器。

-   Wave 输出插针。 此 pin 是包含 PCM 示例的呈现流的源。

下图显示了包含合成器节点的 DirectMusic 筛选器 ([**KSNODETYPE\_合成器**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-synthesizer))。 此筛选器满足上述要求的内核模式软件合成器通过提供 DirectMusic 输入插针和 wave 输出插针。 （此外，支持旧 MIDI 合成 Dmu 微型端口驱动程序可以提供 MIDI 输入插针。）

![说明的内核模式软件合成器的 directmusic 筛选器的关系图](images/wavesink.png)

上图的左侧，MIDI 流将进入 DirectMusic 输入插针通过筛选器。 此插针[IMXF](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-imxf)端口驱动程序向其公开的接口。 端口驱动程序将获取通过调用此接口[ **IMiniportDMus::NewStream** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-iminiportdmus-newstream)方法。 端口驱动程序通过调用馈送 MIDI 消息到的插针[ **IMXF::PutMessage** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-imxf-putmessage)方法。

上图的右侧，批流退出到端口驱动程序的批接收器的 wave 输出插针和流通过筛选器。 通过 pin 与通信端口驱动程序及其**ISynthSinkDMus**接口。 端口驱动程序通过第一个调用来获取此接口**IMiniportDMus::NewStream**若要获取与一个 stream 对象**IMXF**接口，并在然后查询对象的其**ISynthSinkDMus**接口。 批接收器拉取通过调用批数据从 pin [ **ISynthSinkDMus::Render** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-isynthsinkdmus-render)方法。

尽管硬件合成器无法从原理上讲，依赖于端口驱动程序的呈现，在调用批接收器**ISynthSinkDMus::Render**将足够延迟添加到要使其不严重的许多交互式的 MIDI 流应用程序。 若要减少流延迟，硬件合成器很可能会有内部连接到混合和批呈现的硬件，而不是使用端口驱动程序的批接收器。 这种类型的合成器替换硬编码连接为 wave 输出插针上图右侧 (表示为*桥 pin*) 硬件混音器。

**ISynthSinkDMus**接口提供可呈现批接收器，通过波形数据的方法将其从引用时间转换为采样时间和背面，并同步到 master 时钟：

[**ISynthSinkDMus::RefTimeToSample**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-isynthsinkdmus-reftimetosample)

[**ISynthSinkDMus::Render**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-isynthsinkdmus-render)

[**ISynthSinkDMus::SampleToRefTime**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-isynthsinkdmus-sampletoreftime)

[**ISynthSinkDMus::SyncToMaster**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-isynthsinkdmus-synctomaster)

**ISynthSinkDMus**继承自**IMXF**接口。 有关详细信息，请参阅[ISynthSinkDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-isynthsinkdmus)。

Dmu 微型端口驱动程序在上图中标识其 DirectMusic 输入插针和 wave 输出插针，如下所示：

-   若要确定其 DirectMusic 输入插针，微型端口驱动程序定义 pin 的数据范围的主要格式为类型 KSDATAFORMAT\_类型\_音乐和的子格式类型 KSDATAFORMAT\_子类型\_DIRECTMUSIC。 此组合指示 pin 接受加盖时间戳 MIDI 流。 数据范围描述符是类型的结构[ **KSDATARANGE\_音乐**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksdatarange_music)。 (有关示例，请参阅[DirectMusic Stream 数据范围](directmusic-stream-data-range.md)。)微型端口驱动程序定义 pin 的数据流方向为 KSPIN\_数据流\_in。 ( [ **PCPIN\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/ns-portcls-pcpin_descriptor)结构的**KsPinDescriptor**。数据流成员表示数据流方向）。调用时**IMiniportDMus::NewStream**若要创建此 pin 的流对象，该端口驱动程序设置*StreamType* DMU 参数\_流\_MIDI\_呈现。

-   若要确定其 wave 输出插针，微型端口驱动程序定义 pin 的数据范围的主要格式为类型 KSDATAFORMAT\_类型\_音频和的子格式类型 KSDATAFORMAT\_子类型\_PCM。 这一系列表示 pin 发出包含 PCM 示例的波形音频流。 数据范围描述符是类型的结构[ **KSDATARANGE\_音频**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksdatarange_audio)。 (请参阅中的示例[PCM Stream 数据范围](pcm-stream-data-range.md)。)微型端口驱动程序定义 pin 的数据流方向为 KSPIN\_数据流\_出。 调用时**IMiniportDMus::NewStream**若要创建此 pin 的流对象，该端口驱动程序设置*StreamType* DMU 参数\_流\_批\_接收器。

此外，如果该驱动程序以支持 MIDI 输入插针的合成器，其定义将是类似于 DirectMusic 输入插针，但 pin 定义将指定类型 KSDATAFORMAT 的子格式\_子类型\_MIDI，和 pin 以接受原始的 MIDI 流而不是带有时间戳 MIDI 流。

 

 





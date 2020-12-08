---
title: 适用于内核模式软件合成器的 Wave 接收器
description: 适用于内核模式软件合成器的 Wave 接收器
keywords:
- 波形接收器 WDK 音频，内核模式软件合成程序
- MIDI 传输 WDK 音频
- 波形接收器音频，MIDI 传输
- 合成 WDK 音频，MIDI 传输
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8efaf6324b34c1f4a3126d2d005d144f278eb246
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785057"
---
# <a name="a-wave-sink-for-kernel-mode-software-synthesizers"></a>适用于内核模式软件合成器的 Wave 接收器


## <span id="a_wave_sink_for_kernel_mode_software_synthesizers"></span><span id="A_WAVE_SINK_FOR_KERNEL_MODE_SOFTWARE_SYNTHESIZERS"></span>


如上所述，Dmu 端口驱动程序 [为在内核](synthesizers-and-wave-sinks.md)模式下操作的软件合成器实现了波形接收器。 合成器的微型端口驱动程序向端口驱动程序公开 [ISynthSinkDMus](/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-isynthsinkdmus) 接口。 端口驱动程序的波形接收器使用此接口读取合成器生成的波形数据。

若要使用 Dmu 端口驱动程序的 wave 接收器，Dmu 微型端口驱动程序应使用两种类型的 pin 定义 DirectMusic 筛选器：

-   DirectMusic 输入插针或 MIDI 输入插针。 此 pin 是包含 MIDI 消息的呈现流的接收器。

-   波形输出插针。 此 pin 是包含 PCM 样本的呈现流的源。

下图显示了一个包含合成器节点 ([**KSNODETYPE \_ 合成**](./ksnodetype-synthesizer.md) 器) 的 DirectMusic 筛选器。 此筛选器通过提供 DirectMusic 的输入插针和波形输出 pin 满足上述内核模式软件合成器的要求。  (此外，支持旧版 MIDI 合成的 Dmu 微型端口驱动程序可以提供 MIDI 输入插针。 ) 

![阐释内核模式软件合成器的 directmusic 筛选器的关系图](images/wavesink.png)

在该图的左侧，MIDI 流通过 DirectMusic 输入 pin 进入筛选器。 此 pin 具有公开给端口驱动程序的 [IMXF](/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-imxf) 接口。 端口驱动程序通过调用 [**IMiniportDMus：： newstream.ischecked**](/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-iminiportdmus-newstream) 方法获取此接口。 端口驱动程序通过调用 [**IMXF：:P utmessage**](/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-imxf-putmessage) 方法将 MIDI 消息馈送到该 pin。

在该图的右侧，波形流通过波形输出插针退出筛选器，并流向端口驱动程序的波形接收器。 端口驱动程序通过其 **ISynthSinkDMus** 接口与 pin 通信。 端口驱动程序首先调用 **IMiniportDMus：： newstream.ischecked** 以获取具有 **IMXF** 接口的流对象，然后查询该对象的 **ISynthSinkDMus** 接口，从而获取此接口。 波形接收器通过调用 [**ISynthSinkDMus：： Render**](/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-isynthsinkdmus-render) 方法从 pin 中提取波数据。

尽管硬件合成器可能会依赖于端口驱动程序的波形接收器进行呈现，但对 MIDI 流的调用会将足够的 **延迟添加到** MIDI 流，使其不严重许多交互式应用程序。 为了减少流延迟，硬件合成程序可能会建立与混合和波形渲染硬件的内部连接，而不是使用端口驱动程序的波形接收器。 这种类型的合成器将上图右侧的波形输出插针替换为硬编码连接 (表示为) 到硬件混合器的 *桥接* 。

**ISynthSinkDMus** 接口提供了一些方法，可通过波形接收器呈现波形数据、从引用时间转换为采样时间和背面，并同步到主时钟：

[**ISynthSinkDMus::RefTimeToSample**](/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-isynthsinkdmus-reftimetosample)

[**ISynthSinkDMus：： Render**](/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-isynthsinkdmus-render)

[**ISynthSinkDMus::SampleToRefTime**](/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-isynthsinkdmus-sampletoreftime)

[**ISynthSinkDMus::SyncToMaster**](/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-isynthsinkdmus-synctomaster)

**ISynthSinkDMus** 继承自 **IMXF** 接口。 有关详细信息，请参阅 [ISynthSinkDMus](/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-isynthsinkdmus)。

上图中的 Dmu 微型端口驱动程序标识其 DirectMusic 输入插针和波形输出 pin，如下所示：

-   为标识其 DirectMusic 输入 pin，小型端口驱动程序会定义 pin 的数据范围，使其具有类型为 KSDATAFORMAT 类型的 \_ \_ 音乐和 SUBFORMAT 类型 KSDATAFORMAT \_ 子类型 \_ DirectMusic 的主要格式。 此组合指示 pin 接受带有时间戳的 MIDI 流。 数据范围描述符是 [**KSDATARANGE \_ 音乐**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdatarange_music)类型的结构。  (的示例，请参阅 [DirectMusic 流数据范围](directmusic-stream-data-range.md)。 ) 微型端口驱动程序定义要在其中 KSPIN 数据流的 pin 数据流 \_ 方向 \_ 。  ([**PCPIN \_ 描述符**](/windows-hardware/drivers/ddi/portcls/ns-portcls-pcpin_descriptor) 结构的 **KsPinDescriptor**。数据流成员指示数据流方向 ) 。在调用 **IMiniportDMus：： newstream.ischecked** 创建此 pin 的流对象时，端口驱动程序会将 *StreamType* 参数设置为 dmu \_ 流 \_ MIDI \_ RENDER。

-   为标识其波形输出 pin，小型端口驱动程序会定义 pin 的数据范围，使其具有类型为 KSDATAFORMAT \_ 类型的 \_ 音频和 subformat KSDATAFORMAT 子类型 \_ \_ PCM 的主要格式。 此组合指示 pin 发出包含 PCM 样本的 wave 音频流。 数据范围描述符是 [**KSDATARANGE \_ AUDIO**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdatarange_audio)类型的结构。  (参见[PCM 流数据范围](pcm-stream-data-range.md)中的示例。 ) 微型端口驱动程序定义要 KSPIN 流 \_ 出的 pin 数据流方向。 \_ 调用 **IMiniportDMus：： newstream.ischecked** 为此 pin 创建流对象时，端口驱动程序会将 *StreamType* 参数设置为 dmu \_ stream \_ WAVE \_ SINK。

此外，如果驱动程序支持用于合成器的 MIDI 输入插针，则其定义类似于 DirectMusic 输入 pin 的定义，但 pin 定义将指定 KSDATAFORMAT 子类型的 subformat 类型 \_ \_ ，并且 pin 将接受原始 MIDI 流，而不是带时间戳的 midi 流。

 


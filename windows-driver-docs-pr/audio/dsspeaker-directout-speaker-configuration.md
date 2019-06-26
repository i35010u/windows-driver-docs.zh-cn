---
title: DSSPEAKER_DIRECTOUT 扬声器配置
description: DSSPEAKER_DIRECTOUT 扬声器配置
ms.assetid: a4198fb7-157f-40e3-8cca-5a9e392087d2
keywords:
- DSSPEAKER_DIRECTOUT 扬声器配置 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 32d327fafff9fe7794d3d9ac15025b10b2325305
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360084"
---
# <a name="dsspeakerdirectout-speaker-configuration"></a>DSSPEAKER\_DIRECTOUT 扬声器配置


## <span id="dsspeaker_directout_speaker_configuration"></span><span id="DSSPEAKER_DIRECTOUT_SPEAKER_CONFIGURATION"></span>


**请注意**  此信息适用于 Windows XP 和早期版本的操作系统。 从 Windows Vista 开始**IDirectSound::GetSpeakerConfig**并**IDirectSound::SetSpeakerConfig**已弃用。

 

应用程序可以更改 DirectSound 扬声器配置为直接扩展模式通过调用**IDirectSound::SetSpeakerConfig**方法替换扬声器配置参数设置为 DSSPEAKER\_DIRECTOUT （请参阅 Microsoft Windows SDK 文档）。 这将指定在其中播放流从应用程序中的通道将输出直接向音频适配器而不被解释为扬声器位置 speakerless 配置。 但是，仍可以通过采样率转换、 衰减、 筛选和其他类型的处理不要求的说话人到的频道分配任何假设修改输入的流。

一旦设置将生效，DSSPEAKER\_DIRECTOUT 扬声器配置设置是全局设置，会影响作为一个整体的音频设备。 随后运行的所有音频应用程序可能会有所新的设置，直到 DirectSound 更改该设置再次。

在直接扩展模式下，音频设备呈现到该设备上的第一个输出连接器的第一个通道、 设备等上的第二个输出的第二个通道。 这允许音频创作应用程序输出多渠道数据直接向外部 mixer 等设备或音频存储设备 （硬盘、 ADAT，等）。 例如下, 表中所示，则可能会分配 48 通道流中的通道。

通道编号内容 0

语音服务

1

罐

2

吉他

3

低音

...

47

钢琴

 

对于此类型的原始音频数据，扬声器位置无意义的并分配扬声器的位置输入或输出流可能会导致不需要的副作用。 例如，如 KMixer 组件可能不恰当地介入，通过将应用特定于说话人的效果，如 3D 虚拟化或 Dolby Surround Pro 逻辑编码到流。 请注意原始数据通道数不受通道掩码中比特数。

即使设备设计不是专门用于音频编辑通常应接受[ **KSPROPERTY\_音频\_通道\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-channel-config)设置属性请求以更改其扬声器配置到 KSAUDIO\_演讲者\_DIRECTOUT。 一般情况下，设备应避免失败请求，除非它可以以某种方式来验证其输出连接到扬声器和不能用作外部的任何其他目的 （例如，外部混音器的输入）。

使用直接扩展模式下的应用程序通常专为特定硬件设备。 这允许应用程序事先知道哪些直接扩展数据格式以设备支持，包括通道以及应如何解释这些信道中的数据的数量。 这一知识是必需的因为当应用程序调用**IDirectSound::GetSpeakerConfig**中直接扩展模式配置设备，设备只是确定它是在此模式下; 它提供了无需额外有关它在直接扩展模式下支持的流格式中的通道数信息。 (此信息可能会获取，但是，通过发送[ **KSPROPERTY\_音频\_混合\_级别\_CAPS** ](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-mix-level-caps)属性 get 请求到在设备的 mixer pin; supermixer 节点请参阅[DirectSound 节点排序要求](directsound-node-ordering-requirements.md)。)

指定直接扩展流波形格式时，应用程序应设置**dwChannelMask**的成员[ **WAVEFORMATEXTENSIBLE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-waveformatextensible)结构的值KSAUDIO\_演讲者\_DIRECTOUT，为零。 将通道掩码设置为零指示定义的没有扬声器位置。 如往常一样中, 指定的流中的通道数**Format.nChannels**成员。

硬件供应商可以支持 DirectSound 硬件加速，其设备配置在直接扩展模式下时的选择。 DirectSound 应用程序可以播放直接扩展流通过其中一个设备的混合的 pin，如果有可用。 一旦已用尽所有可用的硬件 pin 实例，任何新流将通过 KMixer 相反。

在直接扩展模式下配置后的设备的流混合，KMixer 适用于设备的应用程序中的输入流的通道和它将输出的混合流的通道之间的一对一映射。 这意味着，如果应用程序生成多个具有相同数目的通道的直接扩展流，例如，输出组合的每个通道 N 是只需输入 KMixer 的所有流的通道 N 的总和。

在混合的区别在于它们所包含的通道数的几个直接扩展流，KMixer 的混合算法是稍微复杂一些。 在这种情况下，组合的每个通道 N 是通道 N 具有通道 n。 所有输入流的总数例如，如果 KMixer 包含四核和立体声输入的流，以形成四输出混合，通道零和一输出组合的将是零和通道的分别输入的立体声和四个流的总和。 立体声输入的流没有任何价值，但是，到频道 2 和 3 的组合，只从四个输入流的最后两个通道创建。

尝试执行以下任一操作的应用程序导致不可预知的行为存在风险：

-   播放不是通过在直接扩展模式下配置的设备的直接扩展格式的流。

-   通过设备未在直接扩展模式下配置播放直接出流。

当面对一个这种情况下，可避免 KMixer，只需失败尝试打开流。 相反，它尝试通过使用上文所述的一对一的映射算法处理明显不兼容性。 用户可能会或可能不是结果感到满意。 其他音频组件不会作为 KMixer 相同的方式处理这种情况。 例如，在直接扩展模式下配置的设备的驱动程序应该会尝试打开不是直接向外格式，反之亦然的输出流的硬件缓冲区失败。

音频创作应用程序可能需要用户可侦听对它有混合的第一个数据其输出的几个渠道流式传输，但忽略仍包含在流的其余通道的原始数据。 KMixer 的行为轻松实现此目的。 例如，如果 24 频道可以播放流包含通道 2 到 23 中的通道 0 和 1 和原始数据中的立体声混音，应用程序执行以下任务：

-   配置目标音频设备 （这不一定是应用程序用于编辑流的设备） 在通过调用立体声模式下**SetSpeakerConfig**与 DSSPEAKER\_立体声。

-   更改**dwChannelMask**中播放流[ **WAVEFORMATEXTENSIBLE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-waveformatextensible)结构 KSAUDIO\_演讲者\_立体声但离开**Format.nChannels**设置为 24，这是流中的通道的总数。

KMixer 混合使用仅的立体声通道播放流的通道掩码中所述，并丢弃其余的 22 通道，其中包含的原始数据。 请记住对 DirectSound 扬声器配置设置进行任何更改不太可能才会生效，直到当前 DirectSound 对象被销毁并创建另一个 (请参阅[应用扬声器配置设置](applying-speaker-configuration-settings.md))。

 

 





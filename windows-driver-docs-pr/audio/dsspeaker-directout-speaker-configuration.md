---
title: DSSPEAKER_DIRECTOUT 扬声器配置
description: DSSPEAKER_DIRECTOUT 扬声器配置
ms.assetid: a4198fb7-157f-40e3-8cca-5a9e392087d2
keywords:
- DSSPEAKER_DIRECTOUT 发言人配置 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c43f4bfa8f6213b9293433bb71b67f2e5d8ffe2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833419"
---
# <a name="dsspeaker_directout-speaker-configuration"></a>DSSPEAKER\_DIRECTOUT 发言人配置


## <span id="dsspeaker_directout_speaker_configuration"></span><span id="DSSPEAKER_DIRECTOUT_SPEAKER_CONFIGURATION"></span>


**请注意**  此信息适用于 Windows XP 及更早版本的操作系统。 从 Windows Vista 开始， **IDirectSound：： GetSpeakerConfig**和**IDirectSound：： SetSpeakerConfig**已弃用。

 

应用程序可以通过调用**IDirectSound：： SetSpeakerConfig**方法，并将扬声器配置参数设置为 DSSPEAKER\_DIRECTOUT，将 DirectSound 扬声器配置更改为直接输出模式（请参阅 Microsoft WindowsSDK 文档）。 这将指定一个 speakerless 配置，其中应用程序的播放流中的通道直接输出到音频适配器，而不会被解释为发言人位置。 但是，输入流仍可通过采样率转换、衰减、筛选和其他类型的处理进行修改，这些处理不需要将扬声器分配给频道。

一旦生效，DSSPEAKER\_DIRECTOUT 扬声器配置设置是全局性的，并影响音频设备作为整体。 随后运行的所有音频应用程序都将受新设置的限制，直到 DirectSound 再次更改设置。

在直接输出模式下，音频设备会将第一个通道呈现到设备上的第一个输出连接器，将第二个通道呈现到设备上的第二个输出，依此类推。 这允许音频创作应用程序将多通道数据直接输出到设备，例如外部混音器或音频存储设备（硬盘、ADAT 等）。 例如，可以按下表所示分配48信道流中的通道。

频道号内容0

沉默

1

强光

2

吉他

3

低音

...

47

钢琴

 

对于这种原始音频数据，发言人位置毫无意义，为输入流和输出流指定扬声器位置可能会导致意外的副作用。 例如，如果某个组件（如 KMixer）通过应用特定于扬声器的效果（例如，3D 虚拟化或对流环绕 Pro 逻辑编码），则可能无法正确地进行干预。 请注意，原始数据通道数不受通道掩码中的位数限制。

即使是不是专门针对音频编辑设计的设备，也应接受[**KSPROPERTY\_音频\_通道\_配置**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-channel-config)设置属性请求，将其扬声器配置更改为 KSAUDIO\_发言人\_DIRECTOUT. 通常，设备应避免失败请求，除非它可以通过某种方式验证其输出是否已连接到扬声器，并且不能在外部用于任何其他用途（例如，作为外部混音器的输入）。

使用直接输出模式的应用程序通常是针对特定硬件设备编写的。 这使应用程序能够事先知道设备支持的直接输出数据格式，包括通道数量以及应如何解释这些通道中的数据。 此知识是必需的，因为当应用程序在以直接扩展模式配置的设备上调用**IDirectSound：： GetSpeakerConfig**时，设备只需确认它处于此模式下;它不提供有关在直接输出模式下支持的流格式的通道数的附加信息。 （但是，可以通过将[**KSPROPERTY\_音频\_混合\_级别\_cap**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-mix-level-caps)获取-属性请求发送到设备的混合器 pin 上的 supermixer 节点获取此信息; 请参阅[DirectSound 节点顺序要求](directsound-node-ordering-requirements.md).)

为直接流指定波形格式时，应用程序应将[**WAVEFORMATEXTENSIBLE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-waveformatextensible)结构的**dwChannelMask**成员设置为值 KSAUDIO\_发言人\_DIRECTOUT，该值为零。 通道掩码为零表示未定义发言人位置。 与往常一样，流中的通道数以**nChannels**成员的形式指定。

硬件供应商可以选择在直接模式下配置其设备时支持 DirectSound 硬件加速。 DirectSound 应用程序可以通过设备的混合 pin （如果有）播放直接流。 所有可用的硬件 pin 实例都用尽后，将改为通过 KMixer 传递任何新流。

当混合使用直接输出模式下配置的设备的流时，KMixer 会将输入流的通道与应用程序和它输出到设备的组合流的通道之间进行一对一映射。 这意味着，如果应用程序生成多个具有相同通道数的直接流，则输出混合的每个通道 N 只是所有输入 KMixer 的流的通道 N 的总和。

混合多个直接输出流时，它们所包含的通道数不同，KMixer 的混合算法稍微复杂一些。 在这种情况下，组合的每个通道 N 为所有输入流中具有通道 N 的通道 N 之和。例如，如果 KMixer 混合使用四个和立体声输入流来形成四个输出混合，则通道零和其中一个输出混合是输入立体声和四个通道的每个通道的总和。 但立体声输入流对两个和三个混合通道均不起作用，只是从四个输入流的最后两个通道中提取。

尝试执行以下任一操作的应用程序可能会导致不可预知的行为：

-   通过在直接传出模式下配置的设备播放非直接格式的流。

-   通过未在直接超时模式下配置的设备播放直接流。

当面对其中一种情况时，KMixer 可以避免尝试打开流。 相反，它会尝试使用上文所述的一对一映射算法来处理明显的不兼容。 该用户可能会对结果感到满意，也可能不满意。 其他音频组件不能以与 KMixer 相同的方式处理这些情况。 例如，在直接输出模式下配置的设备的驱动程序应尝试为不是直接输出格式的输出流打开硬件缓冲区，反之亦然。

音频创作应用程序可能需要让用户侦听其已混合到其输出流的前几个通道中的数据，但忽略仍包含在流的其余通道中的原始数据。 KMixer 的行为使这一点非常简单。 例如，如果24通道播放流在通道0中包含立体声混合，在通道2到23中包含原始数据，则该应用程序将执行以下操作：

-   通过使用 DSSPEAKER\_立体声调用**SetSpeakerConfig** ，以立体声模式配置目标音频设备（这不一定是应用程序用于编辑流的设备）。

-   将播放流的[**WAVEFORMATEXTENSIBLE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-waveformatextensible)结构中的**DWCHANNELMASK**更改为 KSAUDIO\_音箱\_立体声，但保留**格式。 nChannels**设置为24，这是流中的通道总数。

KMixer 仅混合播放流的立体声通道（在通道掩码中进行了描述），并放弃其余22个通道，其中包含原始数据。 请记住，在销毁当前 DirectSound 对象并创建另一个对象之前，对 DirectSound 扬声器的配置设置所做的任何更改都不太可能生效（请参阅[应用扬声器配置设置](applying-speaker-configuration-settings.md)）。

 

 





---
title: DSSPEAKER_SURROUND 扬声器配置
description: DSSPEAKER_SURROUND 扬声器配置
keywords:
- DSSPEAKER_SURROUND 发言人配置 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76386f8100a2819ca2717b2e1d6ecc9122fd7a06
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786551"
---
# <a name="dsspeaker_surround-speaker-configuration"></a>DSSPEAKER \_ 环绕发言人配置


## <span id="dsspeaker_surround_speaker_configuration"></span><span id="DSSPEAKER_SURROUND_SPEAKER_CONFIGURATION"></span>


**注意**  此信息适用于 Windows XP 及更早版本的操作系统。 从 Windows Vista 开始， **IDirectSound：： GetSpeakerConfig** 和 **IDirectSound：： SetSpeakerConfig** 已弃用。

 

应用程序可以通过调用 **IDirectSound：： SetSpeakerConfig** 方法将 DirectSound 扬声器配置更改为环绕模式，将扬声器配置参数设置为 DSSPEAKER \_ 环绕。 这将指定一个四通道 PCM 格式，其中通道映射到左、右、中和后扬声器。

一旦生效，DSSPEAKER \_ 环绕发言人的配置设置是全局性的，影响音频设备。 随后运行的所有音频应用程序都将受新设置的限制，直到 DirectSound 再次更改设置。

DirectSound 使用以下算法为环绕模式配置音频系统：

1.  DirectSound 首先要求驱动程序进入环绕发言人模式，方法是将 [**KSPROPERTY \_ 音频 \_ 通道 \_ 配置**](./ksproperty-audio-channel-config.md) 设置属性请求发送到驱动程序的 dac 节点 (或3d 节点（如果它没有 DAC 节点) ）。  (参阅 [**KSNODETYPE \_ DAC**](./ksnodetype-dac.md) and [**KSNODETYPE \_ 3d \_ 效果**](./ksnodetype-3d-effects.md)。 ) 此属性请求附带的 [**KSAUDIO \_ 通道 \_ CONFIG**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_channel_config) 结构指定 KSAUDIO \_ 扬声器 \_ 环绕扬声器配置。 如果请求成功，则音频设备将四个通道路由到四个模拟输出，这些输出直接连接到左、右、中和后扬声器。

2.  如果此操作失败，DirectSound 会要求驱动程序将设备配置为立体声扬声器模式并启用其 [**KSNODETYPE \_ PROLOGIC \_ 编码器**](./ksnodetype-prologic-encoder.md) 节点（如果有）。 如果此方法成功，则设备会将应用程序中的四通道流转换为以数字或模拟形式输出的环绕声编码立体声信号。  (硬件在混合流入到设备的各种混音器引脚的流之后，应执行编码。 ) 用户可以将设备的立体声输出连接到外部解码器，将编码的信号转换为向左、右、居中和背面扬声器输出的四个通道。

3.  如果此操作失败，DirectSound 将启用 \_ KMixer 中的 KSNODETYPE PROLOGIC \_ 编码器节点。  (设备已在上一步中处于立体声模式下。再次 ) ，设备输出的立体声信号可以送入外部解码器。

如果此算法成功，应用程序可以创建并播放四通道 PCM 缓冲区。 在上述情况中，设备从其读取的硬件缓冲区使用四个通道，但在第3种情况下，硬件缓冲区使用立体声格式。 应用程序可以在情况1和2中直接写入硬件缓冲区，但在这种情况下，它应该写入软件缓冲区，并允许 KMixer 将应用程序的四通道流转换为硬件缓冲区所需的环绕编码立体声格式。

在上述 (3) 情况下，应用程序应避免为其任何输出流使用硬件缓冲区。 请注意，在编码组合之前，KMixer 会混合其所有输入流以生成环绕立体声流。 但是，任何输入硬件混合器 pin 的流都在硬件中与 KMixer 的编码立体声混合，这会降低环绕音频在解码时的质量。 应用程序只能使用软件缓冲区来防止这种情况。

\_ \_ 可以通过 [**KSNODETYPE \_ PROLOGIC \_ 解码器**](./ksnodetype-prologic-decoder.md)节点 (左、右、左和后) 将由 KSNODETYPE PROLOGIC 编码器节点包围的立体声流解码为四个通道。

 


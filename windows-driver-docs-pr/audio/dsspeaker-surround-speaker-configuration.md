---
title: DSSPEAKER_SURROUND 扬声器配置
description: DSSPEAKER_SURROUND 扬声器配置
ms.assetid: de8f861b-f190-4915-b3f0-95d39965b612
keywords:
- DSSPEAKER_SURROUND 发言人配置 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51594299afbd6dfb932e938903f38864e136957b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833410"
---
# <a name="dsspeaker_surround-speaker-configuration"></a>DSSPEAKER\_环绕扬声器配置


## <span id="dsspeaker_surround_speaker_configuration"></span><span id="DSSPEAKER_SURROUND_SPEAKER_CONFIGURATION"></span>


**请注意**  此信息适用于 Windows XP 及更早版本的操作系统。 从 Windows Vista 开始， **IDirectSound：： GetSpeakerConfig**和**IDirectSound：： SetSpeakerConfig**已弃用。

 

应用程序可以通过调用**IDirectSound：： SetSpeakerConfig**方法将 DirectSound 扬声器配置更改为环绕模式，将扬声器配置参数设置为 DSSPEAKER\_环绕。 这将指定一个四通道 PCM 格式，其中通道映射到左、右、中和后扬声器。

一旦生效，DSSPEAKER\_环绕扬声器配置设置是全局性的，并影响音频设备作为整体。 随后运行的所有音频应用程序都将受新设置的限制，直到 DirectSound 再次更改设置。

DirectSound 使用以下算法为环绕模式配置音频系统：

1.  DirectSound 首先要求驱动程序进入环绕发言人模式，方法是将[**KSPROPERTY\_音频\_通道\_配置**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-channel-config)集属性请求发送到驱动程序的 dac 节点（如果它没有 DAC 节点，则为3d 节点）。 （请参阅[**KSNODETYPE\_DAC**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-dac)和[**KSNODETYPE\_3d\_效果**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-3d-effects)。）此属性请求附带的[**KSAUDIO\_通道\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_channel_config)结构指定了 KSAUDIO\_音箱\_环绕扬声器配置。 如果请求成功，则音频设备将四个通道路由到四个模拟输出，这些输出直接连接到左、右、中和后扬声器。

2.  如果此操作失败，DirectSound 会要求驱动程序将设备配置为立体声扬声器模式并启用其[**KSNODETYPE\_PROLOGIC\_编码器**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-prologic-encoder)"节点（如果有）。 如果此方法成功，则设备会将应用程序中的四通道流转换为以数字或模拟形式输出的环绕声编码立体声信号。 （硬件应在混合流入设备的各种混音器 pin 的流后执行编码。）用户可以将设备的立体声输出连接到外部解码器，该解码器将编码的信号转换为向左、右、居中和背面扬声器输出的四个声道。

3.  如果此操作失败，DirectSound 将启用 KMixer 中的 KSNODETYPE\_PROLOGIC\_编码器节点。 （设备已在上一步中处于立体声模式。）同样，设备输出的立体声信号可以送入外部解码器。

如果此算法成功，应用程序可以创建并播放四通道 PCM 缓冲区。 在上述情况中，设备从其读取的硬件缓冲区使用四个通道，但在第3种情况下，硬件缓冲区使用立体声格式。 应用程序可以在情况1和2中直接写入硬件缓冲区，但在这种情况下，它应该写入软件缓冲区，并允许 KMixer 将应用程序的四通道流转换为硬件缓冲区所需的环绕编码立体声格式。

在上述情况下（3），应用程序应避免为其任何输出流使用硬件缓冲区。 请注意，在编码组合之前，KMixer 会混合其所有输入流以生成环绕立体声流。 但是，任何输入硬件混合器 pin 的流都在硬件中与 KMixer 的编码立体声混合，这会降低环绕音频在解码时的质量。 应用程序只能使用软件缓冲区来防止这种情况。

KSNODETYPE\_PROLOGIC\_编码器节点的环绕式编码的立体声流可以通过[**KSNODETYPE\_PROLOGIC\_解码器**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-prologic-decoder)节点解码为四个通道（左、右、居中和后退）。

 

 





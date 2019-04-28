---
title: DSSPEAKER_SURROUND 扬声器配置
description: DSSPEAKER_SURROUND 扬声器配置
ms.assetid: de8f861b-f190-4915-b3f0-95d39965b612
keywords:
- DSSPEAKER_SURROUND 扬声器配置 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0859387180b6abd258c5a61b4fad154c84c584ed
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333720"
---
# <a name="dsspeakersurround-speaker-configuration"></a>DSSPEAKER\_环绕扬声器配置


## <span id="dsspeaker_surround_speaker_configuration"></span><span id="DSSPEAKER_SURROUND_SPEAKER_CONFIGURATION"></span>


**请注意**  此信息适用于 Windows XP 和早期版本的操作系统。 从 Windows Vista 开始**IDirectSound::GetSpeakerConfig**并**IDirectSound::SetSpeakerConfig**已弃用。

 

应用程序可以更改 DirectSound 扬声器配置，通过调用环绕模式**IDirectSound::SetSpeakerConfig**方法替换扬声器配置参数设置为 DSSPEAKER\_外侧代码。 这将指定通道将映射左、 右、 居中，且返回发言人的 4 个通道 PCM 格式。

一旦设置将生效，DSSPEAKER\_环绕扬声器配置设置是全局设置，会影响作为一个整体的音频设备。 随后运行的所有音频应用程序可能会有所新的设置，直到 DirectSound 更改该设置再次。

DirectSound 使用以下算法来配置用于环绕模式的音频系统：

1.  DirectSound 首先要求驱动程序通过发送进入环绕演讲者模式[ **KSPROPERTY\_音频\_通道\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff537250)集属性请求到驱动程序的 DAC 节点 （或 3D 节点是否有任何 DAC 节点）。 (请参阅[ **KSNODETYPE\_DAC** ](https://msdn.microsoft.com/library/windows/hardware/ff537158)并[ **KSNODETYPE\_3D\_效果**](https://msdn.microsoft.com/library/windows/hardware/ff537148)。)[ **KSAUDIO\_通道\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff537083)结构，此属性请求附带指定 KSAUDIO\_演讲者\_外侧代码扬声器配置。 如果请求成功，音频设备将路由到四个模拟输出直接连接的左、 右、 居中，且返回发言人的四个通道。

2.  如果该操作失败，DirectSound 要求驱动程序在立体声演讲者模式中配置设备并启用其[ **KSNODETYPE\_PROLOGIC\_编码器**](https://msdn.microsoft.com/library/windows/hardware/ff537187)节点，如果有的话。 如果成功，设备将应用程序中对它以数字或模拟形式输出的环绕声编码的立体声信号转换的 4 个通道流。 （硬件应执行混合的流的流组织到设备的各种 mixer pin 后的编码。）用户可以连接到外部解码器转换到的输出到四个频道编码的信号左、 右、 居中，，并返回发言人的设备的立体声输出。

3.  如果失败，DirectSound 使 KSNODETYPE\_PROLOGIC\_中 KMixer 编码器节点。 （设备已在上一步的立体声模式。）同样，由设备输出的立体声信号可以提供给外部解码器。

如果此算法成功，应用程序可以创建和播放 4 个通道 PCM 缓冲区。 在 1 和 2 更高版本的情况下，从设备读取的硬件缓冲区使用四个通道，但在 3 种情况下硬件缓冲区所使用的立体声格式。 应用程序可以直接写入中用例 1 和 2，硬件缓冲区，但在情况下不应写入到的软件的 3 缓冲并允许 KMixer 将应用程序的四个通道流转换为所需的硬件缓冲区环绕声编码的立体声格式。

在以上示例中 (3)，应用程序应避免使用其输出流的任何硬件缓冲区。 请注意 KMixer 混合编码组合以生成环绕立体声流前使用所有其输入的流。 但是，输入硬件 mixer pin 的任何流中使用编码的立体声硬件混合从 KMixer，会环绕声音频质量的降低时进行解码。 应用程序可以避免上述情况使用仅软件缓冲区。

已由 KSNODETYPE 环绕声编码的立体声流\_PROLOGIC\_编码器节点可以通过解码到四个渠道 （左侧，右、 居中，和备份） [ **KSNODETYPE\_PROLOGIC\_解码器**](https://msdn.microsoft.com/library/windows/hardware/ff537185)节点。

 

 





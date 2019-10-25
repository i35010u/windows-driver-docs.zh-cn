---
title: 从内核流式处理拓扑到音频混音器 API 的转换
description: 从内核流式处理拓扑到音频混音器 API 的转换
ms.assetid: ee89dc67-c9f3-41cd-8a09-0c46d636fe64
keywords:
- 混音器 API WDK 音频
- 内核流式处理 WDK 音频
- 音频混合器线条 WDK 音频
- 源混合器线条 WDK 音频
- 目标混音器线条 WDK 音频
- 将 KS 拓扑转换为混音器曲线 WDK 音频
- 混音器线条乐曲音频
- KS 流混合 WDK 音频
- KS 拓扑 WDK 音频
- 接收器引脚 WDK 音频
- 源引脚 WDK 音频
- KS 引脚音频，转换
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac47a44751cfe58dcc851fe2c76c3c8fabd91a47
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833168"
---
# <a name="kernel-streaming-topology-to-audio-mixer-api-translation"></a>从内核流式处理拓扑到音频混音器 API 的转换


## <span id="kernel_streaming_topology_to_audio_mixer_api_translation"></span><span id="KERNEL_STREAMING_TOPOLOGY_TO_AUDIO_MIXER_API_TRANSLATION"></span>


**混音**器 API 是一组 Windows 多媒体功能，用于检索有关音频混音器设备的信息。 **混音**器 API 将音频混合器行分类为源和目标线。 *源行*是音频卡中的输入（例如 CD、麦克风、线路输入和 wave）。 *目标行*是卡的输出（例如，扬声器、耳机、电话线和波输入）。 为了使源行有效，它应具有从源到目标的唯一路径。 单个源行可能映射到多个目标，但不能有多个路径可以将源行连接到目标行。 有关**混音**器 API 的详细信息，请参阅 Microsoft Windows SDK 文档。

音频适配器的 WDM 驱动程序公开一个 KS 筛选器拓扑，该拓扑表示通过硬件的数据路径和这些路径上可用的功能。 [WDMAud 系统驱动程序](user-mode-wdm-audio-components.md#wdmaud_system_driver)（在 Wdmaud 和 WDMAud 文件中）应解释 KS 筛选器拓扑，并生成通过**混音**器 API 公开的相应源和目标混音器行。 WDMAud 还处理**混音**器 API 调用，并将其转换为对适配器驱动程序管理的筛选器引脚和节点的等效属性调用。

[KMixer 系统驱动](kernel-mode-wdm-audio-components.md#kmixer_system_driver)程序（KMixer）和[SWMidi 系统驱动程序](kernel-mode-wdm-audio-components.md#swmidi_system_driver)（SWMidi）是内核音频堆栈的组成部分。 KMixer 为 PCM 音频流提供系统范围内的音频混合、位深度转换、采样率转换和通道到扬声器配置（supermix）转换。 SWMidi 提供 MIDI 流的高质量软件合成。 系统音频驱动程序 SysAudio （Sysaudio，请参阅[SysAudio 系统驱动程序](kernel-mode-wdm-audio-components.md#sysaudio_system_driver)）将 KMixer 和 SWMidi 的功能与安装的音频适配器驱动程序结合起来，以形成功能增强的[虚拟音频设备](virtual-audio-devices.md)。

WDMAud 管理音频堆栈的 KS 部分和旧（请参阅[Winmm.dll 系统组件](user-mode-wdm-audio-components.md#winmm_system_component)）部分之间的接口。 WDMAud 将 SysAudio 虚拟化筛选器上的 pin 转换为显示在应用程序（如 SndVol32）中的旧混音器行。 从 KS 拓扑转换到混音器行将按如下方式执行：

-   KS 拓扑中的源 pin （KSPIN\_数据流\_输出）作为目标混合器行（MIXERLINE\_COMPONENTTYPE\_DST\_*XXX*）公开。

-   KS 拓扑中的接收器插针（KSPIN\_数据流\_）公开为源混合器行（MIXERLINE\_COMPONENTTYPE\_SRC\_*XXX*）。

-   WDMAud 将引导 KS 筛选器图形，该图形位于位于筛选器图端点的源引脚上，并沿与数据流相反的方向遍历关系图，直到到达接收器 pin。

-   在遍历期间遇到的每个 KS 节点上支持的属性将公开为源混合器行中的控件。

在上述前两个项中，由于术语的不同，将 KS 源和接收器插针映射到目标和源混音器可能会造成混淆。 在 KS 中，设备包装在具有接收器（输入）插针和源（输出）插针的筛选器中。 术语 "sink" 和 "source" 指的是筛选器，而不是引用两个筛选器之间的（通常是缓冲的）连接：

-   上游筛选器的源 pin 是进入连接的数据流的源。

-   数据流通过下游筛选器的接收器 pin 来退出连接。

与此相反，混音器行术语是以设备为中心的：

-   源混合器行是进入设备的流的源。

-   目标混音器行是退出设备的流的目标。

此外，在将其分配给 KS 筛选器的 pin 的流流方向上，KS 术语有些不一致。 Pin 描述符使用[**KSPIN\_数据流**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ne-ks-kspin_dataflow)枚举值来指定方向：

-   通过接收器 pin 进入筛选器的流在中具有 KSPIN\_数据流\_的方向。

-   通过源 pin 退出筛选器的流具有 KSPIN\_数据流\_的方向。

"传入" 和 "输出" 方向以清晰的以筛选方式进行，而 "sink" 和 "源" 这两者以连接为中心。

有关 WDMAud 使用的拓扑分析算法的详细信息，请参阅[WDMAud 拓扑分析](wdmaud-topology-parsing.md)。

本部分还包括：

[拓扑引脚](topology-pins.md)

[拓扑节点](topology-nodes.md)

[托盘和 SndVol32](systray-and-sndvol32.md)

[公开筛选器拓扑](exposing-filter-topology.md)

 

 





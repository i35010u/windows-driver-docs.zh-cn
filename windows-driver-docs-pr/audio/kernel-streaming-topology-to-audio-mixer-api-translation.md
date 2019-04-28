---
title: 从内核流式处理拓扑到音频混音器 API 的转换
description: 从内核流式处理拓扑到音频混音器 API 的转换
ms.assetid: ee89dc67-c9f3-41cd-8a09-0c46d636fe64
keywords:
- mixer API WDK 音频
- 内核流 WDK 音频
- 音频混音器行 WDK 音频
- 源 mixer 行 WDK 音频
- 目标 mixer 行 WDK 音频
- 转换到 mixer 行 WDK 音频 KS 拓扑
- mixer 行 WDK 音频
- KS 流混合 WDK 音频
- KS 拓扑 WDK 音频
- 接收器 pin WDK 音频
- 源 pin WDK 音频
- KS 固定 WDK 音频，转换
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c8cec89573b194e34114757b5bc49cd80ac5602
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333360"
---
# <a name="kernel-streaming-topology-to-audio-mixer-api-translation"></a>从内核流式处理拓扑到音频混音器 API 的转换


## <span id="kernel_streaming_topology_to_audio_mixer_api_translation"></span><span id="KERNEL_STREAMING_TOPOLOGY_TO_AUDIO_MIXER_API_TRANSLATION"></span>


**Mixer** API 是一组 Windows 多媒体函数用于检索有关音频混音器设备的信息。 **Mixer** API 将分为两类音频混音器作为源和目标行的行。 *源行*是声卡 （例如，CD、 麦克风、 行中和 wave） 的输入。 *目标行*是从智能卡 （例如，扬声器、 耳机、 电话线路和批中的） 的输出。 对于源行有效，它应有的唯一路径从源到目标。 包含一个源行可能会映射到多个目标，但不能超过单个路径可以连接到目标行的源行。 有关详细信息**mixer** API，请参阅 Microsoft Windows SDK 文档。

音频的适配器的 WDM 驱动程序公开表示通过硬件和这些路径可用的函数使用的数据路径的 KS 筛选器拓扑。 [WDMAud 系统驱动程序](user-mode-wdm-audio-components.md#wdmaud_system_driver)（在 Wdmaud.sys 和 Wdmaud.drv 文件中） 应解释 KS 筛选器拓扑并生成相应的源和目标通过公开的混音器行**mixer**API。 此外可以处理 WDMAud **mixer** API 调用，并会将它们转换为等效的属性的调用上的筛选器插针和由适配器驱动程序管理的节点。

[KMixer 系统驱动程序](kernel-mode-wdm-audio-components.md#kmixer_system_driver)(Kmixer.sys) 和[SWMidi 系统驱动程序](kernel-mode-wdm-audio-components.md#swmidi_system_driver)(Swmidi.sys) 个内核音频堆栈的不可或缺组成部分。 KMixer 提供整个系统音频混合、 位深度转换、 采样率转换和 PCM 音频流的通道扬声器配置 (supermix) 转换。 SWMidi 提供高质量的软件合成的 MIDI 流。 系统音频驱动程序，SysAudio (Sysaudio.sys，请参见[SysAudio 系统驱动程序](kernel-mode-wdm-audio-components.md#sysaudio_system_driver))，将 KMixer 和 SWMidi 的功能和增强的功能上的窗体所安装的音频适配器驱动程序结合起来[虚拟音频设备](virtual-audio-devices.md)。

WDMAud 管理 KS 部分和旧之间的接口 (请参阅[WinMM 系统组件](user-mode-wdm-audio-components.md#winmm_system_component)) 音频堆栈的一部分。 WDMAud SysAudio 虚拟化筛选器上的针转换为 SndVol32 等应用程序中提供的旧混音器行。 从 KS 拓扑转换为 mixer 行执行，如下所示：

-   源插针 (KSPIN\_数据流\_出) 在 KS 拓扑公开为目标 mixer 行 (MIXERLINE\_COMPONENTTYPE\_DST\_*XXX*)。

-   接收器插针 (KSPIN\_数据流\_中) 在 KS 拓扑公开为源 mixer 行 (MIXERLINE\_COMPONENTTYPE\_SRC\_*XXX*)。

-   WDMAud 指导在源 pin 都是筛选器关系图的终结点并遍历中数据流的相反方向的关系图，直到达到接收器 pin KS 筛选器关系图开始。

-   在遍历过程中遇到每个 KS 节点支持的属性被称为源混音器行上的控件。

在前两个项上，KS 的映射到目标和源混音器行的源和接收器插针是可能会导致混淆由于术语中的差异。 在 KS，设备都包装在筛选器具有接收器 （输入） 插针和源 （输出） 的 pin。 术语"sink"和"源"，请参阅筛选器而不是而是与两个筛选器之间的 （通常为缓冲） 连接：

-   上游筛选器的源 pin 是数据流的进入该连接的源。

-   数据流将退出下游筛选器的接收器 pin 要用的连接。

与此相反，mixer 行术语是以设备为中心：

-   在源 mixer 行是流的输入设备的源。

-   目标 mixer 行是流的退出设备的目标。

此外，KS 术语是某种程度上它将分配给 pin KS 筛选器的流流方向不一致。 使用 pin 描述符[ **KSPIN\_数据流**](https://msdn.microsoft.com/library/windows/hardware/ff563532)枚举值指定的方向：

-   输入通过接收器 pin 的筛选器的流都有的 KSPIN 方向\_数据流\_in。

-   退出通过源 pin 的筛选器的流都有方向的 KSPIN\_数据流\_出。

"In"和"out"的说明是清楚地筛选器以为中心，，而"source"的条款"sink"是连接为中心。

有关分析 WDMAud 所用算法的拓扑的详细信息，请参阅[WDMAud 拓扑分析](wdmaud-topology-parsing.md)。

本部分还包括：

[拓扑 Pin](topology-pins.md)

[拓扑节点](topology-nodes.md)

[系统托盘和 SndVol32](systray-and-sndvol32.md)

[公开筛选拓扑](exposing-filter-topology.md)

 

 





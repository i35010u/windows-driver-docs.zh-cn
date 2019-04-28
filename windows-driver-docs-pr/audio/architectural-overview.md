---
title: 体系结构概述
description: 本主题提供在 Windows 8 中，以便为组合的硬件/软件音频引擎提供支持引入了音频体系结构的概述。
ms.assetid: B8D71C86-E2FF-48F1-8DC1-F232399F324D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37b455a1880e696212edbc50d8cf88eb2e3700ae
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331598"
---
# <a name="architectural-overview"></a>体系结构概述


本主题提供在 Windows 8 中，以便为组合的硬件/软件音频引擎提供支持引入了音频体系结构的概述。

## <a name="span-idthesoftwareaudioenginespanspan-idthesoftwareaudioenginespanspan-idthesoftwareaudioenginespanthe-software-audio-engine"></a><span id="The_software_audio_engine"></span><span id="the_software_audio_engine"></span><span id="THE_SOFTWARE_AUDIO_ENGINE"></span>软件音频引擎


Windows 7 和 Windows，某些早期版本中的音频引擎支持允许第三方开发人员能够插入软件解码器，编码器，并在处理管道中的特定点上的其他一般音频效果的软件音频引擎。

下图显示了 Windows 8 软件音频引擎。

![pcm 或其他编码的音频数据的流以通过应用程序层，通过 wasapi 就可以了层到引擎中之前将流发送到演讲者在其中应用本地和全局处理效果音频流的形式。](images/audio-engine1.png)

您可以看到在上图中，音频流到达软件音频引擎从 Windows 音频会话 API （wasapi 就可以了） 层，并可能通过 Media Foundation 等更高级别的 API。 软件音频引擎本地效果 (LFX)，如卷控件和静音的应用在每个流的基础上独立的流是混合型，然后通过任何可用的全局效果 (GFX) 并发送到演讲者之前。

## <a name="span-idthehardwareaudioenginespanspan-idthehardwareaudioenginespanspan-idthehardwareaudioenginespanthe-hardware-audio-engine"></a><span id="The_hardware_audio_engine"></span><span id="the_hardware_audio_engine"></span><span id="THE_HARDWARE_AUDIO_ENGINE"></span>硬件音频引擎


硬件音频引擎中的音频的适配器实现，并很大程度上反映软件音频引擎的功能。 和 Windows 8 支持硬件卸载音频处理，但给定的音频适配器的音频驱动程序是负责公开使用下图中所示的拓扑的音频硬件的基础功能。

![硬件 auido 引擎旨在接受有限数量的卸载的流加上主机流，它是软件音频引擎的输出。 硬件音频引擎提供了同时连接到扬声器其最终处理阶段中的反馈 （环回） 流。](images/audio-engine3.png)

在关系图中所示，硬件音频引擎必须接受单个主机进程流，并最多 n 卸载流。 这些卸载的流直接从应用程序层在硬件中要处理路由。 换而言之，卸载的流将不能传递通过软件音频引擎。 关系图显示了用于处理最多三个卸载的流实现。 主机进程流是中软件音频引擎处理的所有流软件 mixer 的最终输出。 每个硬件音频引擎还必须包含硬件 mixer。

为了维护奇偶校验带软件音频引擎和 wasapi 就可以了接口，它是必需的硬件音频引擎提供最终的音频输出流返回到环回流的窗体中的音频堆栈。 这是为应用程序和依赖声学回声抵消，需要了解要取消回显并防止反馈的最终输出流的方案尤其重要。

为了实现环回流的路径，音频驱动程序负责公开环回 pin。 如果对数据编码为 PCM 格式，此 pin 将从输出中，最终音频引擎返回的音频数据。 否则为将返回后混合使用 （但预编码） 的结果。 这意味着，对于处理硬件 GFX 为非 PCM 格式进行编码的音频数据，环回流点后硬件混音器，直接在硬件音频引擎 GFX 阶段之前。 在新的 KS 筛选器拓扑表示硬件音频引擎有关的信息，请参阅[实现概述](implementation-overview.md)。

## <a name="span-idtheoverallarchitecturespanspan-idtheoverallarchitecturespanspan-idtheoverallarchitecturespanthe-overall-architecture"></a><span id="The_overall_architecture"></span><span id="the_overall_architecture"></span><span id="THE_OVERALL_ARCHITECTURE"></span>整体体系结构


下图显示最终的体系结构的概述时硬件音频引擎协同工作与 Windows 8 软件音频引擎。

![集成的软件和硬件的音频引擎，显示从硬件引擎将发回 wasapi 就可以了层的环回流体系结构。](images/audio-engine2.png)

这意味着，在其中的音频驱动程序已指明其支持的方案中卸载音频处理，第一个 n (在这种情况下，三个) 初始化的流将直接从 wasapi 就可以了层路由到硬件音频引擎，从而绕过软件音频引擎。 将通过软件音频引擎进行处理路由之后 n 硬件音频引擎支持的任何新音频流。 从软件音频引擎生成的流然后作为主机进程流发送到硬件音频引擎。 主机进程流混合与第一个 n 流、 应用 GFX 处理，并生成流然后发送到演讲者。

**请注意**  之前的音量调节，一般情况下，会应用 GFX 处理。 但在其中 GFX 编码为非 PCM 格式; 的情况下出现异常在这种情况下 GFX/卷控件顺序已反转，以便进行 GFX 处理前音量控制可应用于未压缩的数据。 Windows 7 软件音频引擎遵循相同的模型。

 

 

 





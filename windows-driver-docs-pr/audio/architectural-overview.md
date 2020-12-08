---
title: 体系结构概述
description: 本主题概述了在 Windows 8 中引入的音频体系结构，以便为组合硬件/软件音频引擎提供支持。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 921f2a8b7e99575622193e6e71bf17f3ca4195ba
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789443"
---
# <a name="architectural-overview"></a>体系结构概述


本主题概述了在 Windows 8 中引入的音频体系结构，以便为组合硬件/软件音频引擎提供支持。

## <a name="span-idthe_software_audio_enginespanspan-idthe_software_audio_enginespanspan-idthe_software_audio_enginespanthe-software-audio-engine"></a><span id="The_software_audio_engine"></span><span id="the_software_audio_engine"></span><span id="THE_SOFTWARE_AUDIO_ENGINE"></span>软件音频引擎


Windows 7 和某些早期版本的 Windows 中的音频引擎支持软件音频引擎，该引擎允许第三方开发人员在处理管道中的特定点插入软件解码器、编码器和其他一般音频效果。

下图显示了 Windows 8 软件音频引擎。

![pcm 或其他编码的音频数据将通过应用程序层以流的形式流过，通过 wasapi 层进入音频引擎，其中在流发送到发言人之前应用本地和全局处理效果。](images/audio-engine1.png)

如前面的关系图中所示，音频流从 Windows 音频会话 API 到达软件音频引擎 (WASAPI) 层，并且可能通过更高级别的 API （如媒体基础）。 在软件音频引擎本地效果 (LFX) （如音量控制和静音）在单独的流混合之前应用于每个流，然后通过任何可用的全局效果 (GFX) 并发送到扬声器。

## <a name="span-idthe_hardware_audio_enginespanspan-idthe_hardware_audio_enginespanspan-idthe_hardware_audio_enginespanthe-hardware-audio-engine"></a><span id="The_hardware_audio_engine"></span><span id="the_hardware_audio_engine"></span><span id="THE_HARDWARE_AUDIO_ENGINE"></span>硬件音频引擎


硬件音频引擎在音频适配器中实现，并主要反映软件音频引擎的功能。 虽然 Windows 8 支持硬件卸载音频处理，但给定音频适配器的音频驱动程序负责使用下图中所示的拓扑公开音频硬件的基础功能。

![硬件 auido 引擎旨在接受有限数量的卸载流，以及作为软件音频引擎输出的主机流。 硬件音频引擎提供反馈 (环回) 流，该流来自也连接到扬声器的最终处理阶段。](images/audio-engine3.png)

如图所示，硬件音频引擎必须接受单主机进程流和最多 n 个卸载流。 这些卸载的流直接从要在硬件中处理的应用程序层进行路由。 换句话说，卸载的流将不会通过软件音频引擎传递。 此关系图显示了一个旨在处理多达三个卸载流的实现。 宿主进程流是软件音频引擎中处理的所有流的软件混合器的最终输出。 每个硬件音频引擎还必须包含硬件混合器。

为了保持与软件音频引擎和 WASAPI 接口的奇偶校验，硬件音频引擎需要将最终音频输出流以环回流的形式提供给音频堆栈。 这对于依赖于 "声音回声取消" 的应用程序和方案尤其重要，这需要了解最终输出流来取消回显并阻止反馈。

为了实现环回流的路径，音频驱动程序负责公开环回 pin。 如果数据编码为 PCM 格式，此 pin 将返回最终音频引擎输出的音频数据。 否则，将返回后混合 (但) 结果的预先编码。 这意味着，在使用编码为非 PCM 格式的硬件 GFX 处理的音频数据的情况下，环回流直接在硬件混合器之后获取，然后在硬件音频引擎中的 GFX 阶段之前进行。 有关表示硬件音频引擎的新 KS 筛选器拓扑的信息，请参阅 [实现概述](implementation-overview.md)。

## <a name="span-idthe_overall_architecturespanspan-idthe_overall_architecturespanspan-idthe_overall_architecturespanthe-overall-architecture"></a><span id="The_overall_architecture"></span><span id="the_overall_architecture"></span><span id="THE_OVERALL_ARCHITECTURE"></span>整体体系结构


下图显示了当硬件音频引擎与 Windows 8 软件音频引擎协同工作时所得到的体系结构的概述。

![软件和硬件音频引擎的集成体系结构，显示从硬件引擎返回到 wasapi 层的环回流。](images/audio-engine2.png)

这意味着，在音频驱动程序已指示其对卸载音频处理的支持的情况下，在这种情况下，前 n 个 (会将初始化的三个) 流直接从 WASAPI 层路由到硬件音频引擎，绕过软件音频引擎。 硬件音频引擎支持的 n 之后的任何新音频流都将通过软件音频引擎进行处理，以便进行处理。 然后，将从软件音频引擎生成的流发送到硬件音频引擎，作为主机进程流。 主机进程流与前 n 个流混合，应用 GFX 处理，然后将生成的流发送到扬声器。

**注意**  通常情况下，GFX 处理在进行音量调整前应用。 但在将 GFX 编码为非 PCM 格式的情况下，会出现异常;在这种情况下，将反转 GFX/volume 控制顺序，以便在处理 GFX 之前可以将音量控制应用于未压缩的数据。 Windows 7 软件音频引擎遵循相同的模型。

 

 

 





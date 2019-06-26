---
title: 合成器计时
description: 合成器计时
ms.assetid: 38aca8b7-f895-4b16-aaac-5a13973cf976
keywords:
- 合成器 WDK 音频，计时
- 时间 WDK 音频
- 引用时钟 WDK 音频
- 示例时钟 WDK 音频
- 时钟 WDK 音频，合成器
- 用户模式下 synths WDK 音频，合成器计时
- 自定义 synths WDK 音频，合成器计时
- DirectMusic 自定义呈现 WDK 音频，合成器计时
- 自定义呈现在用户模式 WDK 音频，合成器计时
- DirectMusic WDK 音频，合成器
- 计时器 WDK 音频
- 时钟 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c24bbbe6e8a43b49b8126e6cfe87b34db548f3a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354210"
---
# <a name="synthesizer-timing"></a>合成器计时


## <span id="synthesizer_timing"></span><span id="SYNTHESIZER_TIMING"></span>


合成器适用于两个不同系统的时间：

-   引用时间

-   采样时间

引用时间是一系列消息将会播放的绝对时间 （以 master 时钟为单位）。 在用户模式下实现中，它传递给[ **IDirectMusicSynth::PlayBuffer** ](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-playbuffer) MIDI 消息送入合成器的方法。 合成器、 批接收器和 DirectMusic 的其余部分应由您的实现的附加到合成器的相同主时钟下的所有工作[ **IDirectMusicSynth::SetMasterClock** ](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-setmasterclock)方法再到通过波形接收器[ **IDirectMusicSynthSink::SetMasterClock**](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynthsink-setmasterclock)。

采样时间用于度量到合成器的输出缓冲区的偏移量。 此缓冲区填充波样本的因此示例时间是相对于采样率。 例如，在为 22.1 kHz 采样率，每秒是时间的等效 22,100 示例或 44,200 字节 （对于 16 位的 mono 格式）。

播放 wave 示例缓冲区很可能由不同的计时 crystal 比主时钟控制，因为引用时和示例时倾向于偏离。 通过实现阶段锁定循环中，批接收器保留它们在步骤中。 此时钟同步中所述[时钟同步](clock-synchronization.md)。

本部分还包括：

[合成器延迟](synthesizer-latency.md)

[带有时间戳的事件](time-stamped-events.md)

 

 





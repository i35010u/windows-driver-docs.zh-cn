---
title: 合成器计时
description: 合成器计时
keywords:
- 合成 WDK 音频，计时
- 时间 WDK 音频
- 引用时钟 WDK 音频
- 示例时钟 WDK 音频
- 时钟 WDK 音频，合成合成
- 用户模式 synths WDK 音频，合成器计时
- 自定义 synths WDK 音频，合成器计时
- DirectMusic 自定义渲染 WDK 音频，合成器计时
- 用户模式下的自定义呈现 WDK 音频，合成器计时
- DirectMusic WDK 音频，合成
- 计时器音频
- 时钟 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a7ec61778b89a87a6c4cafd64cbb19886d4bd25c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800543"
---
# <a name="synthesizer-timing"></a>合成器计时


## <span id="synthesizer_timing"></span><span id="SYNTHESIZER_TIMING"></span>


合成器适用于两个不同的时间系统：

-   引用时间

-   采样时间

引用时间是在主时钟单位)  (要播放消息序列的绝对时间。 在用户模式实现中，当 MIDI 消息送入合成器时，它将传递给 [**IDirectMusicSynth：:P laybuffer**](/windows/win32/api/dmusics/nf-dmusics-idirectmusicsynth-playbuffer) 方法。 合成器、波形接收器和 DirectMusic 的其余部分都应在相同的主时钟下运行，这是通过 [**IDirectMusicSynth：： SetMasterClock**](/windows/win32/api/dmusics/nf-dmusics-idirectmusicsynth-setmasterclock) 方法的实现和通过 [**IDirectMusicSynthSink：： SetMasterClock**](/windows/win32/api/dmusics/nf-dmusics-idirectmusicsynthsink-setmasterclock)实现的波形接收器附加到合成器的。

采样时间用于测量合成器的输出缓冲区中的偏移量。 此缓冲区填充了波形样本，因此采样时间与采样速率相关。 例如，如果采样速率为 22.1 kHz，则每秒的时间都等效于22100样本或44200字节 (16 位 mono 格式) 。

由于波形样本缓冲区的播放可能由与主时钟不同的 crystal 来控制，因此，引用时间和采样时间往往会发生偏差。 波形接收器通过实现阶段锁定的循环来保持它们的顺序。 [时钟](clock-synchronization.md)同步中介绍了此时钟同步。

本部分还包括：

[合成器延迟](synthesizer-latency.md)

[带时间戳的事件](time-stamped-events.md)

 


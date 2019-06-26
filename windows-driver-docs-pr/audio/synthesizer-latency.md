---
title: 合成器延迟
description: 合成器延迟
ms.assetid: a3134024-77b9-463b-959b-3c910f83014d
keywords:
- 合成器 WDK 音频，延迟
- 延迟 WDK 音频，合成器
- MIDI 消息延迟 WDK 音频
- IReferenceClock 对象
- 批接收器 WDK 音频，延迟时间
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1aa780999439aa5d463871fadd30ed735302ad80
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354220"
---
# <a name="synthesizer-latency"></a>合成器延迟


## <span id="synthesizer_latency"></span><span id="SYNTHESIZER_LATENCY"></span>


合成器计时的另一个注意事项是延迟，这是当前时间和下可以播放的第一个时间之间的差异。 MIDI 消息不能提交给合成器，并可以在当前的示例时呈现到输出缓冲区。 应给已放入了缓冲区，但不是尚未流式传输到 wave 输出设备的数据限额。

批接收器因此应实现延迟时钟，即[ **IReferenceClock** ](https://docs.microsoft.com/windows/desktop/wmformat/ireferenceclock) （Microsoft Windows SDK 文档中所述） 的对象。 延迟时钟[ **IReferenceClock::GetTime** ](https://docs.microsoft.com/en-us/previous-versions//dd551385(v=vs.85))方法检索到该数据已写入到缓冲区，并将其转换来引用相对于主时钟时间的示例时间. 批接收器 does 参考和示例使用的时间之间的转换[ **IDirectMusicSynthSink::SampleToRefTime** ](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynthsink-sampletoreftime)并[ **IDirectMusicSynthSink::RefTimeToSample** ](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynthsink-reftimetosample)，因此在这种情况下，调用合成**IDirectMusicSynthSink::RefTimeToSample**来完成转换。

所有管理批接收器滞后时间。 实现[ **IDirectMusicSynthSink::GetLatencyClock** ](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynthsink-getlatencyclock)方法应输出到延迟时钟指针和 this 指针又必须检索由[ **IDirectMusicSynth::GetLatencyClock**](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-getlatencyclock)。 应用程序使用延迟时钟来确定在其中可以排队 MIDI 消息时调用传递给合成器播放的时间最早的点[ **IDirectMusicSynth::PlayBuffer** ](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-playbuffer)方法。

MIDI 消息的延迟的示例是在下图中所示。

![说明的 midi 消息延迟时间的关系图](images/dmclock.png)

在上图中，延迟时钟指向可在其中播放下 PCM 缓冲区循环的第一个位置。 请注意，主时钟在 22 时间单位，即其中，从当前播放的声音但 22 和 30 时间单位之间的空间已使用批数据填充，并且不再可以写入到的点。 因此，可以计划新的时间戳 MIDI 事件播放的第一个位置是 30 次。 因此，延迟时钟读取 30 个时间单位。

消息可以这种延迟时间计划到 play 或后，任何时间。 因此，若要立即呈现的消息都标有放入合成器的输入缓冲区中之前的延迟时间 （而不是当前时间）。

 

 





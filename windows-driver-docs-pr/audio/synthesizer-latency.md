---
title: 合成器延迟
description: 合成器延迟
keywords:
- 合成 WDK 音频，延迟
- 延迟 WDK 音频，合成
- MIDI 消息延迟 WDK 音频
- IReferenceClock 对象
- 波形接收器音频，延迟时间
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a51e256674efd262e6be520904be8a9ec989144
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800557"
---
# <a name="synthesizer-latency"></a>合成器延迟


## <span id="synthesizer_latency"></span><span id="SYNTHESIZER_LATENCY"></span>


合成器计时中的另一个注意事项是延迟，这是当前时间与便笺首次可以播放的时间之间的差异。 在当前采样时间，无法将 MIDI 消息提交到合成器并呈现到输出缓冲区。 应为已放入缓冲区中但尚未流式传输到波形输出设备的数据进行限制。

因此，波形接收器应该实现延迟时钟，这是 (Microsoft Windows SDK 文档) 中所述的 [**IReferenceClock**](/windows/desktop/wmformat/ireferenceclock) 对象。 延迟时钟的 [**IReferenceClock：： GetTime**](/previous-versions//dd551385(v=vs.85)) 方法检索数据已写入缓冲区的采样时间，并将其转换为相对于主时钟的引用时间。 波形接收器在引用和采样时间之间进行转换， [**IDirectMusicSynthSink：： SampleToRefTime**](/windows/win32/api/dmusics/nf-dmusics-idirectmusicsynthsink-sampletoreftime) 和 [**IDirectMusicSynthSink：： RefTimeToSample**](/windows/win32/api/dmusics/nf-dmusics-idirectmusicsynthsink-reftimetosample)，因此在这种情况下，合成将调用 **IDirectMusicSynthSink：： RefTimeToSample** 来完成转换。

滞后时间由波形接收器管理。 你的 [**IDirectMusicSynthSink：： GetLatencyClock**](/windows/win32/api/dmusics/nf-dmusics-idirectmusicsynthsink-getlatencyclock) 方法的实现应输出指向延迟时钟的指针，并且此指针必须依次通过 [**IDirectMusicSynth：： GetLatencyClock**](/windows/win32/api/dmusics/nf-dmusics-idirectmusicsynth-getlatencyclock)检索。 应用程序通过调用 [**IDirectMusicSynth：:P laybuffer**](/windows/win32/api/dmusics/nf-dmusics-idirectmusicsynth-playbuffer) 方法，使用延迟时间来确定 MIDI 消息在传递到合成器时可以排队等待的最早时间点。

下图显示了 MIDI 消息延迟的示例。

![说明 midi 消息延迟的示意图](images/dmclock.png)

在上图中，延迟时钟指向 PCM 缓冲区循环中的第一个位置，可以在其中播放注释。 请注意，主时钟的时间单位为22个，这是声音当前播放的点，但22到30个时间单位之间的空间已用波形数据填充，无法再写入。 因此，可以计划在第30次播放带有时间戳的新 MIDI 事件的第一个位置。 因此，延迟时钟会读取30个时间单位。

可以计划在此延迟时间内或之后的任何时间播放消息。 因此，要立即呈现的消息将被标记为延迟时间 (当前时间) 置于合成器的输入缓冲区中。

 


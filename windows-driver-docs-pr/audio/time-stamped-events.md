---
title: 带时间戳的事件
description: 带时间戳的事件
ms.assetid: 8db89e31-bfd7-48cf-9eb2-12ac7784cc31
keywords:
- 合成器 WDK 音频，时间戳
- 时间戳 WDK 音频
- 带有时间戳事件 WDK 音频
- 事件 WDK 音频
- PCM 缓冲区 WDK 音频
- 延迟 WDK 音频、 时钟
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0230c56142540ec0e9f9017632afb10e61f8345e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354202"
---
# <a name="time-stamped-events"></a>带时间戳的事件


## <span id="time_stamped_events"></span><span id="TIME_STAMPED_EVENTS"></span>


合成器计时重要特性是而不是需要播放的确切时间发送下，每个注意是时间戳和放置于缓冲区。 然后处理和两个指定的时间戳的时间 （毫秒） 内播放此缓冲区。 （尽管计时解决方法是在数百个纳秒为单位，但我们将介绍根据毫秒，这将会更方便的时间单位，本次讨论中。）

由于延迟到系统通过延迟时钟，加盖时间戳事件可用于其适当的时间，在播放的缓冲区中等待而不是只是事件放入队列，且希望的延迟较低。

主时钟实现 COM [ **IReferenceClock** ](https://docs.microsoft.com/windows/desktop/wmformat/ireferenceclock)接口 （Microsoft Windows SDK 文档中所述）。 此引用时使用的所有设备在系统上。

Microsoft 的批接收器实现生成唤醒每隔 20 毫秒一个线程。 线程的任务是创建另一个缓冲区，并将其传送到 DirectSound。 若要创建该缓冲区，它调用合成器，并要求它来呈现指定的数量的音乐数据。 它要求输入量决定实际线程唤醒时，这不太可能完全 20 毫秒。

什么实际传递到合成器是只需指向开始写入数据到 PCM 缓冲区和一个长度参数，指定要写入数据量的内存中的位置。 合成器然后可以将 PCM 数据写入到此缓冲区并填充它最多指定的量。 也就是说，它将呈现从起始地址直到达到指定的长度。 内存块可以 DirectSoundBuffer （这是默认情况下），但也可能是 DirectShow 图形或其他由批接收器定义目标。

PCM 缓冲区是从概念上讲循环 （即，不断循环它）。 合成器呈现的缓冲区的后续片段描述声音的 16 位数字。 切片大小略有不同每次都会将唤醒线程，因为接收器无法唤醒完全每隔 20 毫秒。 因此每次唤醒线程 does，它充当 catch 来确定多久它应正在通过缓冲区之前重新进入睡眠状态。

从应用程序的角度来看，合成器端口驱动程序本身具有[ **IDirectMusicSynth::GetLatencyClock** ](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-getlatencyclock)从批接收器获取时钟的函数。 因此，有两个时钟：

-   任何人，包括批接收器侦听主时钟。

-   批接收器，用作 DirectMusic 端口提供延迟时钟可以看到的应用程序实现延迟时钟。

换而言之，应用程序要求提供延迟时钟，但将其视为即将从 DirectMusic 端口抽象而不是批接收器的时钟。

返回此延迟时钟的时间是缓冲区可呈现给，最早时间，因为合成器具有已呈现到缓冲区中该点为止。 如果合成器必须呈现在其最后一个写入的较小的缓冲区，延迟也是较小。

因此，批接收器调用[ **IDirectMusicSynth::Render** ](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-render)上合成器，显示缓冲区和请求，它使用填充呈现数据。 下图中所示，合成器采用加盖时间戳的所有事件为进入[ **IDirectMusicSynth::PlayBuffer** ](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-playbuffer)函数调用。

![说明的时间戳的消息队列的关系图](images/dmevents.png)

每个输入的缓冲区包含时间戳的消息。 每个这些消息放入队列以在指定时间戳的时间呈现到缓冲区。

有关此模型的重要事情之一是，没有任何特定顺序以外的时间戳。 这些事件中，流式传输，因此可以将它们添加到队列在呈现之前的任何时间。 所有内容都是基于事件的时间。 例如，如果当前为 400 个时间单位的参考时间，然后所有内容带时间戳 400 次发生这种情况发生的情况现在。 事件时间戳，从现在起的 10 个单位发生这种情况在 410 时将发生。

 

 





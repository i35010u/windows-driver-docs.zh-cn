---
title: 带时间戳的事件
description: 带时间戳的事件
ms.assetid: 8db89e31-bfd7-48cf-9eb2-12ac7784cc31
keywords:
- 合成 WDK 音频，时间戳
- 时间戳 WDK 音频
- 带有时间戳的事件 WDK 音频
- 事件 WDK 音频
- PCM 缓冲 WDK 音频
- 延迟 WDK 音频，时钟
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ed72f15f1c72d32d3d6e0134d18973fcd35c8d2
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716066"
---
# <a name="time-stamped-events"></a>带时间戳的事件


## <span id="time_stamped_events"></span><span id="TIME_STAMPED_EVENTS"></span>


合成器计时的大图是，无需在需要播放时准确地发送注释，每个注释都将进行时间戳并放置在一个缓冲区中。 然后，在时间戳指定的两毫秒内处理并播放此缓冲区。  (尽管计时解决方法分为数百毫微秒，但我们将以毫秒为单位进行讨论，这是此讨论的更方便的时间单位。 ) 

由于在延迟时间内系统会对系统造成延迟，因此，带时间戳的事件可能会在缓冲区中等待等待正确的时间，而不是仅仅将事件放入队列中，希望延迟较低。

主时钟实现 (COM [**IReferenceClock**](/windows/desktop/wmformat/ireferenceclock) 接口，) Microsoft Windows SDK 文档中所述。 系统上的所有设备都使用此引用时间。

Microsoft 的 wave 接收器实现生成一个线程，该线程每隔20毫秒唤醒一次。 线程的作业是创建另一个缓冲区，并将其交给 DirectSound。 若要创建该缓冲区，它会调入合成器并要求其呈现指定数量的音乐数据。 它要求的量取决于线程唤醒的实际时间，这不太可能正好为20毫秒。

实际传入合成器的方法只是一个指针，指向在内存中开始将数据写入到 PCM 缓冲区的位置，并指定一个长度参数，用于指定要写入的数据量。 然后，合成器可以将 PCM 数据写入此缓冲区，并将其填充到指定的量。 也就是说，它会从起始地址呈现，直到到达指定长度。 这种内存块可以是 DirectSoundBuffer (这是默认情况下) 的默认情况，但也可以是一个 DirectShow 图形，也可以是由波形接收器定义的某个其他目标。

PCM 缓冲区在概念上是循环的 (也就是说，它会不断地循环) 。 合成器呈现16位数字，将声音描述为缓冲区的后续切片。 每次线程 awakens 时，切片大小都略有不同，因为接收器每隔20毫秒就无法唤醒。 因此，每次线程唤醒时，它会一直运行，以确定它在返回到休眠状态之前应该在整个缓冲区中的进度。

从应用程序的角度来看，合成端口驱动程序本身具有一个 [**IDirectMusicSynth：： GetLatencyClock**](/windows/win32/api/dmusics/nf-dmusics-idirectmusicsynth-getlatencyclock) 函数，该函数可从波形接收器获取时钟。 因此有两个时钟：

-   每个人（包括波形接收器）侦听的主时钟。

-   由波形接收器实现的延迟时钟，应用程序将其视为提供延迟时钟的 DirectMusic 端口。

换句话说，应用程序会要求延迟时钟，但会将时钟视为来自 DirectMusic 端口抽象，而不是来自波形接收器。

此延迟时钟返回的时间是缓冲区可呈现到的最早时间，因为合成器已在缓冲区中的该位置上呈现。 如果合成器在其上次写入时呈现了较小的缓冲区，则延迟也会更小。

因此，波形接收器对合成器调用 [**IDirectMusicSynth：： Render**](/windows/win32/api/dmusics/nf-dmusics-idirectmusicsynth-render) ，并显示缓冲区并请求用呈现的数据进行填充。 如下图所示，合成 [**IDirectMusicSynth：:P laybuffer**](/windows/win32/api/dmusics/nf-dmusics-idirectmusicsynth-playbuffer) 函数调用导致的所有带时间戳的事件。

![阐释带有时间戳的消息的队列的关系图](images/dmevents.png)

每个输入缓冲区包含带有时间戳的消息。 其中每个消息都放入队列中，以便在其时间戳指定的时间呈现到缓冲区中。

此模型的一个重要问题是，时间戳以外没有特定顺序。 这些事件是在中进行流式处理的，因此可以在呈现前随时将它们添加到队列中。 一切都是基于事件的，与时间有关。 例如，如果引用时间当前为400时间单位，则时间戳的所有时间都将在时间400发生。 事件时间戳现在会出现10个单位，此时将在410。

 


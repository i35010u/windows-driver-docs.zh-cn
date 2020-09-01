---
title: MIDI 到 Wave
description: MIDI 到 Wave
ms.assetid: 0c69ce48-ded0-44b8-9d34-20decb75058e
keywords:
- 合成 WDK 音频，MIDI 到 wave 转换
- MIDI 到 wave 转换 WDK 音频
- 波形流 WDK 音频
- 自定义 synths WDK 音频，MIDI 到 wave 转换
- 用户模式 synths WDK 音频，MIDI 到 wave 转换
- 将 MIDI 转换为波形
- DirectMusic WDK 音频，MIDI 到 wave 转换
- 用户模式下的自定义呈现 WDK 音频，MIDI 到 wave 转换
- DirectMusic 自定义呈现 WDK 音频，MIDI 到 wave 转换
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e02e62d4ef41e69e59ecd4b8e272ab4185d75f7f
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211381"
---
# <a name="midi-to-wave"></a>MIDI 到 Wave


## <span id="midi_to_wave"></span><span id="MIDI_TO_WAVE"></span>


合成器的主要工作分为两个步骤：

-   获取 MIDI 消息

-   将渲染的注释混合到波形音频流

本节详细介绍了如何在用户模式下完成此操作，尽管概念在内核模式中本质上是相同的。 有关如何使用内核模式微型端口驱动程序执行相同操作的详细信息，请参阅 [内核模式硬件加速 DDI](kernel-mode-hardware-acceleration-ddi.md) 。

在用户模式下，应用程序会在具有可供播放的 MIDI 消息时调用 [**IDirectMusicSynth：:P laybuffer**](/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-playbuffer) 。 应用程序负责及时调用 **PlayBuffer** ，并正确地记下缓冲区的时间，从而考虑到 [合成器滞后](synthesizer-latency.md) 时间。 此方法的实现会检索正在等待的消息，并将其存储为内部格式，该格式使用基于与缓冲区传入的引用时间的时间进行标记。

每当波形接收器准备好接收数据时，就会调用 [**IDirectMusicSynth：： Render**](/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-render) 。 例如，如果呈现的数据的目标是 DirectSound 的辅助缓冲区，则 [**IDirectMusicSynthSink：： Activate**](/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynthsink-activate) 的实现可能会设置一个线程，该线程将等待 DirectSound **PlayBuffer** 通知。 当 DirectSound 缓冲区需要数据时，DirectSound 会通知线程，该线程又调用了 **Render**，并传入指向 **IDirectSoundBuffer** 对象的指针 (在 Microsoft Windows SDK 文档) 以及要呈现的样本的数量和位置。

DirectSound 缓冲区是循环的。 由于环绕发生在缓冲区的末尾，因此必须将几乎连续区域拆分为两个部分。 通常，波形接收器通过两次调用 **Render** 来处理拆分，一次针对 DirectSound 缓冲区的锁定部分的每个部分，因此 **Render** 方法只需要处理连续的内存块。 波形接收器调用 DirectSound 缓冲区上的 **IDirectSoundBuffer：： Lock** 来请求对缓冲区内某个区域的写入权限。 例如，如果波形接收器在从缓冲区末尾开始 1 kb 的 2 kb 的数据上调用 **锁** ，则调用会将最后 1 kb 锁定到缓冲区的末尾，并从缓冲区的开头开始另一个 1 kb。 在这种情况下， **Lock** 实际上返回两个指针和相应的长度，它们共同描述锁定的缓冲区区域。 每个指针都一定指向连续的内存块。

**Render**方法的实现负责确定必须执行哪些操作才能响应**PlayBuffer**中检索到的 MIDI 消息。 从连续调用到**Render**的*dwLength*参数值，方法可以跟踪采样时间，并对当前呈现期间内有效的消息执行操作。 处理注释消息时，可以在内部存储注释并在每次通过方法时再次呈现注释，直到收到相应的附注消息。

 


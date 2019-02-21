---
title: 批的 MIDI
description: 批的 MIDI
ms.assetid: 0c69ce48-ded0-44b8-9d34-20decb75058e
keywords:
- 合成器 WDK 音频、 MIDI 批转换
- MIDI 批转换 WDK 音频
- 批流 WDK 音频
- 自定义 synths WDK 音频、 MIDI 批转换
- 用户模式下 synths WDK 音频、 MIDI 批转换
- 转换为批的 MIDI
- DirectMusic WDK 音频、 MIDI 批转换
- 在用户模式 WDK 音频、 MIDI 批转换的自定义呈现
- DirectMusic 自定义呈现 WDK 音频、 MIDI 批转换
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de3e1f827fb4d8354e7cdb735c937f01b7b4b496
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555576"
---
# <a name="midi-to-wave"></a>批的 MIDI


## <span id="midi_to_wave"></span><span id="MIDI_TO_WAVE"></span>


合成器的主要工作分为两个步骤：

-   获取 MIDI 消息

-   混合到波形音频流的呈现的说明

本部分详述了通常如何做到这一点在用户模式下，尽管概念实质上是在内核模式中相同。 请参阅[内核模式下的硬件加速 DDI](kernel-mode-hardware-acceleration-ddi.md)有关如何执行同样的内核模式微型端口驱动程序的详细信息。

在用户模式下，应用程序调用[ **IDirectMusicSynth::PlayBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff536540)时它已准备好播放 MIDI 消息。 应用程序负责调用**PlayBuffer**及时和时间戳缓冲区正确，采用[合成器延迟](synthesizer-latency.md)到帐户。 此方法的实现检索等待消息，并将其存储在基于引用时间随缓冲区传递一个时间戳的内部格式。

批接收器调用[ **IDirectMusicSynth::Render** ](https://msdn.microsoft.com/library/windows/hardware/ff536541)每当它已准备好接收数据。 例如，如果对已呈现数据的目标是 DirectSound 辅助缓冲区的实现[ **IDirectMusicSynthSink::Activate** ](https://msdn.microsoft.com/library/windows/hardware/ff536521)可能设置了线程等待 DirectSound**PlayBuffer**通知。 DirectSound DirectSound 缓冲区需要的数据，当通知线程，这又会调用**呈现**，并传入一个指向**IDirectSoundBuffer** （Microsoft Windows SDK 中所述的对象文档） 和的数量和位置的示例的呈现。

DirectSound 缓冲区为圆形。 由于自动换行发生在缓冲区的末尾，可能会拆分成两部分的几乎相连区域必须考虑在内。 批接收器通常会通过调用处理拆分**呈现**两次，一次的每一部分 DirectSound 的锁定部分缓冲，以便**呈现**方法仅有要处理的连续块内存。 批接收器调用**IDirectSoundBuffer::Lock**对 DirectSound 缓冲区寻求缓冲区内的区域的写入权限。 例如，如果批接收器调用**锁**然后开始从缓冲区末尾的 1 千字节的数据的 2 千字节，在调用锁定缓冲区和缓冲区的开头处开始的另一个 1 千字节结束之前，最后一个 1 千字节。 在这种情况下，**锁**实际返回的两个指针和对应的长度，一起描述缓冲区已锁定的区域。 保证每个指针指向内存的连续块。

实现**呈现**方法负责确定在响应中检索的 MIDI 消息中必须做什么**PlayBuffer**。 从*dwLength*参数值的连续调用**呈现**，该方法可以跟踪的采样时间和当前的呈现时间是有效的邮件执行操作。 注意在消息处理时，可以在内部存储并再次呈现在每次传递通过方法直到收到相应 note off 消息说明。

 

 





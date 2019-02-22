---
title: MIDI 传输
description: MIDI 传输
ms.assetid: ce9ec589-0aea-4ed9-a60d-50f2ddfb0c13
keywords:
- 端口驱动程序 WDK 音频，合成器
- 微型端口驱动程序 WDK 音频，合成器
- MIDI 传输 WDK 音频
- 批接收器 WDK 音频，MIDI 传输
- 合成器 WDK 音频，MIDI 传输
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9b9dfaed609b57ed9070c597bab95108505b433
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543985"
---
# <a name="midi-transport"></a>MIDI 传输


## <span id="midi_transport"></span><span id="MIDI_TRANSPORT"></span>


Dmu 端口驱动程序涉及到前端和后端两侧 Dmu 微型端口驱动程序的合成器工作上。 端口驱动程序输入一个 MIDI 流，其中包含的时间戳 MIDI 数据并将流路由到排序器。 排序器中删除的时间戳，并将原始的 MIDI 消息传递给微型端口驱动程序，其时间戳到期时。 （DLS 数据通过右端口驱动程序微型端口驱动程序和任何预处理到。）

时 Dmu 微型端口驱动程序 MIDI 输入的流将转换为波形数据，其输出管理批接收器 （也称为"合成器 sink"呈现接收器"）。

Dmu 端口驱动程序实现一个接受来自 DirectMusic 用户模式组件，DirectMusic 数据的输入插针的筛选器内核流式处理 dmusic.dll。 端口驱动程序还具有批输出插针，发出合成的音频流。 批接收器管理此 pin，并在内存中要写入其数据指示合成器。 这种排列方式隔离内核流式处理的详细信息中合成器。 Dmu 微型端口驱动程序只需处理的上佳输入 MIDI 流中的波形数据的详细信息。 端口驱动程序将批数据发送到系统中，并 SysAudio 的筛选器图形连接筛选器以使所有内容正确流。 下图中所示，MIDI 数据到 Dmu 端口驱动程序，并将序列化之后，将传递到 Dmu 微型端口驱动程序。

![说明的 midi 和 dls portdmus 驱动程序通过数据流关系图](images/dmportmi.png)

微型端口驱动程序将 MIDI 数据转换为声波格式，通过端口驱动程序的另一个部分呈现到指定的缓冲区： 批接收器。 然后，而不是发送到 DirectSound 方式与其在用户模式下的 wave 输出转到通过的音频硬件[KMixer 系统驱动程序](kernel-mode-wdm-audio-components.md#kmixer_system_driver)。 DirectSound 是实际上只是公开 KMixer，API，DirectSound 加速包含正在中而不是模拟中的软件的硬件加速的 KMixer 混音器函数。

[SysAudio 系统驱动程序](kernel-mode-wdm-audio-components.md#sysaudio_system_driver)，哪些生成音频筛选器关系图中，连接到硬件 Dmu 端口驱动程序。 端口驱动程序的批接收器部分分发数据通过 SysAudio 可以连接到硬件设备及其批带 pin 码。 它从 Dmu 微型端口驱动程序 （而不考虑是硬件或软件合成器），提取批数据和处理所有的计时问题。 与用户模式相比，微型端口驱动程序是类似于合成器，而只是批接收器端口驱动程序的一部分。

如果 Dmu 微型端口驱动程序可以提供其输出返回到主机，它公开 KSPIN 数据方向的批 pin\_数据流\_OUT (请参阅[ **KSPIN**](https://msdn.microsoft.com/library/windows/hardware/ff563483))，哪些 SysAudio识别并连接到 KMixer。

有关批接收器的详细信息，请参阅[内核模式软件合成器的批接收器](a-wave-sink-for-kernel-mode-software-synthesizers.md)。

本部分还包括：

[IMXF 接口](imxf-interfaces.md)

[Allocator](allocator.md)

 

 





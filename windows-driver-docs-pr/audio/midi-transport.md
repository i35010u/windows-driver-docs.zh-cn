---
title: MIDI 传输
description: MIDI 传输
keywords:
- 端口驱动程序 WDK 音频，合成程序
- 微型端口驱动程序 WDK 音频，合成程序
- MIDI 传输 WDK 音频
- 波形接收器音频，MIDI 传输
- 合成 WDK 音频，MIDI 传输
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cfbd5e90a7d11f488e7d870f86d1c28cb6f4fcab
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801011"
---
# <a name="midi-transport"></a>MIDI 传输


## <span id="midi_transport"></span><span id="MIDI_TRANSPORT"></span>


Dmu 端口驱动程序涉及 Dmu 微型端口驱动程序的合成器工作的正面和背面。 端口驱动程序会输入一个 MIDI 流，其中包含带时间戳的 MIDI 数据，并将该流路由到 sequencer。 Sequencer 将删除时间戳，并将原始 MIDI 消息传递给微型端口驱动程序（如果它们的时间戳到期）。  (DLS 数据通过端口驱动程序直接传递到无预处理的微型端口驱动程序。 ) 

当 Dmu 微型端口驱动程序的 MIDI 输入流转换为波形数据时，其输出由波形接收器管理 (也称为 "合成接收器" 或 "render sink" ) 。

Dmu 端口驱动程序使用输入插针实现内核流筛选器，该输入插针接受 DirectMusic 用户模式组件（dmusic.dll）中的 DirectMusic 数据。 端口驱动程序还具有发出合成音频流的波形输出插针。 波形接收器管理此 pin，并告诉合成要在内存中写入数据的位置。 此安排将合成从内核流式处理的详细信息中隔离开来。 Dmu 微型端口驱动程序只需处理来自输入 MIDI 流的综合 wave 数据的详细信息。 端口驱动程序将 wave 数据发送到系统，SysAudio 的筛选器图连接筛选器以使所有内容正确流动。 如下图所示，MIDI 数据进入 Dmu 端口驱动程序，并在序列化后传递到 Dmu 微型端口驱动程序。

![说明通过 portdmus 驱动程序的 midi 和 dls 数据流的示意图](images/dmportmi.png)

微型端口驱动程序将 MIDI 数据转换为波形格式，该格式呈现为端口驱动程序的其他部分指定的缓冲区：波形接收器。 然后，通过 KMixer 系统驱动程序，而不是在用户模式下 DirectSound，而是通过 [系统驱动程序](kernel-mode-wdm-audio-components.md#kmixer_system_driver)进入音频硬件。 DirectSound 实际上只是一个公开 KMixer 的 API，而 DirectSound 加速包含在硬件中加速的混音器函数，而不是在软件中按 KMixer 进行模拟。

[SysAudio 系统驱动程序](kernel-mode-wdm-audio-components.md#sysaudio_system_driver)（用于生成音频筛选器图）将 dmu 端口驱动程序连接到一片硬件。 端口驱动程序的波形接收器部分通过其向外的 SysAudio （可以连接到硬件设备）来向外传递数据。 它从 Dmu 微型端口驱动程序 (拉出波形数据，而不考虑它是硬件合成) 还是软件合成，并处理所有计时问题。 与用户模式相比，小型端口驱动程序类似于合成，而波形接收器只是端口驱动程序的一部分。

如果 Dmu 微型端口驱动程序可以向主机提供其输出，则会公开数据方向为 KSPIN 数据流的波形 pin \_ \_ (参阅 [**KSPIN**](/windows-hardware/drivers/ddi/ks/ns-ks-_kspin)) ，SysAudio 识别并连接到 KMixer。

有关波形接收器的详细信息，请参阅 [Kernel-Mode 软件合成程序的波形接收器](a-wave-sink-for-kernel-mode-software-synthesizers.md)。

本部分还包括：

[IMXF 接口](imxf-interfaces.md)

[分配器](allocator.md)

 


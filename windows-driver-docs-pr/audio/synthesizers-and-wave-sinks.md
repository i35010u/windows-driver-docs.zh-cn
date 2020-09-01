---
title: 合成器和 Wave 接收器
description: 合成器和 Wave 接收器
ms.assetid: ddcb847e-d46e-4860-9be9-4480e5a6b710
keywords:
- DirectMusic 自定义呈现 WDK 音频，合成
- 用户模式下的自定义呈现 WDK 音频，合成
- 用户模式下的自定义呈现 WDK 音频、波形接收器
- 波形接收器音频，用户模式
- 自定义 synths WDK 音频，DirectMusic 体系结构
- DirectMusic 自定义呈现 WDK 音频，波形接收器
- 用户模式 synths WDK 音频，DirectMusic 体系结构
- 用户模式波形接收器 WDK 音频
- 默认波形接收器
- 默认合成
- 自定义波形接收器 WDK 音频
- 合成 WDK 音频，关于用户模式合成程序
- 渲染引擎 WDK 音频
- DirectMusic WDK 音频，合成
- Dmu 端口驱动程序 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f5c19522a4957bfc99c338eeafc17509ba60e29e
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210341"
---
# <a name="synthesizers-and-wave-sinks"></a>合成器和 Wave 接收器


## <span id="synthesizers_and_wave_sinks"></span><span id="SYNTHESIZERS_AND_WAVE_SINKS"></span>


呈现引擎有两部分：

-   合成器，它采用 MIDI 消息并将其转换为波形音频示例。

-   波形接收器，它提供波形样本的目标并帮助同步输出。

默认情况下，DirectMusic 应用程序使用 Microsoft 软件合成器 ( # A0) 作为合成器和 DirectSound 作为波形输出设备。

在 DirectX 6.1 和 DirectX 7 中，DirectMusic 应用程序可以覆盖这些默认值。 例如，应用程序可能使用 Microsoft 软件合成器，但将输出定向到 .wav 文件，或者它可能实现适用于默认波形接收器的自定义合成器。 后一种情况更有可能，因为默认波形接收器应该适用于大多数合成程序。

在 DirectX 8 及更高版本中，DirectMusic 始终使用其内置波形接收器从用户模式合成输出数据，但应用程序可以覆盖默认的软件合成。 这意味着，DirectMusic 应用程序可以实现自定义用户模式合成器，但合成器必须使用 DirectMusic 的内置波形接收器。

下图显示了 DirectMusic 体系结构如何合并用户模式合成程序和波形接收器。 请注意，在下图中标记为 "DirectMusic Port" 的块不应与 PortCls 系统驱动程序模块中的内核模式 [dmu 端口驱动程序](dmus-port-driver.md) 混淆，portcls.sys。 DirectMusic 端口是一种用户模式对象，其中的 **IDirectMusicPort** 接口 (部分 DirectMusic API) 并在 dmusic.dll 实现。 有关 DirectMusic 端口的详细信息，请参阅 Microsoft Windows SDK 文档。

![说明用户模式合成程序和波形接收器的 directmusic 体系结构的关系图](images/dmblock.png)

在上图中，应用程序将数据发送到用户模式 DirectMusic 端口，该端口将 (MIDI 或 DLS) 下的数据传递给软件合成器 ( # A0 默认情况下) ，使其能够将笔记呈现为波数据。 波形接收器管理计时，并向合成器发送缓冲区以便在准备好接收数据突发时进行填充。 在默认情况下，合成器会将缓冲区填满 (**IDirectSoundBuffer** 对象) ，以便可以将其传递给 DirectSound。 DirectSound 可以通过 [KMixer 系统驱动程序](kernel-mode-wdm-audio-components.md#kmixer_system_driver) 播放数据，也可以通过音频设备上 DirectSound 硬件加速的渲染插针播放数据（如果有） (参阅 [DirectSound 硬件加速) 概述](overview-of-directsound-hardware-acceleration.md) 。

此相同的基本体系结构还适用于内核模式实现，但波形接收器直接将数据缓冲区直接传递到硬件或 KMixer 系统驱动程序例外。 Dmu 端口驱动程序实现内核模式软件合成器的波形接收器。 有关详细信息，请参阅 [内核模式软件合成程序的波形接收器](a-wave-sink-for-kernel-mode-software-synthesizers.md)。

完成这些步骤后，用户模式 DirectMusic 端口应打开并激活以供使用。 一旦这大部分驱动程序代码都在运行，就可以开始实现功能。 将用户模式 Microsoft 软件合成器的源代码用作模板并开始添加新功能。

用户模式软件合成器可以实现为具有 [IDirectMusicSynth](/windows/desktop/api/dmusics/nn-dmusics-idirectmusicsynth) 接口的对象。 用户模式波形接收器可实现为具有 [IDirectMusicSynthSink](/windows/desktop/api/dmusics/nn-dmusics-idirectmusicsynthsink) 接口的对象。 有关详细信息，请参阅 [IDirectMusicSynth 和 IDirectMusicSynthSink](idirectmusicsynth-and-idirectmusicsynthsink.md)。

 


---
title: 合成器和 Wave 接收器
description: 合成器和 Wave 接收器
ms.assetid: ddcb847e-d46e-4860-9be9-4480e5a6b710
keywords:
- DirectMusic 自定义呈现 WDK 音频，合成器
- 在用户模式 WDK 音频，合成器的自定义呈现
- 在用户模式 WDK 音频，批中的自定义呈现接收器
- 批接收器 WDK 音频，用户模式
- 自定义 synths WDK 音频，DirectMusic 体系结构
- DirectMusic 自定义呈现 WDK 音频，批接收器
- 用户模式下 synths WDK 音频，DirectMusic 体系结构
- 用户模式下批接收器 WDK 音频
- 默认批接收器
- 默认合成器
- 自定义批接收器 WDK 音频
- 合成器 WDK 音频，有关用户模式下合成器
- 呈现引擎 WDK 音频
- DirectMusic WDK 音频，合成器
- Dmu 端口驱动程序 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14263ab8c78348a5ae37bc9aaa3007927531fcba
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354199"
---
# <a name="synthesizers-and-wave-sinks"></a>合成器和 Wave 接收器


## <span id="synthesizers_and_wave_sinks"></span><span id="SYNTHESIZERS_AND_WAVE_SINKS"></span>


呈现引擎具有两个部分：

-   采用 MIDI 合成器消息，并将它们转换为 wave 音频示例。

-   批接收器，它为波样本并帮助提供目标同步输出。

默认情况下，DirectMusic 应用程序使用 Microsoft 软件合成器 (dmsynth.dll)，作为合成器和 DirectSound 为 wave 输出设备。

在 DirectX 6.1 和 DirectX 7，DirectMusic 应用程序可以重写这些默认值。 例如，应用程序可能使用 Microsoft 软件合成器，但将输出定向到.wav 文件，或者它可能会实现自定义的合成器的工作方式与默认批接收器。 后一种方案是更有可能，因为默认批接收器应适用于大多数合成器。

DirectX 8 及更高版本，DirectMusic 始终使用其内置批接收器来从用户模式下合成器，输出数据，但应用程序可以覆盖默认软件合成器。 这意味着 DirectMusic 应用程序可以实现自定义的用户模式下合成器，但是合成器必须使用 DirectMusic 的内置批接收器。

下图显示了如何 DirectMusic 体系结构包含用户模式下合成和批接收器。 请注意在下图中标记为"DirectMusic 端口"的块不应与内核模式混淆[Dmu 端口驱动程序](dmus-port-driver.md)PortCls 系统驱动程序模块中 portcls.sys。 DirectMusic 端口是一个具有用户模式对象**IDirectMusicPort**接口 （DirectMusic API 的一部分），并在 dmusic.dll 中实现。 有关 DirectMusic 端口的详细信息，请参阅 Microsoft Windows SDK 文档。

![说明用于用户模式下合成和批 directmusic 体系结构的关系图接收器](images/dmblock.png)

在上图中，应用程序将数据发送到用户模式下 DirectMusic 端口，从而传递软件合成器 (默认情况下 dmsynth.dll) 下的数据 （MIDI 或 DLS），以便它可以呈现到波形数据的说明。 批接收器管理时间，并将合成器传递的缓冲区填满时已准备好接收数据的突然增加。 合成器已满缓冲区 ( **IDirectSoundBuffer**对象默认情况下) 的数据，因此它可以传递给 DirectSound。 DirectSound 或者通过播放数据[KMixer 系统驱动程序](kernel-mode-wdm-audio-components.md#kmixer_system_driver)或它通过 DirectSound 硬件加速呈现 pin 上播放的音频设备，如果有可用 (请参阅[DirectSound 硬件概述加速](overview-of-directsound-hardware-acceleration.md))。

此相同的基本体系结构还适用于内核模式实现，但例外波形接收器将数据缓冲区，直接与硬件或 KMixer 系统驱动程序。 Dmu 端口驱动程序实现内核模式软件合成器的批接收器。 有关详细信息，请参阅[批接收器的内核模式软件合成器](a-wave-sink-for-kernel-mode-software-synthesizers.md)。

完成这些步骤后，用户模式下 DirectMusic 端口应为打开状态且用于已激活。 只要此驱动程序代码的大部分操作有效的产品，可以开始实现功能。 用于用户模式下的 Microsoft 软件合成器作为模板的源代码并开始添加新功能。

用户模式软件合成器可以作为一个对象来实现[IDirectMusicSynth](https://docs.microsoft.com/windows/desktop/api/dmusics/nn-dmusics-idirectmusicsynth)接口。 用户模式下批接收器可以作为一个对象来实现[IDirectMusicSynthSink](https://docs.microsoft.com/windows/desktop/api/dmusics/nn-dmusics-idirectmusicsynthsink)接口。 有关详细信息，请参阅[IDirectMusicSynth 和 IDirectMusicSynthSink](idirectmusicsynth-and-idirectmusicsynthsink.md)。

 

 





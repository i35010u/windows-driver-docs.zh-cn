---
title: DLS 下载支持
description: DLS 下载支持
ms.assetid: be080b53-0a9d-47fc-b07b-88052efdf9a8
keywords:
- 可下载的声音 WDK 音频
- DirectMusic 自定义呈现 WDK 音频、 可下载声音
- 在用户模式 WDK 音频、 可下载声音中的自定义呈现
- DLS WDK 音频
- 乐器声音 WDK 音频
- MIDI 注意消息转换
- MIDI 注意转换 WDK 音频
- 用户模式下 synths WDK 音频、 可下载声音
- 自定义 synths WDK 音频、 可下载声音
- 合成器 WDK 音频、 可下载声音
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc16fdf73e9c72529a847cdd74d796b58e96fd3e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360123"
---
# <a name="dls-download-support"></a>DLS 下载支持


## <span id="custom_dls"></span><span id="CUSTOM_DLS"></span>


如果你正在编写你自己合成器，您还必须可下载声音 (DL) 提供支持，以便应用程序可以将 MIDI 注意消息转换为特定乐器的声音。 具体而言，应实现你[ **IDirectMusicSynth::Download** ](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-download)方法，以便它可以检测批和清晰表述数据下载到合成器。 此方法应接受原始数据 （通常是从集合文件），并将其存储在可由呈现引擎的窗体。

DirectMusic DLS 数据下载到驱动程序时，按照多个 DirectMusic 结构定义的数据缓冲区格式。 下载的数据开头为两个结构：

<span id="DMUS_DOWNLOADINFO"></span><span id="dmus_downloadinfo"></span>DMU\_DOWNLOADINFO  
固定大小标头描述正在下载的信息。

<span id="DMUS_OFFSETTABLE"></span><span id="dmus_offsettable"></span>DMU\_OFFSETTABLE  
一个偏移量的表，遵循标头并描述了各种块内下载的数据的信息的偏移量。

后面偏移的表使用的是实际数据，可以开始与以下组件之一：

<span id="DMUS_INSTRUMENT"></span><span id="dmus_instrument"></span>DMU\_检测  
一个描述 DLS 检测的结构。

<span id="DMUS_WAVEDATA"></span><span id="dmus_wavedata"></span>DMU\_WAVEDATA  
包含大量 PCM 格式的批数据的结构。

有关这些数据结构和用于下载检测和波形数据的数据格式的详细信息，请参阅 DirectMusic 低级别 DLS Microsoft Windows SDK 文档中的讨论。

DLS 数据格式是在内核和用户模式中相同的。

[KSPROPSETID\_合成\_Dls](https://docs.microsoft.com/windows-hardware/drivers/audio/kspropsetid-synth-dls)属性集包含用于下载 DLS 示例和 instruments 到 DirectMusic 合成器的属性。 设置此属性可用于下载 DLS 级别 1 和 2 DLS 级数据。 仅 DLS 级别 1 和 2 之间的已下载的数据更改的格式。

 

 





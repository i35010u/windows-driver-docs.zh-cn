---
title: DLS 下载支持
description: DLS 下载支持
ms.assetid: be080b53-0a9d-47fc-b07b-88052efdf9a8
keywords:
- 可下载声音乐曲音频
- DirectMusic 自定义渲染声音频，可下载声音
- 用户模式下的自定义呈现声音频，可下载声音
- DLS WDK 音频
- 检测声音声音频
- 转换 MIDI 注释消息
- MIDI 便笺转换 WDK 音频
- 用户模式 synths WDK 音频，可下载声音
- 自定义 synths WDK 音频，可下载声音
- 合成 WDK 音频，可下载声音
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a3a799b85ec54874abdbfbf5bbfb28b557ba560
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208089"
---
# <a name="dls-download-support"></a>DLS 下载支持


## <span id="custom_dls"></span><span id="CUSTOM_DLS"></span>


如果你正在编写自己的合成器，则还必须为 (DLS) 的可下载声音提供支持，使应用程序能够将 MIDI 注释消息转换为特定乐器声音。 具体而言，你应该实现 [**IDirectMusicSynth：:D o) **](/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-download) 方法，以便它可以将检测波和 articulation 数据下载到合成器。 此方法应接受 (通常来自集合文件的原始数据) 并将其存储在可供呈现引擎使用的窗体中。

当 DirectMusic 将 DLS 数据下载到驱动程序时，将根据几个 DirectMusic 结构定义数据缓冲区的格式。 下载的数据以两个结构开始：

<span id="DMUS_DOWNLOADINFO"></span><span id="dmus_downloadinfo"></span>DMU \_ DOWNLOADINFO  
描述要下载的信息的固定大小的标头。

<span id="DMUS_OFFSETTABLE"></span><span id="dmus_offsettable"></span>DMU \_ OFFSETTABLE  
在标头之后的偏移表，用于描述已下载数据中各种信息块的偏移量。

下面的偏移表是实际数据，可以从以下任一值开始：

<span id="DMUS_INSTRUMENT"></span><span id="dmus_instrument"></span>DMU \_ 仪器  
描述 DLS 检测的结构。

<span id="DMUS_WAVEDATA"></span><span id="dmus_wavedata"></span>DMU \_ WAVEDATA  
一个结构，其中包含 PCM 格式的波形数据块。

若要详细了解这些数据结构以及用于下载检测和波形数据的数据格式，请参阅 Microsoft Windows SDK 文档中的 DirectMusic 低级别 DL 讨论。

在内核模式和用户模式下，DLS 数据格式是相同的。

[KSPROPSETID \_ 合成器 \_ Dls](./kspropsetid-synth-dls.md)属性集包含用于将 Dls 示例和乐器下载到 DirectMusic 合成器的属性。 此属性集可用于下载 DLS Level 1 和 DLS Level 2 数据。 只有已下载数据的格式在 DL 级别1和2之间发生更改。

 


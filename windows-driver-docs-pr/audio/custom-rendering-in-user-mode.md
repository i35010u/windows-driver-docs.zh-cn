---
title: 用户模式下的自定义呈现
description: 用户模式下的自定义呈现
keywords:
- DirectMusic 自定义呈现 WDK 音频
- DirectMusic 自定义呈现 WDK 音频，关于用户模式自定义呈现
- Microsoft 软件合成器 WDK 音频
- 自定义 synths WDK 音频
- 用户模式 synths WDK 音频，自定义
- 自定义用户模式渲染 WDK 音频
- 波形接收器音频，用户模式自定义呈现
- DirectMusic WDK 音频，自定义 synths
- 用户模式下的自定义呈现 WDK 音频
- 用户模式下的自定义呈现 WDK 音频，关于自定义呈现
- DirectMusic WDK 音频，用户模式
- 默认合成
- 合成 WDK 音频，用户模式自定义呈现
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a6e5eebe7763b1d082fb1155831a8bea7d6dd99
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789319"
---
# <a name="custom-rendering-in-user-mode"></a>用户模式下的自定义呈现


## <span id="custom_rendering_in_user_mode"></span><span id="CUSTOM_RENDERING_IN_USER_MODE"></span>


Microsoft 软件合成器是 DirectMusic 安装的用户模式组件，应该足以满足大多数合成合成目的。 DirectMusic 使用此组件作为其默认合成器。

此外，DirectMusic 允许你实现自己的用户模式软件合成器。 合成器接受包含 MIDI 事件的输入流，并生成一个包含波形数据的输出流。 通常，自定义合成器会将其生成的波形流馈送到 DirectMusic 的内置波形接收器，这会通过 Microsoft DirectSound 播放流。 但是，在 Microsoft DirectX 6.1 和7中，DirectMusic 允许你使用自定义的用户模式波形接收器将呈现的波形输出重定向到 DirectSound 以外的其他设备。 但是，很少需要自定义波形接收器。 在 DirectX 8 及更高版本中，DirectMusic 不支持自定义波形接收器。

最重要的 DirectMusic synths 头文件是 dmusics (用户模式仅) ，dmusicks (内核模式仅) 、dmusbuff 和 dmusprop。

本部分的其余部分将讨论自定义呈现过程的各个方面。 本部分中的示例假定用户模式实现，尽管它们提供的概念适用于用户模式和内核模式，但在其他情况下除外。 本文讨论了以下主题：

[合成器和 Wave 接收器](synthesizers-and-wave-sinks.md)

[IDirectMusicSynth 和 IDirectMusicSynthSink](idirectmusicsynth-and-idirectmusicsynthsink.md)

[MIDI 到 Wave](midi-to-wave.md)

[合成器计时](synthesizer-timing.md)

[DLS 下载支持](dls-download-support.md)

[注册合成器](registering-your-synthesizer.md)

 

 





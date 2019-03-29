---
title: 用户模式下的自定义呈现
description: 用户模式下的自定义呈现
ms.assetid: a30c9eae-c3a9-4ff8-8e6c-d98c83f8596e
keywords:
- DirectMusic 自定义呈现 WDK 音频
- DirectMusic 自定义呈现 WDK 音频，有关用户模式下自定义呈现
- Microsoft 软件合成器 WDK 音频
- 自定义 synths WDK 音频
- 用户模式下 synths WDK 音频，自定义
- 自定义用户模式下呈现 WDK 音频
- 批接收器 WDK 音频，用户模式下自定义呈现
- DirectMusic WDK 音频、 自定义 synths
- 用户模式 WDK 音频中的自定义呈现
- 在用户模式 WDK 音频，有关自定义呈现的自定义呈现
- DirectMusic WDK 音频，用户模式
- 默认合成器
- 合成器 WDK 音频，用户模式下自定义呈现
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31dee4bd93f88200ae1c5ccb23cefdc318f647b6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577296"
---
# <a name="custom-rendering-in-user-mode"></a>用户模式下的自定义呈现


## <span id="custom_rendering_in_user_mode"></span><span id="CUSTOM_RENDERING_IN_USER_MODE"></span>


Microsoft 软件合成器是 DirectMusic 安装的用户模式组件，并且应该适合大多数情况下合成器。 DirectMusic 使用此组件作为其默认合成器。

此外，DirectMusic，可实现您自己的用户模式软件合成器。 合成器接受 MIDI 事件所组成的输入的流并生成包含波形数据的输出流。 通常情况下，自定义的合成器到 DirectMusic 的内置批接收器，播放流通过 Microsoft DirectSound 馈送它生成的批的流。 用户模式下批中 Microsoft DirectX 6.1 和 7，DirectMusic，可使用自定义，但是，接收器为 wave 输出呈现的重定向到 DirectSound 以外的其他设备。 但是，自定义批接收器很少是必需的。 DirectX 8 及更高版本，DirectMusic 提供自定义批接收器不支持。

Dmusics.h （仅限用户模式）、 dmusicks.h （仅适用于内核模式）、 dmusbuff.h 和 dmusprop.h DirectMusic synths 最重要的标头文件。

本部分的其余部分将讨论自定义呈现过程的各个方面。 在本部分中的示例假定一个用户模式的实现，尽管它们在呈现的概念适用于用户和内核模式下，除否则标注的位置。 论述了以下主题：

[合成和批接收器](synthesizers-and-wave-sinks.md)

[IDirectMusicSynth 和 IDirectMusicSynthSink](idirectmusicsynth-and-idirectmusicsynthsink.md)

[批的 MIDI](midi-to-wave.md)

[合成器计时](synthesizer-timing.md)

[DLS 下载支持](dls-download-support.md)

[注册你合成器](registering-your-synthesizer.md)

 

 





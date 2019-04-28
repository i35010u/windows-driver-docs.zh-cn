---
title: DirectSound 节点排序要求
description: DirectSound 节点排序要求
ms.assetid: baca55f5-c669-4bd2-82b5-3985030864f2
keywords:
- 硬件加速 WDK DirectSound，节点排序要求
- 节点排序要求 WDK DirectSound
- 节点链接 WDK DirectSound
- SUM 节点 WDK DirectSound
- 3D 混合 WDK 音频
- 2D 混合 WDK 音频
- 软件模拟三维处理 WDK 音频
- supermixer 节点 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4c692927dd1f5a696b07986a453822f903a519d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333776"
---
# <a name="directsound-node-ordering-requirements"></a>DirectSound 节点排序要求


## <span id="directsound_node_ordering_requirements"></span><span id="DIRECTSOUND_NODE_ORDERING_REQUIREMENTS"></span>


DirectSound 2D 或 3D mixer pin 应包含以下一系列节点的节点链：

-   卷节点 (请参阅[ **KSNODETYPE\_卷**](https://msdn.microsoft.com/library/windows/hardware/ff537208)。)

-   3D 节点 （此节点是可选的。 请参阅[ **KSNODETYPE\_3D\_效果**](https://msdn.microsoft.com/library/windows/hardware/ff537148)。)

-   Supermixer 节点 (请参阅[ **KSNODETYPE\_SUPERMIX**](https://msdn.microsoft.com/library/windows/hardware/ff537198)。)

-   卷节点 （适用于平移效果）

-   SRC 节点 (请参阅[ **KSNODETYPE\_SRC**](https://msdn.microsoft.com/library/windows/hardware/ff537190)。)

-   SUM 节点 (请参阅[ **KSNODETYPE\_SUM**](https://msdn.microsoft.com/library/windows/hardware/ff537196)。)

此列表中的节点显示的数据固定到流式处理出现的顺序。 其他节点可以交错而不会导致问题，前提保留上述顺序这些节点之间。

2D pin 要求在上一列表中，除 3D 节点，这是可选的所有节点。 3D pin 需要在列表中，包括 3D 节点的所有节点。

SRC （采样率转换） 节点应有的总和节点。 虽然这不是一项要求 SRC 和 SUM 节点通常相邻。 **IDirectSoundBuffer::SetFrequency**方法 （请参阅 Microsoft Windows SDK 文档） perturbs SRC 节点重新采样速率。

包含唯一的 SRC 和 SUM 节点混音器足以满足管理的系统驱动程序，如 SWMidi 和 Redbook 的流混合 (请参阅[SWMidi 系统驱动程序](kernel-mode-wdm-audio-components.md#swmidi_system_driver)并[Redbook 系统驱动程序](kernel-mode-wdm-audio-components.md#redbook_system_driver))，但此外，DirectSound 需要两个卷节点和 supermixer 节点位于 SUM 节点。 DirectSound 发送批量更改所得**IDirectSoundBuffer::SetVolume**对第一个卷节点和平移效果从发送调用**IDirectSoundBuffer::SetPan**对第二个调用卷节点。

DirectSound 可以通过使用生成三维效果的 2D 插针**SetVolume**， **SetPan**，并**SetFrequency**调用，以控制的卷和 SRC 节点：

-   **SetVolume**调用可以模拟的距离的声音源从侦听器中的更改。

-   **SetPan**调用可以模拟方向相对于侦听器的声音源中的更改。

-   **SetFrequency**调用可以模拟 Doppler 效果和 HRTFs （head 相关传输函数）。

Supermixer 节点是十字条矩阵 M 输入的通道连接到 N 的输出渠道，其中 N 应等于的中设备的最终输出流的通道数。

管理硬件加速的 3D 效果所需的可选 3D 节点 (请参阅[WDM 音频中支持三维 DirectSound 加速](supporting-3d-directsound-acceleration-in-wdm-audio.md))，但不是需要的软件模拟三维处理。 大多数现有的实现将放置在 SRC 节点之前和 supermixer 节点中，第一个卷节点之间的 3D 节点但可使用其他配置。

输入的流到三维节点通常包含一条通道。 DirectSound 8.0 及更高版本，则可以使用三维效果创建 mono PCM 缓冲区。 早期版本的 DirectSound，但是，支持具有 mono 和立体声输入流，3D 节点和驱动程序应支持这两个以确保与较旧的应用程序兼容性。

 

 





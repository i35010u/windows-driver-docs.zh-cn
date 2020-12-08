---
title: DirectSound 节点排序要求
description: DirectSound 节点排序要求
keywords:
- 硬件加速 WDK DirectSound，节点顺序要求
- 节点顺序要求 WDK DirectSound
- 节点链 WDK DirectSound
- SUM 节点 DirectSound
- 3D 混合 WDK 音频
- 2D 混合 WDK 音频
- 软件模拟3D 处理 WDK 音频
- supermixer 节点 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9520c63985b79c6d68a36f5e191cdff4c08b5ff4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786599"
---
# <a name="directsound-node-ordering-requirements"></a>DirectSound 节点排序要求


## <span id="directsound_node_ordering_requirements"></span><span id="DIRECTSOUND_NODE_ORDERING_REQUIREMENTS"></span>


DirectSound 2D 或3D 合成器 pin 应具有包含以下节点序列的节点链：

-   卷节点 (参阅 [**KSNODETYPE \_ VOLUME**](./ksnodetype-volume.md)。 ) 

-   3D 节点 (此节点是可选的。 请参阅 [**KSNODETYPE \_ 三维 \_ 效果**](./ksnodetype-3d-effects.md)。 ) 

-   Supermixer 节点 (参阅 [**KSNODETYPE \_ SUPERMIX**](./ksnodetype-supermix.md)。 ) 

-   用于平移效果的卷节点 () 

-   SRC 节点 (参阅 [**KSNODETYPE \_ SRC**](./ksnodetype-src.md)。 ) 

-   SUM 节点 (参阅 [**KSNODETYPE \_ SUM**](./ksnodetype-sum.md)。 ) 

此列表中的节点按数据流式传输到 pin 中的顺序出现。 其他节点可以在这些节点之间交错，而不会导致问题，前提是上述顺序已保留。

二维 pin 需要上一列表中的所有节点，3D 节点除外，这是可选的。 三维 pin 需要列表中的所有节点，包括3D 节点。

SRC (采样率转换) 节点应位于 SUM 节点之前。 尽管这不是必需的，但 SRC 和 SUM 节点通常是相邻的。 **IDirectSoundBuffer：： SetFrequency** 方法 (参阅 Microsoft Windows SDK 文档) perturbs SRC 节点的重新采样速率。

仅包含 SRC 和 SUM 节点的混音器足以用于混合由系统驱动程序（例如 SWMidi 和 Redbook）管理的流 (参阅 [SWMidi 系统驱动](kernel-mode-wdm-audio-components.md#swmidi_system_driver) 程序和 [Redbook 系统驱动程序](kernel-mode-wdm-audio-components.md#redbook_system_driver)) ，但 DirectSound 还要求两个卷节点和 supermixer 节点位于 SUM 节点之前。 DirectSound 会将 **IDirectSoundBuffer：： SetVolume** 调用产生的卷更改发送到第一个卷节点，并将 **IDirectSoundBuffer：： SetPan** 调用的平移效果发送到第二个卷节点。

DirectSound 可以通过使用 **SetVolume**、 **SetPan** 和 **SetFrequency** 调用来控制卷和 SRC 节点，从而在二维引脚上生成三维效果：

-   **SetVolume** 调用可以模拟声音源与侦听器之间的变化。

-   **SetPan** 调用可以模拟相对于侦听器的声音源的变化。

-   **SetFrequency** 调用可以模拟 Doppler 效果和 HRTFs (头相关传输函数) 。

Supermixer 节点是将 M 输入通道连接到 N 个输出通道的一种纵横比矩阵，其中 N 应等于设备最终输出流中的通道数。

需要可选的3D 节点来管理硬件加速三维效果 (参阅 [在 WDM 音频) 中支持 3D DirectSound 加速](supporting-3d-directsound-acceleration-in-wdm-audio.md) ，但不需要进行软件模拟3d 处理。 大多数现有的实现将3D 节点放在 SRC 节点之前以及第一个卷节点和 supermixer 节点之间，但可以进行其他配置。

三维节点的输入流通常包含单个通道。 在 DirectSound 8.0 和更高版本中，仅可以通过三维效果创建 mono PCM 缓冲区。 但是，早期版本的 DirectSound 支持带有 mono 和立体声输入流的3D 节点，并且驱动程序应同时支持这两者，以确保与较旧的应用程序兼容。

 


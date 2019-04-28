---
title: DirectSound 硬件加速概述
description: DirectSound 硬件加速概述
ms.assetid: 1f18f88a-2dd6-4b7a-b083-f43ab58571b3
keywords:
- 硬件加速 WDK DirectSound 有关 DirectSound 硬件加速
ms.date: 10/27/2017
ms.localizationpriority: medium
ms.openlocfilehash: 610712f39e8837e7ce687c0147b12b8ee450f1fe
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332236"
---
# <a name="overview-of-directsound-hardware-acceleration"></a>DirectSound 硬件加速概述


## <span id="overview_of_directsound_hardware_acceleration"></span><span id="OVERVIEW_OF_DIRECTSOUND_HARDWARE_ACCELERATION"></span>


许多音频适配器提供 DirectSound 硬件加速，对于一个或多个 DirectSound 流执行混合使用的硬件的能力。 硬件混合使用通过音频混合操作从 CPU 卸载和执行这些硬件的速度提高了性能。 除了混合，硬件执行相关的操作如衰减，采样率转换 （源） 和 （可选） 3D 处理，否则需要在软件中执行。

所有 WaveCyclic 或 WavePci 呈现设备提供一个或多个硬件 pin 进行混合音频流。 在单一流设备的情况下[KMixer 系统驱动程序](kernel-mode-wdm-audio-components.md#kmixer_system_driver)始终在一个可用的硬件呈现插针上实例化。

DirectSound 采用硬件加速的设备提供多个硬件混合使用 pin。 每个其他的 pin 可以用于混合 DirectSound 流。 DirectSound 流馈送到硬件 mixer pin 绕过 KMixer，避免在 KMixer 中混合使用的软件的延迟。 DirectSound 利用了所有音频设备的可用硬件加速混音器固定，只要这些 pin 必须符合的拓扑[DirectSound 节点排序要求](directsound-node-ordering-requirements.md)。 DirectSound 还要求球瓶，支持 DirectSound 数据格式由 KSDATAFORMAT\_说明符\_DSOUND (请参阅[DirectSound Stream 数据格式](directsound-stream-data-format.md))。

[SysAudio 系统驱动程序](kernel-mode-wdm-audio-components.md#sysaudio_system_driver)始终为 KMixer 保留一个硬件插针，以便其他 （非保留） 硬件 pin 所有已分配后，可以通过 KMixer 混合和送入保留的硬件 pin 任何其他流。

在图[呈现批内容使用 DirectSound 软件和硬件缓冲区](rendering-wave-content-using-directsound-software-and-hardware-buffers.md)演示了这些概念。

如果音频设备提供足够数量混合使用 pin，所有 DirectSound 应用程序的输出流可以是硬件的硬件加速。 如果不是，DirectSound 应用程序具有几个选项：

-   它可以静态方式分配可用的硬件混合的流的要求最低延迟的 pin。

-   它可以动态地分配混合到流的 pin，如他们所需的球瓶视为共享资源池的可用硬件。

有关详细信息，请参阅 Microsoft Windows SDK 文档中的语音管理的讨论。

DirectSound 可以使用两种类型的硬件 mixer pin:2D 和 3D。 2D pin 执行 SRC、 衰减，和混合使用，但不是三维定位。 DirectSound 可以使用 2D pin 进行三维定位通过在软件中执行必要的衰减和频率计算并将结果应用于的 2D 插针的相应节点。 与此相反，3D pin 包含无法计算而不是依靠 DirectSound 若要执行此操作的 3D 缓冲区和 3D 侦听器属性直接从其自身三维效果的三维节点。 3D 节点的属性的列表，请参阅[ **KSNODETYPE\_3D\_效果**](https://msdn.microsoft.com/library/windows/hardware/ff537148)。 有关 2D 和 3D pin 的详细信息，请参阅[WDM 音频中支持 2D DirectSound 加速](supporting-2d-directsound-acceleration-in-wdm-audio.md)并[WDM 音频中支持三维 DirectSound 加速](supporting-3d-directsound-acceleration-in-wdm-audio.md)。

 





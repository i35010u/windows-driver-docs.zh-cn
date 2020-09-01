---
title: DirectSound 硬件加速概述
description: DirectSound 硬件加速概述
ms.assetid: 1f18f88a-2dd6-4b7a-b083-f43ab58571b3
keywords:
- 硬件加速 WDK DirectSound，关于 DirectSound 硬件加速
ms.date: 10/27/2017
ms.localizationpriority: medium
ms.openlocfilehash: 320fbae1a1912471a89f773a4064a9bd1727b4ab
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210533"
---
# <a name="overview-of-directsound-hardware-acceleration"></a>DirectSound 硬件加速概述


## <span id="overview_of_directsound_hardware_acceleration"></span><span id="OVERVIEW_OF_DIRECTSOUND_HARDWARE_ACCELERATION"></span>


许多音频适配器提供 DirectSound 硬件加速功能，这是为一个或多个 DirectSound 流执行硬件混合的能力。 硬件混合通过从 CPU 中卸载音频混合操作并按硬件速度执行，从而提高了性能。 除混合外，硬件还会执行相关操作，例如 (SRC 的采样速率转换) 、衰减，还可以选择在软件中执行的3D 处理。

所有 WaveCyclic 或 WavePci 渲染设备都提供一个或多个硬件 pin 来混合音频流。 对于单流设备， [KMixer 系统驱动程序](kernel-mode-wdm-audio-components.md#kmixer_system_driver) 将始终在可用硬件呈现 pin 上实例化。

具有 DirectSound 硬件加速的设备提供了多个硬件混合 pin。 可以使用每个额外的 pin 来混合 DirectSound 流。 传入硬件混音器 pin 的 DirectSound 流将绕过 KMixer，并避免 KMixer 中软件混合的延迟。 DirectSound 利用音频设备的所有可用硬件加速混音器 pin，只要这些针脚的拓扑符合 [DirectSound 的节点顺序要求](directsound-node-ordering-requirements.md)即可。 DirectSound 还要求 pin 支持 KSDATAFORMAT 说明符 DSOUND 指定的 DirectSound 数据格式 \_ \_ (参阅 [DirectSound Stream 数据格式](directsound-stream-data-format.md)) 。

[SysAudio 系统驱动程序](kernel-mode-wdm-audio-components.md#sysaudio_system_driver)始终为 KMixer 保留一个硬件 pin，以便在另一)  (未保留硬件 pin 已分配后，可通过 KMixer 将任何其他流混合到预留硬件 pin 中。

[使用 DirectSound 软件和硬件缓冲区呈现波形内容](rendering-wave-content-using-directsound-software-and-hardware-buffers.md)的图演示了这些概念。

如果音频设备提供了足够数量的硬件混合 pin，则所有 DirectSound 应用程序的输出流都可以进行硬件加速。 如果不是，则 DirectSound 应用程序具有几个选项：

-   它可以静态地将可用硬件混合 pin 分配到需要最低延迟的流中。

-   它可以通过将 pin 视为共享资源池，根据需要动态地将可用硬件混合 pin 分配给流。

有关详细信息，请参阅 Microsoft Windows SDK 文档中的语音管理讨论。

DirectSound 可以使用两种类型的硬件混合器 pin：二维和三维。 二维 pin 执行 SRC、衰减和混合，但不执行3D 定位。 DirectSound 可以通过在软件中执行必要的衰减和频率计算，并将结果应用于 2D pin 上的相应节点，来使用 2D pin 来执行3D 定位。 与此相反，3D pin 包含一个3D 节点，该节点可以直接从3D 缓冲区和3D 侦听器属性计算自己的3D 效果，而不是依赖 DirectSound 来实现此目的。 有关3D 节点的属性列表，请参阅 [**KSNODETYPE \_ 3d \_ 效果**](./ksnodetype-3d-effects.md)。 有关二维和3D 插针的详细信息，请参阅 [支持 Wdm 音频中的 2D DirectSound 加速](supporting-2d-directsound-acceleration-in-wdm-audio.md) 和 [支持 wdm 音频中的 3d DirectSound 加速](supporting-3d-directsound-acceleration-in-wdm-audio.md)。


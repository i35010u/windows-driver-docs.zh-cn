---
title: 音频筛选器图
description: 音频筛选器图
ms.assetid: 823de0d5-9368-4ae6-9f11-a8daa0640edd
keywords:
- 音频筛选器 WDK 音频，关系图
- 筛选器关系图 WDK 音频，有关筛选器关系图
- KS 筛选器关系图中会 WDK 音频，有关 KS 筛选器关系图
- 接收器 pin WDK 音频
- 源 pin WDK 音频
- 桥 pin WDK 音频
- pin WDK 音频，筛选器关系图
- KS 筛选器关系图 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6ba6e0b89b4e7cea8e50f77ddfbc5a17b33d0f3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331485"
---
# <a name="audio-filter-graphs"></a>音频筛选器图


## <span id="audio_filter_graphs"></span><span id="AUDIO_FILTER_GRAPHS"></span>


KS 筛选器关系图是已连接在一起处理一个或多个数据流的 KS 筛选器的集合。 音频筛选器关系图是包含处理的音频数据流量的筛选器的 KS 筛选器关系图。 例如下, 图是执行音频呈现和捕获音频筛选器关系图的简化的关系图。

![说明简单呈现和捕获音频筛选器的关系图](images/graph.png)

在图中，筛选器关系图扩展球瓶的两个批筛选器的顶部到底部的两个拓扑筛选器的球瓶。 用户模式软件模块和外部的音频设备 （即，扬声器和麦克风） 位于关系图之外。

该图的下半部分中的四个筛选器表示音频的适配器上的硬件设备，可以呈现和捕获批流。 每个图中所示的筛选器是通过将端口驱动程序绑定到微型端口驱动程序实现的。 适配器驱动程序通过绑定到相应的批 WaveRT、 WavePci 或 WaveCyclic 端口驱动程序，从而形成批筛选器*Xxx*微型端口驱动程序。 适配器驱动程序通过拓扑端口驱动程序绑定到拓扑微型端口驱动程序，从而形成拓扑筛选器。

上图的左侧，从 DirectSound 或 waveOut 应用程序 （顶端） 的音频流播放通过扬声器 （底部）。 在右侧，DirectSoundCapture 或 waveIn 的应用程序 （前） 记录来自麦克风 （底端） 输入的流。 在这两个面上执行混合的 Windows Vista 中的系统时，音频引擎的实例插入批筛选器与应用程序之间。 (在 Windows Server 2003、 Windows XP、 Windows 2000 和 Windows Me / 98， [KMixer 系统驱动程序](kernel-mode-wdm-audio-components.md#kmixer_system_driver)是系统 mixer。)

音频引擎是在用户模式下运行的多用途软件筛选器，并轻松地以不同的音频格式与在其源和接收器的插针的采样速率之间进行转换。 音频引擎通常可以适应该硬件配置的流格式和应用程序所需的流格式之间的差异。

在上图中的底部，并接收麦克风信号接收器 pin 源 pin 驱动说话人标记为桥的 pin。 桥 pin 桥接的筛选器关系图和与外部环境之间的边界。

在上图中，通常显示每个批筛选器和其相应的拓扑筛选器之间的数据路径表示的物理连接： 无法通过软件配置的音频适配器上的固定，硬件连接。

由于已永久连接桥 pin 或物理连接的 pin，pin 隐式地存在，无法实例化或删除。 因此，有没有桥 pin 对象 （实例的桥 pin） 来发送 Irp 到，但您可以查询的筛选器对象[KSPROPSETID\_Pin](https://msdn.microsoft.com/library/windows/hardware/ff566584)其插针，桥的属性。 同一规则适用于使用物理连接的插针。

传递桥 pin 或物理连接的信号可以模拟或数字。

例如，在上图中，这两种两个桥 pin 处理模拟信号。 在左侧的桥 pin 传输从 DAC （数字模拟转换器），从而推动了演讲者的输出信号。 在右侧的桥 pin 从麦克风输入 ADC （模拟到数字转换器） 接收信号。 但是，桥 pin 也可能表示音频设备上的 S/PDIF 连接器。 在这种情况下，通过桥 pin 的信号是数字，而不是模拟。

 

 





---
title: 音频筛选器图
description: 音频筛选器图
ms.assetid: 823de0d5-9368-4ae6-9f11-a8daa0640edd
keywords:
- 音频筛选 WDK 音频，图形
- 筛选器图形 WDK 音频，关于筛选器图形
- KS 筛选器图形 WDK 音频，关于 KS 筛选器图
- 接收器引脚 WDK 音频
- 源引脚 WDK 音频
- 桥接 WDK 音频
- 锁定 WDK 音频，筛选器图形
- KS 筛选器图形 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f979dc882c3305e37553ebc9779240ca765f3b82
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208335"
---
# <a name="audio-filter-graphs"></a>音频筛选器图


## <span id="audio_filter_graphs"></span><span id="AUDIO_FILTER_GRAPHS"></span>


KS 筛选器图是已连接在一起以处理一个或多个数据流的 KS 筛选器的集合。 音频筛选器图是一个 KS 筛选器图形，其中包含处理音频数据流的筛选器。 例如，下图是执行音频呈现和捕获的音频筛选器图的简化图。

![说明用于渲染和捕获的简单音频过滤器的示意图](images/graph.png)

在该图中，筛选器图从两个波形滤镜顶部的引脚延伸到两个拓扑过滤器底部的针脚。 用户模式软件模块和外部音频设备 (即，扬声器和麦克风) 位于图形外。

图下半部分的四个筛选器表示音频适配器上的硬件设备，可呈现和捕获波形流。 图中所示的每个筛选器都是通过将端口驱动程序绑定到微型端口驱动程序来实现的。 适配器驱动程序通过将 WaveRT、WavePci 或 WaveCyclic 端口驱动程序绑定到相应的波浪*Xxx* 微型端口驱动程序形成波形筛选器。 适配器驱动程序通过将拓扑端口驱动程序绑定到拓扑微型端口驱动程序形成拓扑筛选器。

在该图的左侧，来自 DirectSound 或 waveOut 应用程序的音频流 (顶部) 通过扬声器 (底部) 播放。 在右侧，"DirectSoundCapture" 或 "waveIn" 应用程序 (top ") 记录从麦克风 (底部) 输入的流。 在这两个方面，在 Windows Vista 中对系统执行混合的音频引擎实例在 wave 筛选器和应用程序之间是 interposed 的。  (在 Windows Server 2003、Windows XP、Windows 2000 和 Windows Me/98 中， [KMixer 系统驱动程序](kernel-mode-wdm-audio-components.md#kmixer_system_driver) 是系统混音器。 ) 

音频引擎是一种通用的软件筛选器，在用户模式下运行，可以在其源和接收器插针之间轻松转换各种音频格式和采样速率。 音频引擎通常可以容纳为硬件配置的流格式和应用程序预期的流格式之间的差异。

在上图的底部，驱动扬声器的源插针和接收麦克风信号的接收器 pin 标记为桥接 pin。 桥接程序在筛选器图和外部环境之间桥接边界。

在上图中，每个波形筛选器和其对应的拓扑筛选器之间显示的数据路径通常表示物理连接：音频适配器上的固定硬件连接，不能通过软件进行配置。

由于桥接 pin 或具有物理连接的 pin 是永久性连接的，因此，该 pin 将隐式存在并且无法实例化或删除。 因此，虽然您可以在 [KSPROPSETID \_ 端口](../stream/kspropsetid-pin.md) 上查询其桥接程序的 "筛选器" 属性，但 (不存在桥接) 要将 irp 发送到的桥插端口实例。 相同的规则适用于具有物理连接的 pin。

通过桥接 pin 或物理连接传递的信号可以是模拟或数字。

例如，在上图中，两个桥接器都处理模拟信号。 左侧的桥接会将来自 DAC (数字到模拟转换器) 的输出信号传输到用于驱动扬声器的信号。 右侧的桥接会接收来自麦克风的信号，该信号会输入 ADC (模拟到数字转换器) 。 但是，桥接 pin 可能还会在音频设备上表示 S/PDIF 连接器。 在这种情况下，通过桥接 pin 的信号是数字，而不是模拟。

 


---
title: 用于管理波次输出延迟的因素
description: 用于管理波次输出延迟的因素
ms.assetid: 6342ffd4-b0e8-41a4-ab97-1f658052748b
keywords:
- WDM 音频驱动程序 WDK，延迟
- 音频驱动程序 WDK，延迟
- 波次输出延迟 WDK 音频
- 延迟 WDK 音频、 批输出的数据流
- WDK 音频进行流式处理延迟
- 输出延迟 WDK 音频
- 硬件延迟 WDK 音频
- 软件延迟 WDK 音频
- 混合延迟问题 WDK 音频
- DirectSound WDK 音频，延迟
- 资源不足 WDK 音频
- 时间 WDK 音频
- 缓冲区 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb597f123eaa0992204f0b7125f13fcc389d1598
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554043"
---
# <a name="factors-governing-wave-output-latency"></a>用于管理波次输出延迟的因素


## <span id="factors_governing_wave_output_latency"></span><span id="FACTORS_GOVERNING_WAVE_OUTPUT_LATENCY"></span>


本部分介绍 wave 输出流的延迟的源。 下面是一些会影响滞后时间的因素：

-   流是输出到 WaveCyclic 或 WavePci 设备

-   DirectSound 是否生成流或**waveOut** API

讨论了以下主题：

[WaveCyclic 延迟](wavecyclic-latency.md)

[WavePci 延迟](wavepci-latency.md)

[避免数据复制](avoiding-data-copying.md)

 

 





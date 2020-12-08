---
title: 控制 Wave 输出延迟的因素
description: 控制 Wave 输出延迟的因素
keywords:
- WDM 音频驱动程序 WDK，延迟
- 音频驱动程序 WDK，延迟
- 波形输出延迟 WDK 音频
- 延迟 WDK 音频，波形输出流
- 流延迟 WDK 音频
- 输出延迟 WDK 音频
- 硬件延迟 WDK 音频
- 软件延迟 WDK 音频
- 混合延迟问题 WDK 音频
- DirectSound WDK 音频，延迟
- 音质音频不足
- 时间 WDK 音频
- 缓冲 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2969c64ebd48b732d5332dcf198eb887e6fc4e26
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784809"
---
# <a name="factors-governing-wave-output-latency"></a>控制 Wave 输出延迟的因素


## <span id="factors_governing_wave_output_latency"></span><span id="FACTORS_GOVERNING_WAVE_OUTPUT_LATENCY"></span>


本部分介绍了波形输出流的延迟源。 影响延迟的一些因素包括：

-   流是输出到 WaveCyclic 还是 WavePci 设备

-   流是由 DirectSound 还是 **waveOut** API 生成

本文讨论了以下主题：

[WaveCyclic 延迟](wavecyclic-latency.md)

[WavePci 延迟](wavepci-latency.md)

[避免数据复制](avoiding-data-copying.md)

 

 





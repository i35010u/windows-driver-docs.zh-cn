---
title: 针对 DirectMusic 的驱动程序支持
description: 针对 DirectMusic 的驱动程序支持
ms.assetid: 48f6245e-0911-46b6-9cf9-ea4db8875021
keywords:
- DirectMusic WDK 音频
- 音频驱动程序 WDK DirectMusic
- 合成器 WDK 音频
- 批接收器 WDK 音频
- WDM 音频驱动程序 WDK DirectMusic
- Dmu WDK 音频
- 合成器接收器 WDK 音频
- 呈现接收器 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 75c3a4b60205a85ca4432980cede12c02c874ca8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333740"
---
# <a name="driver-support-for-directmusic"></a>针对 DirectMusic 的驱动程序支持


## <span id="driver_support_for_directmusic"></span><span id="DRIVER_SUPPORT_FOR_DIRECTMUSIC"></span>


本文档适用于实现 Microsoft DirectMusic 合成器 (synths) 的驱动程序的设计指南和批接收器：

-   合成器是输入的时间戳 MIDI 消息流，并输出模拟音频信号或定期采样波次的数字音频流的设备。

-   批接收器是流式处理的批设备，从合成器提取波形音频示例并馈送到目标音频设备。

可以在用户模式下实现软件 synths 和批接收器。 可以在内核模式下实现提供相同的功能的软件或硬件组件。 有关 synths 和批接收器之间的关系的详细信息，请参阅[合成和批接收器](synthesizers-and-wave-sinks.md)。 有关 DirectMusic API 的信息，请参阅 Microsoft Windows SDK 文档。

此设计指南包含以下部分：

[DirectMusic DDI 概述](directmusic-ddi-overview.md)

[在用户模式下的自定义呈现](custom-rendering-in-user-mode.md)

[内核模式硬件加速 DDI](kernel-mode-hardware-acceleration-ddi.md)

 

 





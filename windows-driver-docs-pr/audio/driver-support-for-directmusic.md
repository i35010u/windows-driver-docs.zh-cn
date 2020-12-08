---
title: 针对 DirectMusic 的驱动程序支持
description: 针对 DirectMusic 的驱动程序支持
keywords:
- DirectMusic WDK 音频
- 音频驱动程序 WDK，DirectMusic
- 合成 WDK 音频
- 波形接收器音频
- WDM 音频驱动程序 WDK，DirectMusic
- Dmu WDK 音频
- 合成接收器音频
- 呈现接收器 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a5d836cadb57e908f06202212b961cb9d7054fb5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789249"
---
# <a name="driver-support-for-directmusic"></a>针对 DirectMusic 的驱动程序支持


## <span id="driver_support_for_directmusic"></span><span id="DRIVER_SUPPORT_FOR_DIRECTMUSIC"></span>


本文档介绍了如何实现适用于 Microsoft DirectMusic 合成 (synths) 和波形接收器的驱动程序的设计指南：

-   合成器是一种设备，可输入带有时间戳的 MIDI 消息的流，并输出模拟音频信号或定期采样的波形数字音频流。

-   波形接收器是一种流式处理 wave 设备，可从合成器中提取 wave 音频样本，并将其送入目标音频设备。

可以在用户模式下实现软件 synths 和波形接收器。 提供相同功能的软件或硬件组件可以在内核模式下实现。 有关 synths 与波形接收器之间的关系的详细信息，请参阅 [合成和波形接收器](synthesizers-and-wave-sinks.md)。 有关 DirectMusic API 的信息，请参阅 Microsoft Windows SDK 文档。

本设计指南包含以下部分：

[DirectMusic DDI 概述](directmusic-ddi-overview.md)

[用户模式下的自定义呈现](custom-rendering-in-user-mode.md)

[内核模式硬件加速 DDI](kernel-mode-hardware-acceleration-ddi.md)

 

 





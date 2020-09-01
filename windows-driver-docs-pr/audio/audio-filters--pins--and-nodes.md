---
title: 音频筛选器、引脚和节点
description: 音频筛选器、引脚和节点
ms.assetid: 5f30703c-bf33-49bb-bce2-990ad5b54a9c
keywords:
- WDM 音频驱动程序 WDK，筛选器
- 音频驱动程序 WDK，筛选器
- WDM 音频驱动程序 WDK，pin
- 音频驱动程序 WDK，pin
- WDM 音频驱动程序 WDK，节点
- 音频驱动程序 WDK，节点
- 筛选 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e6a098199e3f39cbf2e819e85af38d8d055fa113
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208341"
---
# <a name="audio-filters-pins-and-nodes"></a>音频筛选器、引脚和节点


## <span id="audio_filters_pins_and_nodes"></span><span id="AUDIO_FILTERS_PINS_AND_NODES"></span>


Microsoft Windows 驱动模型 (WDM) 适配器驱动程序将其音频硬件公开为一组筛选器工厂，其中每个工厂都可以创建一个或多个筛选器实例。 内核流式传输 (KS) filter 对象可以封装音频硬件功能，该功能可对通过筛选器进行流式处理的声波音频数据执行某种类型的数字处理。 例如，筛选器可能会对流进行呈现或合成操作，也可能会将回响添加到流中。

筛选器实例公开 pin 工厂，其中每个工厂都可以创建一个或多个 pin 实例。 这些 pin 可以连接到其他筛选器的 pin，以生成筛选器关系图。 若要成为音频筛选器关系图的一部分，筛选器必须有一个或多个固定实例。

Pin 表示数据流进入或退出筛选器时所用的输入或输出连接点。 每个 pin 均指定它可以支持的数据格式范围，并且只有具有兼容格式的流可以流过该 pin。

WDM 音频设备的筛选器以节点和连接的形式公开其内部拓扑。

拓扑节点位于通过筛选器传递的数据路径上。 节点表示筛选器中的控制点。 每个节点都以逻辑方式封装筛选器功能的模块化块，并对通过节点的数据流执行数字信号处理。 节点可能表示可以在 "软件控制" 下调整的音量控件。

Filter 对象还指定了其不同的 pin 与节点之间的连接。 这些连接中的隐式是通过筛选器沿每个数据路径对节点进行排序。

本部分介绍特定于 WDM 音频驱动程序的筛选器、pin 和节点的功能。 本文讨论了以下主题：

[音频筛选器](audio-filters.md)

[筛选器工厂](filter-factories.md)

[引脚工厂](pin-factories.md)

[节点和连接](nodes-and-connections.md)

[音频筛选器图](audio-filter-graphs.md)

[滤波器](wave-filters.md)

[MIDI 和 DirectMusic 筛选器](midi-and-directmusic-filters.md)

[拓扑筛选器](topology-filters.md)

有关内核流式处理筛选器、pin 和节点的更多常规讨论，请参阅 [KS 微型驱动程序体系结构](../stream/ks-minidriver-architecture.md)。

 


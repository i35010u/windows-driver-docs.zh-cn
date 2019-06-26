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
- 筛选器 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 59d24d6a79619703afa2f2d3e0cb13b475f014fb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355690"
---
# <a name="audio-filters-pins-and-nodes"></a>音频筛选器、引脚和节点


## <span id="audio_filters_pins_and_nodes"></span><span id="AUDIO_FILTERS_PINS_AND_NODES"></span>


Microsoft Windows 驱动程序模型 (WDM) 适配器驱动程序将作为筛选器工厂，其中每个可以创建一个或多个筛选器实例的集合公开其音频硬件。 流式处理 (KS) 筛选器对象是内核可以封装执行某种类型的数字处理的波形音频数据，以流式传输通过筛选器的音频硬件函数。 例如，可能会执行筛选器，呈现或合成一个流，或它可能会向流中添加混响。

筛选器实例公开 pin 工厂，其中每个可以创建一个或多个 pin 实例。 这些引脚可连接到其他筛选器来生成筛选器图形的 pin。 若要音频筛选器图形的一部分，筛选器必须具有一个或多个 pin 实例。

Pin 表示通过该数据流进入或退出该筛选器的输入或输出的连接点。 每个插针指定数据格式，它可以支持，并且仅具有兼容的格式的流可以流过 pin 的范围。

用于 WDM 音频设备的筛选器公开其内部形式的节点和连接拓扑。

拓扑节点位于通过筛选器的数据路径上。 一个节点表示的控件在筛选器内的点。 每个节点以逻辑方式封装模块化块的筛选器的功能，并对通过节点的数据流执行数字信号处理。 节点可能表示音量控制，例如，可以在软件控制下进行调整。

筛选器对象还指定了不同的 pin 和节点之间的连接。 在这些连接中隐式是通过筛选器的每个数据路径上的节点的顺序。

本部分提供的筛选器、 pin 和特定于 WDM 音频驱动程序的节点的功能。 论述了以下主题：

[音频筛选器](audio-filters.md)

[筛选器工厂](filter-factories.md)

[Pin 工厂](pin-factories.md)

[节点和连接](nodes-and-connections.md)

[音频筛选器关系图](audio-filter-graphs.md)

[批筛选器](wave-filters.md)

[MIDI 和 DirectMusic 筛选器](midi-and-directmusic-filters.md)

[拓扑筛选器](topology-filters.md)

内核流式处理筛选器、 pin 和节点，请参阅更多常规讨论[KS 微型驱动程序体系结构](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-minidriver-architecture)。

 

 





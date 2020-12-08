---
title: 音频筛选器
description: 音频筛选器
keywords:
- 音频筛选器 WDK 音频
- 音频筛选 WDK 音频，关于音频筛选器
- 筛选 WDK 音频，关于音频筛选器
- KS 筛选 WDK 音频
- KS 筛选 WDK 音频，关于 KS 筛选器
- 接收器引脚 WDK 音频
- 源引脚 WDK 音频
- Irp WDK 音频
- 中断服务例程 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9660fe1d9178d813dc30952e1a827d299cea3e48
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784993"
---
# <a name="audio-filters"></a>音频筛选器


## <span id="audio_filters"></span><span id="AUDIO_FILTERS"></span>


KS 筛选器是一个内核对象，由内核对象句柄标识。 在下图中，中心中的大框是代表音频设备的 KS 筛选器。 数据流从左侧流向筛选器，传递几个节点进行处理，并退出右侧的筛选器。 筛选器是由筛选器工厂创建的，筛选器工厂在筛选器的底部显示为带有虚线边缘的框。

![阐释包含两个节点的 ks 筛选器的关系图](images/filter-1.png)

在该图中，在筛选器上实例化两个针脚。 左侧的 pin 是数据接收器，右侧的 pin 是数据源。 数据通过接收器 pin 流入筛选器并通过源 pin 流出筛选器。

按照约定，在 KS 中术语 "源" 和 "接收器" 的使用是以缓冲为中心的 (或更普遍的以连接为中心的) 。 在一个筛选器上的源插针连接到另一个筛选器的接收器 pin 时，通常需要数据缓冲区。 缓冲区以数据从源插针传入的速率进行了不规则，并退出接收器 pin。 当然 (，并非所有连接都需要缓冲。 同一适配器卡上两个设备之间可能会发生 bufferless 连接，例如，接收器和源数据速率更易于匹配。 ) 

与此相反，用于 SRC 和 DST (源和目标) 混合器行的混音器 API 术语是以设备为中心的：

-   流通过 SRC 混合器行进入混音器设备。

-   流通过 DST 混合器行退出混音器设备。

换句话说，SRC 混合器行映射到 KS 筛选器上的数据接收器 pin，而 DST 混合器行映射到数据源 pin。 有关详细信息，请参阅 [音频混音器 API 转换的内核流拓扑](kernel-streaming-topology-to-audio-mixer-api-translation.md)。

为了简单起见，该图省略了用于创建 pin 实例的筛选器的 pin 工厂。

除了数据接收器和数据源外，pin 和筛选器还可以是 IRP 接收器和 IRP 源。 不仅可以固定和筛选器接收 Irp，还可以发送 Irp。 图中的三个深色箭头表示 Irp。 图左侧的固定为 IRP 接收器。 右侧的 pin 是 IRP 源。 该图还显示了发送到筛选器对象本身的 IRP。

 

 





---
title: 音频筛选器
description: 音频筛选器
ms.assetid: d4b14327-2870-4d4d-a575-68725421da95
keywords:
- 音频筛选器 WDK 音频
- 音频筛选器 WDK 音频，有关音频筛选器
- 筛选器 WDK 音频，有关音频筛选器
- KS WDK 音频筛选器
- KS 筛选器 WDK 音频，有关 KS 筛选器
- 接收器 pin WDK 音频
- 源 pin WDK 音频
- Irp WDK 音频
- 中断服务例程 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6eae436b51d591876cd89d158adb7a10b1109757
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575351"
---
# <a name="audio-filters"></a>音频筛选器


## <span id="audio_filters"></span><span id="AUDIO_FILTERS"></span>


KS 筛选器是一个内核对象，由内核对象句柄。 在下图中，在中心中的大型框是代表一个音频设备 KS 筛选器。 数据流输入到筛选器从左侧通过几个节点以进行处理，并在右侧退出筛选器。 筛选器创建的筛选器工厂，与在筛选器的底部虚线边缘显示为一个框。

![说明具有两个节点的 ks 筛选器的关系图](images/filter-1.png)

在图中，两个 pin 被实例化筛选器。 在左侧的 pin 是数据接收器，并在右侧的 pin 是数据源。 数据流入通过接收器 pin 和流出源 pin 通过筛选器的筛选器。

按照惯例，条款源和接收器 KS 中的使用情况是缓冲区为中心 (或这样一来，更普遍的情况，以连接为中心)。 经常需要源 pin 上一个筛选器连接到另一个接收器 pin 的点处的数据缓冲区。 缓冲区平滑处理，从而扩展中的数据来自源 pin 并退出到接收器 pin 的速率的异常。 （当然，并非所有连接都需要缓冲。 无需缓冲区的连接可能会出现更轻松地匹配接收器和源数据费率相同适配器卡，例如，两个设备之间。）

与此相反，SRC 和 DST （源和目标） 混音器行的混音器 API 的术语是以设备为中心：

-   该流将进入 mixer 设备通过 SRC 混音器行。

-   流退出 mixer 设备通过 DST 混音器行。

换而言之，SRC mixer 行映射到数据接收器 pin KS 筛选器和 DST mixer 行映射到一个数据源的 pin。 有关详细信息，请参阅[音频 Mixer API 转换到内核流式处理拓扑](kernel-streaming-topology-to-audio-mixer-api-translation.md)。

为简单起见，该图将忽略创建 pin 实例的筛选器的 pin 工厂。

除了数据接收器和数据源，IRP 接收器和 IRP 源，则也可以是插针和筛选器。 不仅可以插针和筛选器接收 Irp-它们也可以发送 Irp。 在图中的三个深色箭头表示 Irp。 图左侧 pin 是 IRP 接收器。 在右侧 pin 是 IRP 源。 该图还显示 IRP 发送到筛选器对象本身。

 

 





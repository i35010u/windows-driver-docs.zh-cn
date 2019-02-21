---
title: 数据交集处理程序
description: 数据交集处理程序
ms.assetid: 7206afdb-8a34-4b5a-8cea-87119f426161
keywords:
- WDM 音频驱动程序 WDK，数据交集处理程序
- 音频驱动程序 WDK，数据交集处理程序
- 数据交集处理程序 WDK 音频
- 处理程序 WDK 音频
- 虚拟音频设备 WDK
- 音频筛选器 WDK 音频数据交集处理程序
- 筛选 WDK 音频数据交集处理程序
- 格式 WDK 音频数据交集处理程序
- pin WDK 音频数据交集处理程序
- 关系图 WDK 音频
- 范围交集 WDK 音频
- 数据范围 WDK 音频交集
- WDK 的音频数据格式
- 音频数据范围 WDK
- 端口驱动程序 WDK 音频数据交集处理程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c35d9e78a4049ab989b137ac5600005b0829528
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545053"
---
# <a name="data-intersection-handlers"></a>数据交集处理程序


## <span id="data_intersection_handlers"></span><span id="DATA_INTERSECTION_HANDLERS"></span>


本部分介绍在 Microsoft Windows 驱动程序模型 (WDM) 音频驱动程序中的数据交叉处理程序。 一般情况下筛选数据交集 KS 处理的更广泛介绍，请参阅[AVStream DataRange 结合](https://msdn.microsoft.com/library/windows/hardware/ff558680)。

在较旧版本的 Windows，如 Windows XP [SysAudio 系统驱动程序](kernel-mode-wdm-audio-components.md#sysaudio_system_driver)构造[虚拟音频设备](virtual-audio-devices.md)通过连接到窗体一起对音频筛选器的 pin[音频筛选器图形](audio-filter-graphs.md)。 上一个筛选器的源 pin 可以连接到另一个接收器 pin 之前，SysAudio 必须协商两个 pin 可用于交换数据的通用格式。 此协商的详细信息很大程度上都委托给在单独的筛选器中实现的数据交叉处理程序。

同样，在 Windows Vista 及更高版本，音频引擎必须协商批筛选器表示音频呈现设备中的数据交叉处理程序的常见流格式。

适配器驱动程序在从 Portcls.sys 中创建到相应端口驱动程序的绑定之一的微型端口驱动程序将音频设备的 WaveRT 筛选器。 端口驱动程序包含默认的数据交叉处理程序，但默认处理程序的第一个机会来确定一种通用格式始终都提供微型端口驱动程序的专有数据交集处理程序。 如果专有的处理程序拒绝这一机会，但是，端口驱动程序的默认处理程序确定的格式。

端口驱动程序的默认数据交集处理程序用于处理最常见的硬件功能。 对于简单的音频设备，默认处理程序提供一个便捷替代方式，到在适配器驱动程序中实现专有的处理程序。 但是，有更高级的功能的适配器可能需要专有的处理程序，以便公开硬件的完整功能。

本部分的其余部分介绍了一些端口驱动程序的默认数据交集处理程序的限制，并呈现设计方案的适配器驱动程序的专有数据交集处理程序所需的技术。 讨论了以下主题：

[数据交集](data-intersection.md)

[默认数据交集的处理程序](default-data-intersection-handlers.md)

[专有数据交集处理程序](proprietary-data-intersection-handlers.md)

[采样频率的硬件约束](hardware-constraints-on-sample-frequency.md)

[输出缓冲区大小](output-buffer-size.md)

[具有离散值的数据范围](data-ranges-with-discrete-values.md)

[通配符](wild-cards.md)

[数据范围属性](data-range-properties.md)



 

 





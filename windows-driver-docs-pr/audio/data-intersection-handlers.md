---
title: 数据交集处理程序
description: 数据交集处理程序
keywords:
- WDM 音频驱动程序 WDK，数据交集处理程序
- 音频驱动程序 WDK，数据交集处理程序
- 数据交集处理程序 WDK 音频
- 处理程序 WDK 音频
- 虚拟音频设备 WDK
- 音频筛选 WDK 音频，数据交集处理程序
- 筛选 WDK 音频、数据交集处理程序
- 设置 WDK 音频、数据交集处理程序的格式
- 锁定 WDK 音频、数据交集处理程序
- 曲线图乐曲音频
- 范围交集 WDK 音频
- 数据范围 WDK 音频，交叉
- 音频数据格式 WDK
- 音频数据范围 WDK
- 端口驱动程序 WDK 音频，数据交集处理程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1d4129ce83ecaee07f9bd8362a36b4f9f616d340
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789321"
---
# <a name="data-intersection-handlers"></a>数据交集处理程序


## <span id="data_intersection_handlers"></span><span id="DATA_INTERSECTION_HANDLERS"></span>


本部分讨论 Microsoft Windows 驱动模型 (WDM) 音频驱动程序中的数据交集处理程序。 有关对 KS 筛选器的数据交集处理的更广泛讨论，请参阅 [AVStream 中的 DataRange 交集](../stream/data-range-intersections-in-avstream.md)。

在较旧版本的 Windows （如 Windows XP）中， [SysAudio 系统驱动程序](kernel-mode-wdm-audio-components.md#sysaudio_system_driver) 通过连接各种音频筛选器 pin 来构造一个 [虚拟音频设备](virtual-audio-devices.md) ，以形成 [音频筛选器图](audio-filter-graphs.md)。 在一个筛选器上的源 pin 可以连接到另一个筛选器的接收器 pin 之前，SysAudio 必须协商两个 pin 可用于交换数据的通用格式。 此协商的详细信息很大程度上会委托给在单个筛选器中实现的数据交集处理程序。

同样，在 Windows Vista 和更高版本中，音频引擎必须使用表示音频呈现设备的波形筛选器中的数据交集处理程序来协商公共流格式。

适配器驱动程序通过将其某个小型端口驱动程序绑定到 Portcls.sys 中的相应端口驱动程序，为音频设备创建 WaveRT 筛选器。 端口驱动程序包含默认的数据交集处理程序，但默认处理程序始终向微型端口驱动程序的专用数据交集处理程序提供第一次决定常见格式的机会。 但是，如果专有处理程序拒绝此机会，则端口驱动程序的默认处理程序将确定格式。

端口驱动程序的默认数据交集处理程序设计用于处理最常见的硬件功能。 对于简单的音频设备，默认处理程序提供了一种方便的替代方法来实现适配器驱动程序中的专有处理程序。 但是，具有更高级功能的适配器可能需要专有处理程序才能公开硬件的全部功能。

本部分的其余部分介绍了端口驱动程序的默认数据交集处理程序的一些限制，并提供了为适配器驱动程序设计专有数据交集处理程序所需的技术。 本文讨论了以下主题：

[数据交集](data-intersection.md)

[默认数据交集处理程序](default-data-intersection-handlers.md)

[专有数据交集处理程序](proprietary-data-intersection-handlers.md)

[采样频率的硬件约束](hardware-constraints-on-sample-frequency.md)

[输出缓冲区大小](output-buffer-size.md)

[具有离散值的数据范围](data-ranges-with-discrete-values.md)

[通配符](wild-cards.md)

[数据范围属性](data-range-properties.md)



 


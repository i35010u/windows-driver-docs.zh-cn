---
title: 音频的终结点、 属性和事件
description: 音频的终结点、 属性和事件
ms.assetid: ffc5834f-30c8-40b5-b57b-fe784331690c
keywords:
- 音频事件 WDK
- 音频属性 WDK
- 端口驱动程序 WDK 音频，属性
- 端口驱动程序 WDK 音频，事件
- 适配器驱动程序 WDK 音频，事件
- 适配器驱动程序 WDK 音频，属性
- 音频属性 WDK，有关音频属性
- 有关音频事件的音频事件 WDK，
- WDM 音频属性 WDK
- WDM 音频事件 WDK
- WDM 音频属性 WDK，有关音频属性
- KS 属性 WDK 音频
- KS 事件 WDK 音频
- 属性 WDK 音频
- pin WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 27992b8952761b42a049e746ea329a2446297586
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543415"
---
# <a name="audio-endpoints-properties-and-events"></a>音频的终结点、 属性和事件


## <span id="audio_properties_and_events"></span><span id="AUDIO_PROPERTIES_AND_EVENTS"></span>


PortCls 系统驱动程序支持的内部函数中所述的操作子集[KS 属性、 事件和方法](https://msdn.microsoft.com/library/windows/hardware/ff567673)。

Portcls.sys 中的端口驱动程序支持的属性和事件通过提供的某些属性和事件的请求处理程序，并且其他请求转发到微型端口驱动程序的处理程序。

WaveCyclic、 WavePci、 MIDI 和 Dmu 端口驱动程序的当前实现提供以下信息：

-   支持的筛选器和其 pin 和节点属性

-   支持为插针和节点上的事件而不是筛选器上的事件

客户端可以指定筛选器或 pin 实例的句柄作为属性或事件请求的目标。 节点属性或事件的请求指定除了筛选器或 pin 的句柄的节点 ID。 有关详细信息，请参阅[筛选器、 Pin 和节点属性](filter--pin--and-node-properties.md)。

拓扑端口驱动程序提供以下功能：

-   对筛选器和它的节点上的属性的支持

-   对节点上的事件的支持

拓扑筛选器上的针表示永久存在，因此无法进行实例化或删除的硬编码连接。

无端口驱动程序是筛选器或其 pin 和节点上的方法提供支持。 端口驱动程序永远不会处理方法的请求，并且它们不会转发到微型端口驱动程序用于处理这些请求。

音频适配器驱动程序支持某些或所有以下标准属性集：

[KSPROPSETID\_AC3](https://msdn.microsoft.com/library/windows/hardware/ff537436)

[KSPROPSETID\_声学\_Echo\_取消](https://msdn.microsoft.com/library/windows/hardware/ff537438)

[KSPROPSETID\_Audio](https://msdn.microsoft.com/library/windows/hardware/ff537440)

[KSPROPSETID\_DirectSound3DBuffer](https://msdn.microsoft.com/library/windows/hardware/ff537447)

[KSPROPSETID\_DirectSound3DListener](https://msdn.microsoft.com/library/windows/hardware/ff537449)

[KSPROPSETID\_DrmAudioStream](https://msdn.microsoft.com/library/windows/hardware/ff537481)

[KSPROPSETID\_General](https://msdn.microsoft.com/library/windows/hardware/ff566576)

[KSPROPSETID\_Hrtf3d](https://msdn.microsoft.com/library/windows/hardware/ff537482)

[KSPROPSETID\_插孔](https://msdn.microsoft.com/library/windows/hardware/ff537484)

[KSPROPSETID\_Pin](https://msdn.microsoft.com/library/windows/hardware/ff566584)

[KSPROPSETID\_合成器](https://msdn.microsoft.com/library/windows/hardware/ff537486)

[KSPROPSETID\_合成器\_Dls](https://msdn.microsoft.com/library/windows/hardware/ff537488)

[KSPROPSETID\_TopologyNode](https://msdn.microsoft.com/library/windows/hardware/ff537491)

所有的音频驱动程序支持**KSPROPSETID\_音频**属性集。

一些音频适配器驱动程序支持以下事件组：

[KSEVENTSETID\_AudioControlChange](https://msdn.microsoft.com/library/windows/hardware/ff537122)

此外，音频适配器驱动程序是免费提供的其他属性集的标头文件 Ksmedia.h 中定义的属性处理程序。 驱动程序还可以定义并支持其自己的自定义属性和事件集，但知道有关自定义属性或事件的应用程序将能够使用它。

本部分介绍特定于音频的属性和事件。 它包含以下主题：

[音频属性请求](audio-property-requests.md)

[筛选器、 Pin 和节点属性](filter--pin--and-node-properties.md)

[音频属性处理程序](audio-property-handlers.md)

[基本支持查询的音频属性](basic-support-queries-for-audio-properties.md)

[音频的终结点生成器算法](audio-endpoint-builder-algorithm.md)

[动态子注册和注销](dynamic-subdeviceregistration-and-unregistration.md)

[公开多渠道的节点](exposing-multichannel-nodes.md)

[Pin Category 属性](pin-category-property.md)

[音频端点设备的友好名称](friendly-names-for-audio-endpoint-devices.md)

[音频位置属性](audio-position-property.md)

[固定数据区域和交集属性](pin-data-range-and-intersection-properties.md)

[Jack Description 属性](jack-description-property.md)

[麦克风阵列 Geometry 属性](microphone-array-geometry-property.md)

[硬件事件](hardware-events.md)

 

 





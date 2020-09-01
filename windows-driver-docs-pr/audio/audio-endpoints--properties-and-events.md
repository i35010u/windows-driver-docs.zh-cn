---
title: 音频终结点、属性和事件
description: 音频终结点、属性和事件
ms.assetid: ffc5834f-30c8-40b5-b57b-fe784331690c
keywords:
- 音频事件 WDK
- 音频属性 WDK
- 端口驱动程序 WDK 音频，属性
- 端口驱动程序 WDK 音频，事件
- 适配器驱动程序 WDK 音频，事件
- 适配器驱动程序 WDK 音频，属性
- 音频属性 WDK，关于音频属性
- 音频事件 WDK，关于音频事件
- WDM 音频属性 WDK
- WDM 音频事件 WDK
- WDM 音频属性 WDK，关于音频属性
- KS 属性 WDK 音频
- KS 事件 WDK 音频
- 属性 WDK 音频
- 锁定 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 369475358455bab13f7b18962495425ae5108e05
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208327"
---
# <a name="audio-endpoints-properties-and-events"></a>音频终结点、属性和事件


## <span id="audio_properties_and_events"></span><span id="AUDIO_PROPERTIES_AND_EVENTS"></span>


PortCls 系统驱动程序支持 [KS 属性、事件和方法](../stream/ks-properties--events--and-methods.md)中所述的内部操作的子集。

Portcls.sys 中的端口驱动程序通过为某些属性和事件请求提供处理程序，并将其他请求转发给微型端口驱动程序的处理程序，来支持属性和事件。

WaveCyclic、WavePci、MIDI 和 Dmu 端口驱动程序的当前实现提供以下各项：

-   对筛选器及其 pin 和节点的属性的支持

-   支持引脚和节点上的事件，但不支持筛选器上的事件

客户端可以指定筛选器或 pin 实例的句柄，作为属性或事件请求的目标。 节点属性或事件的请求除了指定筛选器或固定句柄外，还指定节点 ID。 有关详细信息，请参阅 [筛选器、固定和节点属性](filter--pin--and-node-properties.md)。

拓扑端口驱动程序提供以下内容：

-   支持筛选器及其节点上的属性

-   支持节点上的事件

拓扑筛选器上的 pin 表示永久存在并且无法实例化或删除的硬编码连接。

端口驱动程序都不提供对筛选器或其 pin 和节点上的方法的支持。 端口驱动程序从不处理方法请求，它们永远不会将这些请求转发给微型端口驱动程序进行处理。

音频适配器驱动程序支持以下部分或全部标准属性集：

[KSPROPSETID \_ e-ac3](./kspropsetid-ac3.md)

[KSPROPSETID \_ 回声 \_ \_ 取消](./kspropsetid-acoustic-echo-cancel.md)

[KSPROPSETID \_ 音频](./kspropsetid-audio.md)

[KSPROPSETID \_ DirectSound3DBuffer](./kspropsetid-directsound3dbuffer.md)

[KSPROPSETID \_ DirectSound3DListener](./kspropsetid-directsound3dlistener.md)

[KSPROPSETID \_ DrmAudioStream](./kspropsetid-drmaudiostream.md)

[KSPROPSETID \_ 常规](../stream/kspropsetid-general.md)

[KSPROPSETID \_ Hrtf3d](./kspropsetid-hrtf3d.md)

[KSPROPSETID \_ 插座](./kspropsetid-jack.md)

[KSPROPSETID \_ Pin](../stream/kspropsetid-pin.md)

[KSPROPSETID \_ 合成](./kspropsetid-synth.md)

[KSPROPSETID \_ 合成 \_ dl](./kspropsetid-synth-dls.md)

[KSPROPSETID \_ TopologyNode](./kspropsetid-topologynode.md)

所有音频驱动程序均支持 **KSPROPSETID \_ audio** 属性集。

某些音频适配器驱动程序支持以下事件集：

[KSEVENTSETID \_ AudioControlChange](./kseventsetid-audiocontrolchange.md)

此外，可以为头文件 Ksmedia 中定义的其他属性集免费提供音频适配器驱动程序。 驱动程序还可以定义和支持自己的自定义属性和事件集，但只有知道自定义属性或事件的应用程序才能使用它。

本节讨论特定于音频的属性和事件。 本节包含以下主题：

[音频属性请求](audio-property-requests.md)

[筛选器、引脚和节点属性](filter--pin--and-node-properties.md)

[音频属性处理程序](audio-property-handlers.md)

[音频属性的基本支持查询](basic-support-queries-for-audio-properties.md)

[音频终结点生成器算法](audio-endpoint-builder-algorithm.md)

[动态子设备注册和注销](dynamic-subdeviceregistration-and-unregistration.md)

[公开多声道节点](exposing-multichannel-nodes.md)

[引脚类别属性](pin-category-property.md)

[音频终结点设备的友好名称](friendly-names-for-audio-endpoint-devices.md)

[音频位置属性](audio-position-property.md)

[引脚数据范围和交集属性](pin-data-range-and-intersection-properties.md)

[插孔说明属性](jack-description-property.md)

[麦克风阵列几何属性](microphone-array-geometry-property.md)

[硬件事件](hardware-events.md)

 


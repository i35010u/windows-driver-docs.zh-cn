---
title: 音频属性请求
description: 音频属性请求
ms.assetid: dcfd139c-fca3-4068-8324-aa2c952dbc1f
keywords:
- 音频属性 WDK，请求
- WDM 音频属性 WDK，请求
- 筛选 WDK 音频属性请求
- 节点 WDK 音频属性请求
- pin WDK 音频属性请求
- KS WDK 音频筛选器、 属性请求
- overspecified 的请求 WDK 音频
- underspecified 的请求 WDK 音频
- 筛选 WDK 音频描述符
- 属性请求 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ab33e12650ed7a04f1e4e5a2e6b939b49de891c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355654"
---
# <a name="audio-property-requests"></a>音频属性请求


## <span id="audio_property_requests"></span><span id="AUDIO_PROPERTY_REQUESTS"></span>


Microsoft Windows 驱动程序模型 (WDM) 的音频驱动程序的客户端可以将请求发送[KS 属性](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-properties)KS 筛选器和驱动程序已实例化的 pin。 例如，用户模式下客户端可以发送 KS 属性请求，通过调用[ **DeviceIoControl** ](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)起作用 （请参阅 Microsoft Windows SDK 文档） IOCTL 到 O 控制代码\_KS\_属性。 此函数将发送 IRP 包含对指定的筛选器或 pin 对象的属性请求。

音频驱动程序属性上支持 get、 set 和 basic 支持请求 (KSPROPERTY\_类型\_GET、 KSPROPERTY\_类型\_集和 KSPROPERTY\_类型\_BASICSUPPORT)。 有关详细信息，请参阅[音频驱动程序的属性集](https://docs.microsoft.com/windows-hardware/drivers/audio/audio-drivers-property-sets)。

客户端可以发送三种类型的属性的请求： 筛选器属性、 pin 属性和节点属性。 有关详细信息，请参阅[筛选器、 Pin 和节点属性](filter--pin--and-node-properties.md)。

客户端将筛选器属性请求发送给筛选器对象，其实例句柄通过指定目标筛选器 (请参阅[筛选器工厂](filter-factories.md))。 同样，将 pin 属性请求发送给 pin 对象，则目标 pin 指定通过其实例句柄 (请参阅[Pin 工厂](pin-factories.md))。 包含请求的任何一种[ **KSPROPERTY** ](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))结构，它指定以下：

-   标识属性集的 GUID

-   设置标识中指定的属性的属性项的索引

-   这些标志指示的属性请求 (get、 集，或者 basic 支持) 的类型

相关的属性中收集在一起以形成一个属性设置。 通过其属性设置并指定其组中的位置的索引标识的特定属性。

节点属性请求包含[ **KSNODEPROPERTY** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty)结构，它结合了 KSPROPERTY 结构和一个节点 id。 具体取决于节点属性，属性请求的目标是筛选器实例或 pin 实例。

如果筛选器可以创建多个特定节点类型的实例，由固定句柄指定请求的目标。 句柄标识的开头或末尾节点实例所驻留的数据路径的 pin 实例。 在包含的总和或 MUX 节点的筛选器的情况下 (请参阅[ **KSNODETYPE\_SUM** ](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-sum)并[ **KSNODETYPE\_MUX** ](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-mux))，则适用以下规则：

-   如果该属性属于存在于一个接收器 （输入） 的 pin 的下游和上游的总和或 MUX 节点从一个节点，属性请求发送到接收器插针。

-   如果该属性属于存在于求和或 MUX 节点的下游和上游源 （输出） pin 从一个节点，属性请求发送到源插针。 （此外，求和或 MUX 节点的属性请求发送到源 pin。）

这些约定，可以唯一地标识特定的数据路径上的特定节点。

有关使用 mixer API 遍历数据路径中的节点的信息，请参阅[音频 Mixer API 转换到内核流式处理拓扑](kernel-streaming-topology-to-audio-mixer-api-translation.md)。

 

 





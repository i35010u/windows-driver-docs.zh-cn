---
title: 音频属性请求
description: 音频属性请求
keywords:
- 音频属性 WDK，请求
- WDM 音频属性 WDK，请求
- 筛选 WDK 音频，属性请求
- 节点 WDK 音频，属性请求
- 锁定 WDK 音频，属性请求
- KS 筛选 WDK 音频，属性请求
- overspecified 请求 WDK 音频
- underspecified 请求 WDK 音频
- 筛选 WDK 音频、描述符
- 属性请求 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2730228c1c18072218f66f9ed2f0a77fba16c9ce
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784961"
---
# <a name="audio-property-requests"></a>音频属性请求


## <span id="audio_property_requests"></span><span id="AUDIO_PROPERTY_REQUESTS"></span>


Microsoft Windows 驱动模型 (WDM) 音频驱动程序的客户端可以将 [ks 属性](../stream/ks-properties.md) 请求发送到 ks 筛选器，并将该驱动程序实例化。 例如，用户模式客户端可以通过调用 [**DeviceIoControl**](/windows/win32/api/ioapiset/nf-ioapiset-deviceiocontrol) 函数发送 KS 属性请求 (参阅 Microsoft Windows SDK 文档) 和 IOCTL KS 属性的 i/o 控制代码 \_ \_ 。 此函数将包含属性请求的 IRP 发送到指定的筛选器或固定对象。

音频驱动程序支持获取、设置和基本-支持 (KSPROPERTY \_ 类型 \_ GET、KSPROPERTY \_ 类型 \_ 集和 KSPROPERTY \_ 类型 \_ BASICSUPPORT) 的属性的请求。 有关详细信息，请参阅 [音频驱动程序属性集](./audio-drivers-property-sets.md)。

客户端可以发送对三种属性的请求：筛选器属性、pin 属性和节点属性。 有关详细信息，请参阅 [筛选器、固定和节点属性](filter--pin--and-node-properties.md)。

向筛选器对象发送筛选器属性请求时，客户端将通过其实例句柄来指定目标筛选器 (请参阅 [筛选器工厂](filter-factories.md)) 。 同样，将 pin 属性请求发送到 pin 对象时，目标 pin 由其实例句柄指定 (参阅) [固定工厂](pin-factories.md) 。 任一类型的请求都包含一个指定以下内容的 [**KSPROPERTY**](/previous-versions/ff564262(v=vs.85)) 结构：

-   标识属性集的 GUID

-   标识指定属性集中的属性项的索引

-   指示属性请求的类型的标志 (获取、设置或基本支持) 

相关属性一起收集以构成属性集。 特定属性由其属性集和指定其在该集中的位置的索引标识。

节点属性请求包含 [**KSNODEPROPERTY**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty) 结构，该结构结合了 KSPROPERTY 结构和节点 ID。 根据 node 属性，属性请求的目标是筛选器实例或 pin 实例。

如果筛选器可以创建一个特定节点类型的多个实例，则该请求的目标通过 pin 句柄来指定。 该句柄标识节点实例所在的数据路径开头或结尾处的固定实例。 对于包含 SUM 或 MUX 节点的筛选器 (参阅 [**KSNODETYPE \_ SUM**](./ksnodetype-sum.md) and [**KSNODETYPE \_ MUX**](./ksnodetype-mux.md)) ，以下规则适用：

-   如果该属性属于来自接收器的下游节点 (输入) 从 SUM 或 MUX 节点传输和上游，则会将该属性请求发送到接收器 pin。

-   如果属性属于来自 SUM 或 MUX 节点的下游节点，并且源 (输出) 固定，则会将属性请求发送到源 pin。  (还会将 SUM 或 MUX 节点的属性请求发送到源插针。 ) 

使用这些约定，特定数据路径上的特定节点可以唯一地标识。

有关使用混音器 API 遍历数据路径中的节点的信息，请参阅 [音频混音器 Api 转换的内核流拓扑](kernel-streaming-topology-to-audio-mixer-api-translation.md)。

 


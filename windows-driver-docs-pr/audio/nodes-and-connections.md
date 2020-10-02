---
title: 节点和连接
description: 节点和连接
ms.assetid: 829b1067-8246-49fc-94f1-4988e61defac
keywords:
- 音频筛选 WDK 音频、节点
- 音频筛选 WDK 音频，连接
- 音频拓扑节点 WDK
- 拓扑节点 WDK 音频
- 连接 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ed9039ea8d6cd96f50b1d3162c3775fa41ae16f
ms.sourcegitcommit: 372464be981a39781c71049126f36891cb5d0cad
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2020
ms.locfileid: "91646041"
---
# <a name="nodes-and-connections"></a>节点和连接


## <span id="nodes_and_connections"></span><span id="NODES_AND_CONNECTIONS"></span>


筛选器提供了其拓扑节点的描述，其形式为节点描述符 ([**PCNODE \_ 描述符**](/windows-hardware/drivers/ddi/portcls/ns-portcls-pcnode_descriptor) 结构) 的形式。 数组中的每个描述符描述单个节点，并且包含一个 GUID，用于指定节点类型 (例如， [**KSNODETYPE \_ 回音**](./ksnodetype-reverb.md)) 。 有关为音频设备定义的标准节点类型的列表，请参阅 [音频拓扑节点](./audio-topology-nodes.md)。

筛选器将通过描述符数组中节点的索引来标识其每个节点。 例如，将特定于节点的属性请求发送到筛选器或筛选器上的特定 pin 时，客户端会在请求中包含节点 ID (数组索引) ，以便标识目标节点。

该筛选器以连接描述符数组的形式提供其内部连接的说明 ([**PCCONNECTION \_ 描述符**](/windows-hardware/drivers/ddi/portcls/ns-portcls-_pcconnection_descriptor) 结构) 。 每个描述符描述了一个筛选器的内部连接。 描述符可以描述 pin 与节点之间的连接，或者两个节点之间的连接。

筛选器公开的节点和连接定义筛选器的内部拓扑。 拓扑是音频设备的内部布局的地图，应准确反映它所表示的硬件的组织。 例如，Microsoft Windows 多媒体混音器 API 将筛选器的内部连接转换为混合器行及其节点到混音器线条上的控件 (参阅 [将内核流式处理拓扑转换为音频混音器 API 转换](kernel-streaming-topology-to-audio-mixer-api-translation.md)) 。 筛选器内部拓扑中的任何错误都将反映在混音器的表示形式中，并可能会在使用混音器 API 的应用程序中导致错误或意外行为。

 


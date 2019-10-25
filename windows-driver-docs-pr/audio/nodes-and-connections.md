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
ms.openlocfilehash: 11eef7490ba213800714e50bcc355873772993f2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830350"
---
# <a name="nodes-and-connections"></a>节点和连接


## <span id="nodes_and_connections"></span><span id="NODES_AND_CONNECTIONS"></span>


该筛选器以节点描述符数组（[**PCNODE\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ns-portcls-pcnode_descriptor)结构）的形式提供其拓扑节点的说明。 数组中的每个描述符描述单个节点，并包含指定节点类型的 GUID （例如， [**KSNODETYPE\_回音**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-reverb)）。 有关为音频设备定义的标准节点类型的列表，请参阅[音频拓扑节点](https://docs.microsoft.com/windows-hardware/drivers/audio/audio-topology-nodes)。

筛选器将通过描述符数组中节点的索引来标识其每个节点。 例如，将特定于节点的属性请求发送到筛选器或筛选器上的特定 pin 时，客户端将在请求中包含节点 ID （数组索引）以标识目标节点。

该筛选器以连接描述符数组（[**PCCONNECTION\_描述符**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537688(v=vs.85))结构）的形式提供其内部连接的说明。 每个描述符描述了一个筛选器的内部连接。 描述符可以描述 pin 与节点之间的连接，或者两个节点之间的连接。

筛选器公开的节点和连接定义筛选器的内部拓扑。 拓扑是音频设备的内部布局的地图，应准确反映它所表示的硬件的组织。 例如，Microsoft Windows 多媒体混音器 API 将筛选器的内部连接转换为混音器线，并将其节点转换为混音器线条上的控件（请参阅[音频混音器 API 转换的内核流拓扑](kernel-streaming-topology-to-audio-mixer-api-translation.md)）。 筛选器内部拓扑中的任何错误都将反映在混音器的表示形式中，并可能会在使用混音器 API 的应用程序中导致错误或意外行为。

 

 





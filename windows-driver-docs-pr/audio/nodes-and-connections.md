---
title: 节点和连接
description: 节点和连接
ms.assetid: 829b1067-8246-49fc-94f1-4988e61defac
keywords:
- 音频筛选器 WDK 音频节点
- 音频筛选 WDK 音频连接
- 音频拓扑节点 WDK
- 拓扑节点 WDK 音频
- 连接 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc52e794fe859c4754cf7a70480760e97f307e09
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363214"
---
# <a name="nodes-and-connections"></a>节点和连接


## <span id="nodes_and_connections"></span><span id="NODES_AND_CONNECTIONS"></span>


筛选器提供其拓扑中的节点的节点描述符的数组的形式说明 ([**PCNODE\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/ns-portcls-pcnode_descriptor)结构)。 数组中的每个描述符描述单个节点，并包含指定的节点类型的 GUID (例如， [ **KSNODETYPE\_混响**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-reverb))。 为音频设备定义的标准节点类型的列表，请参阅[音频拓扑节点](https://docs.microsoft.com/windows-hardware/drivers/audio/audio-topology-nodes)。

筛选器通过描述符数组中的节点的索引来标识每个节点。 例如时特定于节点的属性请求发送到筛选器或筛选器上的特定 pin 时，, 客户端以便确定目标节点请求中包含的节点 ID （数组索引）。

筛选器提供的连接描述符的数组的形式在其内部连接的说明 ([**PCCONNECTION\_描述符**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537688(v=vs.85))结构)。 每个说明符所描述的多个筛选器的内部连接。 Pin 和节点之间的连接或两个节点之间的连接，或者可以描述一个描述符。

在节点与筛选器一起提供的连接定义筛选器的内部拓扑。 拓扑是音频设备的内部布局的映射，并应准确反映的硬件，它表示组织。 Microsoft Windows 多媒体混音器 API，例如，转换成 mixer 行筛选器的内部连接和混音器行上的控件将其节点 (请参阅[音频 Mixer API 转换到内核流式处理拓扑](kernel-streaming-topology-to-audio-mixer-api-translation.md))。 筛选器的内部拓扑中错误的信息将反映在 mixer 行表示形式，并且可能导致错误或意外的行为使用混音器 API 的应用程序中。

 

 





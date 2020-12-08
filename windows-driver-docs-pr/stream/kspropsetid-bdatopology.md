---
title: KSPROPSETID \_ BdaTopology
description: KSPROPSETID \_ BdaTopology
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 276c0df5b8136ab6182e998fc58b7dd43a5f1532
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829137"
---
# <a name="kspropsetid_bdatopology"></a>KSPROPSETID \_ BdaTopology


## <span id="ddk_kspropsetid_bdatopology_ks"></span><span id="DDK_KSPROPSETID_BDATOPOLOGY_KS"></span>


KSPROPSETID \_ BdaTopology 为 BDA 拓扑属性集。 它用于查询有关其功能的筛选器。

以下属性可用：

<span id="KSPROPERTY_BDA_NODE_TYPES"></span><span id="ksproperty_bda_node_types"></span>[**KSPROPERTY \_ BDA \_ 节点 \_ 类型**](ksproperty-bda-node-types.md)  
返回节点类型的列表。

<span id="KSPROPERTY_BDA_PIN_TYPES"></span><span id="ksproperty_bda_pin_types"></span>[**KSPROPERTY \_ BDA \_ 引脚 \_ 类型**](ksproperty-bda-pin-types.md)  
返回 pin 类型的列表。

<span id="KSPROPERTY_BDA_TEMPLATE_CONNECTIONS"></span><span id="ksproperty_bda_template_connections"></span>[**KSPROPERTY \_ BDA \_ 模板 \_ 连接**](ksproperty-bda-template-connections.md)  
返回模板拓扑中的 pin 与节点之间的连接列表。

<span id="KSPROPERTY_BDA_NODE_METHODS"></span><span id="ksproperty_bda_node_methods"></span>[**KSPROPERTY \_ BDA \_ 节点 \_ 方法**](ksproperty-bda-node-methods.md)  
返回节点上支持的方法的列表。

<span id="KSPROPERTY_BDA_NODE_PROPERTIES"></span><span id="ksproperty_bda_node_properties"></span>[**KSPROPERTY \_ BDA \_ 节点 \_ 属性**](ksproperty-bda-node-properties.md)  
返回节点上支持的属性列表。

<span id="KSPROPERTY_BDA_NODE_EVENTS"></span><span id="ksproperty_bda_node_events"></span>[**KSPROPERTY \_ BDA \_ 节点 \_ 事件**](ksproperty-bda-node-events.md)  
返回节点上支持的事件列表。

<span id="KSPROPERTY_BDA_CONTROLLING_PIN_ID"></span><span id="ksproperty_bda_controlling_pin_id"></span>[**KSPROPERTY \_ BDA \_ 控制 \_ PIN \_ ID**](ksproperty-bda-controlling-pin-id.md)  
为 BDA 模板连接列表中的节点返回控制 pin。

<span id="KSPROPERTY_BDA_NODE_DESCRIPTORS"></span><span id="ksproperty_bda_node_descriptors"></span>[**KSPROPERTY \_ BDA \_ 节点 \_ 描述符**](ksproperty-bda-node-descriptors.md)  
返回节点的列表。

### <a name="comments"></a>注释

BDA 支持库提供了处理此属性集的默认方法。 网络提供程序筛选器使用此属性集来确定筛选器的模板拓扑，以及每个节点和 pin 支持的方法、属性和事件。 网络提供程序筛选器使用此节点和固定信息来确定筛选器可以对信号执行的操作类型，以及是否向图形添加筛选器。 筛选器的实际拓扑是指由网络提供程序实际在筛选器上进行的固定和节点连接。

此属性集中的属性定义筛选器可执行的操作。 通常情况下，不需要筛选器来截获这些属性中的任何一个。 有关详细信息，请参阅 [广播驱动程序体系结构微型驱动程序](./broadcast-driver-architecture-minidrivers.md) ，了解如何使用 bda 微型驱动程序 for 筛选器来提供这些属性的默认处理。 驱动程序编写器应创建允许处理此属性集的静态结构。 一旦创建了这些结构并将其注册到 BDA 支持库，驱动程序编写器就不需要执行任何进一步的操作来支持此属性集。

 


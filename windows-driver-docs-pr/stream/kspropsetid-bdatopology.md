---
title: KSPROPSETID\_BdaTopology
description: KSPROPSETID\_BdaTopology
ms.assetid: 26d67e68-56a9-4d36-9e33-6fb4486d7cd9
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d240bf2601d66448b2d6b66017fd313f7f509b9c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564582"
---
# <a name="kspropsetidbdatopology"></a>KSPROPSETID\_BdaTopology


## <span id="ddk_kspropsetid_bdatopology_ks"></span><span id="DDK_KSPROPSETID_BDATOPOLOGY_KS"></span>


KSPROPSETID\_BdaTopology 是 BDA 拓扑属性集。 它用于查询筛选器及其相关功能。

可用属性如下：

<span id="KSPROPERTY_BDA_NODE_TYPES"></span><span id="ksproperty_bda_node_types"></span>[**KSPROPERTY\_BDA\_NODE\_TYPES**](ksproperty-bda-node-types.md)  
返回节点类型的列表。

<span id="KSPROPERTY_BDA_PIN_TYPES"></span><span id="ksproperty_bda_pin_types"></span>[**KSPROPERTY\_BDA\_PIN\_TYPES**](ksproperty-bda-pin-types.md)  
返回 pin 类型的列表。

<span id="KSPROPERTY_BDA_TEMPLATE_CONNECTIONS"></span><span id="ksproperty_bda_template_connections"></span>[**KSPROPERTY\_BDA\_模板\_连接**](ksproperty-bda-template-connections.md)  
返回 pin 和模板拓扑中的节点之间的连接的列表。

<span id="KSPROPERTY_BDA_NODE_METHODS"></span><span id="ksproperty_bda_node_methods"></span>[**KSPROPERTY\_BDA\_节点\_方法**](ksproperty-bda-node-methods.md)  
返回的节点上所支持的方法列表。

<span id="KSPROPERTY_BDA_NODE_PROPERTIES"></span><span id="ksproperty_bda_node_properties"></span>[**KSPROPERTY\_BDA\_节点\_属性**](ksproperty-bda-node-properties.md)  
返回支持的节点上的属性列表。

<span id="KSPROPERTY_BDA_NODE_EVENTS"></span><span id="ksproperty_bda_node_events"></span>[**KSPROPERTY\_BDA\_节点\_事件**](ksproperty-bda-node-events.md)  
返回支持的节点上的事件列表。

<span id="KSPROPERTY_BDA_CONTROLLING_PIN_ID"></span><span id="ksproperty_bda_controlling_pin_id"></span>[**KSPROPERTY\_BDA\_控制\_PIN\_ID**](ksproperty-bda-controlling-pin-id.md)  
返回一个节点的控制 pin BDA 模板连接列表中。

<span id="KSPROPERTY_BDA_NODE_DESCRIPTORS"></span><span id="ksproperty_bda_node_descriptors"></span>[**KSPROPERTY\_BDA\_节点\_描述符**](ksproperty-bda-node-descriptors.md)  
返回节点的列表。

### <a name="comments"></a>备注

BDA 支持库提供用于处理设置此属性的默认方法。 网络提供程序筛选器使用此属性设置以确定筛选器，方法、 属性和支持每个节点和 pin 码的事件的模板拓扑。 网络提供程序筛选器使用此节点和 pin 信息来确定哪些类型的操作筛选器可以执行在信号，以及是否将筛选器添加到关系图。 筛选器的实际的拓扑结构是指通过网络提供商实际进行的筛选器的 pin 和节点连接。

此设置的属性中的属性定义筛选器可以执行的操作。 通常情况下，筛选器不需要截获任何这些属性。 有关详细信息，请参阅[广播驱动程序体系结构微型驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff556588)BDA 微型驱动程序筛选器如何使用 BDA 支持库的函数以提供这些属性的默认处理。 驱动程序编写器应创建的可以设置此属性的方式处理静态结构。 一旦这些结构是创建并注册到 BDA 支持库，驱动程序编写器不需要执行任何操作更进一步，支持设置此属性。

 

 






---
title: 确定 BDA 设备拓扑
description: 确定 BDA 设备拓扑
ms.assetid: fdac317e-d4fc-47c9-87d3-bec597f758f5
keywords:
- 方法设置 WDK BDA，BDA 设备拓扑
- 属性设置 WDK BDA，BDA 设备拓扑
- KSPROPERTY_BDA_NODE_TYPES
- KSPROPERTY_BDA_PIN_TYPES
- KSPROPERTY_BDA_TEMPLATE_CONNECTIONS
- 模板筛选器拓扑，WDK BDA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 56057682f986365397b299a70e1b4310099f1daa
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185405"
---
# <a name="determining-bda-device-topology"></a>确定 BDA 设备拓扑





BDA 设备拓扑由已连接的节点网络组成，其中每个节点都代表信号上的某种转换。 节点可以任意分组到不同的筛选器中。 这种任意分组为硬件供应商提供了在实现其硬件和驱动程序的方式上的特定自由，使此类硬件和驱动程序以通用方式与他们希望支持的不同类型的网络的网络提供程序协同工作。

要使这一任意分组体系结构正常工作，网络提供程序必须能够查询筛选器执行哪些类型的转换，这些筛选器会对信号执行何种类型的转换 (即，筛选器可支持的节点网络类型) 。 用于筛选器的底层环0微型驱动程序通过 [KSPROPSETID \_ BdaTopology](./kspropsetid-bdatopology.md) 属性集将其支持的节点网络的图片传达给网络提供商。

在确定筛选器的模板拓扑时，网络提供程序会循环访问节点类型和固定类型的列表，并在每个节点和固定其功能时进行查询。 网络提供程序使用 KSPROPSETID BdaTopology 的以下属性 \_ 来确定筛选器的模板拓扑：

-   KSPROPERTY \_ BDA \_ 节点 \_ 类型

    节点类型表示筛选器中可能的功能节点。 "KSPROPERTY \_ BDA \_ 节点 \_ 类型" 属性返回一个列表，其中列出了 BDA 微型驱动程序的筛选器实例提供的所有节点类型。 微型驱动程序分配任意值来标识节点类型。 通常，微型驱动程序使用微型驱动程序的节点类型列表中每个元素的索引作为每个节点类型的值。 BDA 微型驱动程序将节点说明 GUID 分配给每个节点类型。 *Bdamedia*中定义了网络提供程序当前支持的节点类型的说明 guid。 此节点说明向网络提供商指示节点的功能。 在模板拓扑中，节点类型只能出现一次。 不过，特定类型的多个节点可能具有相同的节点说明 GUID。 这允许在筛选器拓扑中的多个位置进行特定信号转换，同时允许网络提供程序明确标识单个拓扑节点。

-   KSPROPERTY \_ BDA \_ 引脚 \_ 类型

    固定类型表示关系图中其他筛选器的可能连接。 KSPROPERTY \_ BDA \_ 引脚 \_ types 属性返回可以在筛选器上创建的所有 PIN 类型的列表。 在模板拓扑中，pin 类型只能出现一次。

-   KSPROPERTY \_ BDA \_ 模板 \_ 连接

    KSPROPERTY \_ BDA \_ TEMPLATE \_ CONNECTIONS 属性返回一个数组，该数组表示可以在筛选器上配置的节点类型和固定类型之间的所有可能连接。 有关详细信息，请参阅 [映射连接拓扑](mapping-connection-topology.md) 。

首次创建筛选器实例并将其添加到关系图中时，它通常具有输入插针，但没有输出插针。 若要创建输出插针，网络提供程序首先使用 KSPROPSETID \_ BdaTopology 属性来确定筛选器可执行的操作。 通过这些属性，网络提供程序可确定需要筛选器对特定筛选器关系图执行的操作。 然后，网络提供程序使用 [KSMETHODSETID \_ BdaDeviceConfiguration](./ksmethodsetid-bdadeviceconfiguration.md) 方法集创建与特定 pin 类型匹配的输出插针，并创建内部拓扑（这是在这些针脚与输入插针之间的实际硬件路径）。 有关详细信息，请参阅 [配置 BDA 筛选器](configuring-a-bda-filter.md) 。

下面的代码段演示如何将由 "BDA 支持库" 导出的函数定义为 KSPROPSETID \_ BdaTopology 属性集的调度例程：

```cpp
//
//  KSPROPSETID_BdaTopology property set
//
//  Defines the dispatch routines for the filter level
//  topology properties
//
DEFINE_KSPROPERTY_TABLE(FilterTopologyProperties)
{
    DEFINE_KSPROPERTY_ITEM_BDA_NODE_TYPES(
        BdaPropertyNodeTypes,
        NULL
        ),
    DEFINE_KSPROPERTY_ITEM_BDA_PIN_TYPES(
        BdaPropertyPinTypes,
        NULL
        ),
    DEFINE_KSPROPERTY_ITEM_BDA_TEMPLATE_CONNECTIONS(
        BdaPropertyTemplateConnections,
        NULL
        ),
    DEFINE_KSPROPERTY_ITEM_BDA_CONTROLLING_PIN_ID(
        BdaPropertyGetControllingPinId,
        NULL
        )
};
```

 


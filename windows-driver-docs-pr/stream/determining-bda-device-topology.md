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
- 模板筛选器拓扑 WDK BDA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03e9fd63ba928358c3ae5395f3a3544c04c29ae1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374069"
---
# <a name="determining-bda-device-topology"></a>确定 BDA 设备拓扑





BDA 设备拓扑组成的节点，其中每个表示信号一些转换连接的网络。 节点可以在不同的筛选器之间任意分组。 此任意分组为硬件供应商提供了某些自由它们如何实现其硬件和驱动程序，以便与不同类型的网络在想要支持的网络提供程序以一般方式处理此类硬件和驱动程序。

若要运行此任意分组体系结构，为网络提供商必须能够进行方式来 （即，支持哪些类型的节点网络筛选器可以） 信号的哪种转换这些筛选器执行的查询筛选器。 筛选器基础 Ring 0 微型驱动程序传递给网络提供商通过其支持的节点的网络的图片[KSPROPSETID\_BdaTopology](https://msdn.microsoft.com/library/windows/hardware/ff566561)属性集。

在确定筛选器的模板拓扑时，网络提供商循环访问节点类型的列表和 pin 类型，并查询每个节点和其功能的 pin。 网络提供程序使用的下列属性的 KSPROPSETID\_BdaTopology 以确定筛选器的模板拓扑：

-   KSPROPERTY\_BDA\_NODE\_TYPES

    节点类型表示可能功能节点中的筛选器。 KSPROPERTY\_BDA\_节点\_BDA 微型驱动程序筛选器实例的类型属性返回提供的所有节点类型的列表。 微型驱动程序将分配用于标识节点类型的任意值。 通常情况下，微型驱动程序使用的每个元素的索引的微型驱动程序的节点类型列表中的值为每个节点类型。 BDA 微型驱动程序将每个节点类型分配节点说明的 GUID。 为网络提供商目前支持的类型中定义的节点说明 Guid *bdamedia.h*。 此节点说明向网络提供商指示节点执行的操作。 在模板拓扑中，节点类型可以只出现一次。 但是，多个特定类型的节点可能具有相同的节点说明的 GUID。 这允许特定的信号转换发生在筛选器的拓扑中的多个位置同时允许要明确标识单个拓扑节点的网络提供程序。

-   KSPROPERTY\_BDA\_PIN\_TYPES

    Pin 类型表示可能的连接到关系图中的其他筛选器。 KSPROPERTY\_BDA\_PIN\_类型属性将返回所有可以创建筛选器的固定类型的列表。 在模板拓扑中，pin 类型可以只出现一次。

-   KSPROPERTY\_BDA\_模板\_连接

    KSPROPERTY\_BDA\_模板\_连接属性将返回一个数组，表示节点类型与可以在筛选器配置 pin 类型之间的所有可能的连接。 请参阅[映射连接拓扑](mapping-connection-topology.md)有关详细信息。

当首次创建筛选器实例并将其添加到图形时，它通常具有输入插针，但没有输出插针。 若要创建输出插针，网络提供商，首先使用 KSPROPSETID\_BdaTopology 属性以确定筛选器可以执行哪些操作。 这些属性，请从网络提供商确定哪些操作它要求筛选器来执行特定筛选器关系图。 然后，使用网络提供商[KSMETHODSETID\_BdaDeviceConfiguration](https://msdn.microsoft.com/library/windows/hardware/ff563404)方法设置为创建特定 pin 类型相匹配的输出插针，并创建内部拓扑，这是实际的硬件路径之间这些 pin 和输入插针。 请参阅[配置 BDA 筛选器](configuring-a-bda-filter.md)有关详细信息。

下面的代码段演示如何定义导出的函数按 BDA 支持库作为调度例程的 KSPROPSETID\_BdaTopology 属性集：

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

 

 





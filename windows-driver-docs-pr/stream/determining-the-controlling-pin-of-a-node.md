---
title: 确定节点的控制引脚
description: 确定节点的控制引脚
keywords:
- 方法设置 WDK BDA，节点控制 pin
- 属性设置 WDK BDA，节点控制 pin
- 控制 pin WDK BDA
- 控制 pin WDK BDA 的节点
- 阵列 WDK BDA
- 固定控制器 WDK BDA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f8eb0f7b451f06c3e7dff027ab83f85f800487f8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817945"
---
# <a name="determining-the-controlling-pin-of-a-node"></a>确定节点的控制引脚





与筛选器和 pin 不同，节点没有关联的文件句柄，在这种情况下，应用程序在环3中可以访问它们。 由于节点是筛选器内的内部组件，因此它们存在于筛选器的输入插针和输出插针之间。 网络提供程序必须确定要使用的筛选器 pin，然后使用 pin 来访问节点。 此筛选器 pin 称为该节点的控制 pin。 若要确定筛选器 "BDA 模板连接" 列表中每个节点的控制 pin，网络提供程序会查询 \_ \_ \_ \_ [KSPROPSETID \_ BdaTopology](./kspropsetid-bdatopology.md) 属性集的 KSPROPERTY BDA 控制 pin ID 属性。 BDA 微型驱动程序依次为每个节点调用 [**BdaPropertyGetControllingPinId**](/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdapropertygetcontrollingpinid) 支持功能。 在此调用中，微型驱动程序将指针传递到 [**KSP \_ BDA \_ 节点 \_ 固定**](/windows-hardware/drivers/ddi/bdamedia/ns-bdamedia-_ksp_bda_node_pin) 结构。 此结构标识用于检索特定节点类型的控制 pin 以及一对筛选器的输入插针和输出插针的属性请求。 BDA 支持库返回节点类型的控制 pin 的标识符。

BDA 微型驱动程序通常不会截获 KSPROPERTY \_ BDA \_ 控制 \_ PIN \_ ID 属性。 微型驱动程序自动调度 KSPROPSETID BdaTopology 属性集中的 **BdaPropertyGetControllingPinId** 支持函数 \_ 。 有关详细信息，请参阅 [确定 BDA 设备拓扑](determining-bda-device-topology.md) 。

支持库可以完成确定控制 pin 标识符的所有工作，因为 BDA 微型驱动程序提供了支持库，并在 BDA 微型驱动程序开始操作时提供了一个指向该 [**bda \_ 筛选器 \_ 模板**](/windows-hardware/drivers/ddi/bdasup/ns-bdasup-_bda_filter_template) 结构的指针。 有关详细信息，请参阅 [启动 BDA 微型驱动程序](starting-a-bda-minidriver.md) 。 BDA 微型驱动程序告知 BDA 支持库如何通过包含在 BDA 筛选器模板中的信息来确定控制 pin \_ \_ 。 此信息包括：

-   连接的数组。 此数组是一种 [**KSTOPOLOGY \_ 连接**](/windows-hardware/drivers/ddi/ks/ns-ks-kstopology_connection) 数组，它提供可以在筛选器之间或筛选器与相邻筛选器之间进行的节点和 pin 类型之间的所有可能连接的表示形式。 有关 KSTOPOLOGY 连接数组的详细信息，请参阅 [映射连接拓扑](mapping-connection-topology.md) \_ 。

-   接点值的数组。 连接是拓扑中的一个点，其中的一个输入拆分为不同输出的一个或多个路径，或者一个或多个输入加入单个输出路径。 为接点提供的值对应于 KSTOPOLOGY 连接数组中元素的索引 \_ 。 大多数拓扑将只有一个接头。

-   [**BDA \_ PIN \_ 配对**](/windows-hardware/drivers/ddi/bdasup/ns-bdasup-_bda_pin_pairing)结构的数组。 这些结构标识输入和输出插针类型、可以在筛选器上创建的输入类型实例的最大数目，以及可以在筛选器上创建的最大输出类型实例数。 这些结构还包含指向输入插针和输出插针之间的接点值的数组的指针。 有关 BDA 引脚配对阵列的详细信息，请参阅 [启动 Bda 微型驱动程序](starting-a-bda-minidriver.md) \_ \_ 。

下图显示了支持库如何确定控制特定节点的筛选器 pin：

![说明支持库如何确定控制特定节点的筛选器 pin 的关系图](images/bdajoint.png)

 


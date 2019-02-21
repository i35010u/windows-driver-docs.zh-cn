---
title: 确定一个节点的控制 Pin
description: 确定一个节点的控制 Pin
ms.assetid: be1236e2-c710-4833-863e-54e826e53f92
keywords:
- 方法设置 WDK BDA，控制 pin 的节点
- 属性设置 WDK BDA，控制 pin 的节点
- 控制固定 WDK BDA
- 节点控制 pin WDK BDA
- 数组 WDK BDA
- 固定控制器 WDK BDA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7a10ded8e395f1e02d375f900b35043b83d1fc6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526968"
---
# <a name="determining-the-controlling-pin-of-a-node"></a>确定一个节点的控制 Pin





与筛选器和插针，不同节点不具有所依据的 3 环中的应用程序可以访问它们的关联的文件句柄。 因为节点是一个筛选器中的内部组件，它们存在某个位置之间的筛选器的输入和输出插针。 网络提供商必须确定哪些筛选器的 pin 以使用，然后使用 pin 访问节点。 此筛选器 pin 该节点称为控制 pin。 若要确定每个节点在 BDA 模板连接列表中的筛选器的控制 pin，网络提供商查询 KSPROPERTY\_BDA\_控制\_PIN\_ID 属性[KSPROPSETID\_BdaTopology](https://msdn.microsoft.com/library/windows/hardware/ff566561)属性集。 BDA 微型驱动程序将调用[ **BdaPropertyGetControllingPinId** ](https://msdn.microsoft.com/library/windows/hardware/ff556480)支持为每个节点的函数。 在此调用，微型驱动程序将传递一个指向[ **KSP\_BDA\_节点\_PIN** ](https://msdn.microsoft.com/library/windows/hardware/ff566716)结构。 此结构标识属性请求来检索特定节点类型和一对筛选器的输入的控制 pin 和输出插针。 BDA 支持库返回的节点类型的控制 pin 的标识符。

BDA 微型驱动程序通常不截获 KSPROPERTY\_BDA\_控制\_PIN\_ID 属性。 微型驱动程序会自动将调度**BdaPropertyGetControllingPinId**支持函数从 KSPROPSETID\_BdaTopology 属性集。 请参阅[确定 BDA 设备拓扑](determining-bda-device-topology.md)有关详细信息。

支持库是能够执行确定控制 pin 的标识符，因为 BDA 微型驱动程序用一个指针指向提供支持库的所有工作[ **BDA\_筛选器\_模板**](https://msdn.microsoft.com/library/windows/hardware/ff556523)结构 BDA 微型驱动程序启动运行时。 请参阅[启动 BDA 微型驱动程序](starting-a-bda-minidriver.md)有关详细信息。 BDA 微型驱动程序通知 BDA 支持库如何确定 BDA 中包含的信息通过控制 pin\_筛选器\_模板。 此类信息包括：

-   连接一个数组。 此数组是[ **KSTOPOLOGY\_连接**](https://msdn.microsoft.com/library/windows/hardware/ff567148)内部筛选器或筛选器之间可以进行数组，其中提供的表示形式节点和 pin 之间所有可能的连接类型且靠近筛选器。 请参阅[映射连接拓扑](mapping-connection-topology.md)详细了解 KSTOPOLOGY\_连接数组。

-   联合值的数组。 接头是拓扑中的点其中一个输入拆分到不同的输出，一个或多个路径或一个或多个输入联接到单个输出路径中。 提供给联合的值对应于 KSTOPOLOGY 中的元素的索引\_连接数组。 大多数拓扑必须只有一个联合。

-   一个数组[ **BDA\_PIN\_配对**](https://msdn.microsoft.com/library/windows/hardware/ff556544)结构。 这些结构标识输入和输出插针类型、 筛选器，可以创建的输入类型实例的最大数量，并且可以创建筛选器的输出类型实例的最大数量。 这些结构还包含指向输入和输出插针之间的联合值的数组的指针。 请参阅[启动 BDA 微型驱动程序](starting-a-bda-minidriver.md)详细了解 BDA\_PIN\_配对数组。

下图显示了如何支持库确定控制特定节点的筛选器 pin:

![说明如何支持库确定筛选器 pin，用于控制特定节点的关系图](images/bdajoint.png)

 

 





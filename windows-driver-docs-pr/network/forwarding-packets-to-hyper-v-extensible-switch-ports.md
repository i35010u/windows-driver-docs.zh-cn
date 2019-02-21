---
title: 将数据包转发到的 HYPER-V 可扩展交换机端口
description: 将数据包转发到的 HYPER-V 可扩展交换机端口
ms.assetid: C8DA9064-21EE-45F4-BE6D-D24851C5480B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c8e442f6952efd52db3152a61760e725ee0674ae
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520526"
---
# <a name="forwarding-packets-to-hyper-v-extensible-switch-ports"></a>将数据包转发到的 HYPER-V 可扩展交换机端口


此页介绍了如何转发扩展的 HYPER-V 可扩展交换机可以将数据包转发到一个或多个端口。 此类扩展也可向连接到可扩展交换机外部网络适配器的单个网络适配器转发数据包。

**请注意**  仅转发扩展或可扩展交换机自身可扩展交换机可以将数据包转发到可扩展的交换机端口。

 

**请注意**  此页面假定您熟悉的信息和中的关系图[概述的 HYPER-V 可扩展交换机](overview-of-the-hyper-v-extensible-switch.md)并[混合转发](hybrid-forwarding.md)。

 

**请注意**  可扩展交换机接口，在 NDIS 筛选器驱动程序被称为*可扩展交换机扩展*驱动程序堆栈称为*可扩展交换机驱动程序堆栈*. 有关扩展的详细信息，请参阅[HYPER-V 可扩展交换机扩展](hyper-v-extensible-switch-extensions.md)。

 

如果已安装并启用了可扩展交换机驱动程序堆栈中转发扩展，它负责为其获取可扩展交换机入口数据路径每个数据包转发决策。 根据这些转发的决策，通过扩展到的数据包的带外 (OOB) 数据中的目标端口数组中添加目标端口[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构。 在数据包后已完成的可扩展交换机数据路径，可扩展交换机接口提供了其遍历到指定的目标端口的数据包。

**请注意**  如果未安装或启用转发扩展，可扩展开关时，它将从传入数据路径获取的数据包转发决策。 开关将目标端口添加到 OOB 数据中的数据包[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构之前将转发的数据包可扩展交换机出口数据路径。

 

**请注意**  转发扩展数据包是否 NVGRE 数据包，可以将目标端口添加到目标端口数组。 但是，可扩展交换机的 HYPER-V 网络虚拟化 (HNV) 组件负责确定目标端口和转发数据包。 有关详细信息，请参阅[混合转发](hybrid-forwarding.md)。

 

转发扩展可以仅向数据包从入口数据路径获取添加端口的目标。 将数据包转发向上出口数据路径之后，筛选和转发扩展可以排除的数据包发送到可扩展交换机端口。 有关详细信息，请参阅[可扩展交换机目标端口不包括数据包传递](excluding-packet-delivery-to-extensible-switch-destination-ports.md)。

中的数据包的 OOB 数据[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构，数据中包含目标端口[ **NDIS\_交换机\_转发\_目标\_数组**](https://msdn.microsoft.com/library/windows/hardware/hh598210)结构。 数组中的每个元素定义了目标端口，其格式为[ **NDIS\_交换机\_端口\_目标**](https://msdn.microsoft.com/library/windows/hardware/hh598224)结构。

转发扩展可以调用以下 HYPER-V 可扩展交换机处理程序函数来管理[ **NDIS\_交换机\_转发\_目标\_数组**](https://msdn.microsoft.com/library/windows/hardware/hh598210)结构并将其[ **NDIS\_交换机\_端口\_目标**](https://msdn.microsoft.com/library/windows/hardware/hh598224)元素：

<a href="" id="addnetbufferlistdestination"></a>[*AddNetBufferListDestination*](https://msdn.microsoft.com/library/windows/hardware/hh598133)  
此函数将添加到单个目标端口[ **NDIS\_交换机\_转发\_目标\_数组**](https://msdn.microsoft.com/library/windows/hardware/hh598210)中数据包的 OOB 结构数据。

<a href="" id="getnetbufferlistdestinations"></a>[*GetNetBufferListDestinations*](https://msdn.microsoft.com/library/windows/hardware/hh598157)  
此函数返回一个指向[ **NDIS\_交换机\_转发\_目标\_数组**](https://msdn.microsoft.com/library/windows/hardware/hh598210)数据包的 OOB 数据中的结构。

<a href="" id="grownetbufferlistdestinations"></a>[*GrowNetBufferListDestinations*](https://msdn.microsoft.com/library/windows/hardware/hh598158)  
此函数添加到多个目标端口元素[ **NDIS\_交换机\_转发\_目标\_数组**](https://msdn.microsoft.com/library/windows/hardware/hh598210)的数据包的结构OOB 数据。

<a href="" id="updatenetbufferlistdestinations"></a>[*UpdateNetBufferListDestinations*](https://msdn.microsoft.com/library/windows/hardware/hh598303)  
此函数将提交该扩展做要添加或排除某个数据包的一个或多个目标端口的修改。 这些更改会提交到[ **NDIS\_交换机\_转发\_目标\_数组**](https://msdn.microsoft.com/library/windows/hardware/hh598210)数据包的 OOB 数据中的结构。

当转发扩展[ *FilterSendNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff549966)调用函数时， *NetBufferList*参数包含指向的链接列表的指针[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构。 每个这些结构指定的入口数据路径从获得一个数据包。

每个[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)在此列表中，转发扩展的结构将数据包的目标端口添加通过执行以下步骤：

1.  扩展，可以根据各种类型的条件将数据包转发决策。 这些条件包括：

    -   根据数据包的源端口和网络适配器连接的策略条件。 转发扩展使用获取此信息[ **NET\_缓冲区\_列表\_开关\_转发\_详细**](https://msdn.microsoft.com/library/windows/hardware/hh598259)宏。

    -   数据包的有效负载数据的基础之上的可扩展交换机端口的策略条件。 例如，可扩展交换机端口的策略可能包括筛选器以便传递仅 IP 版本 4 (IPv4) 数据包。

    **请注意**  数据包是否 NVGRE 数据包，可扩展交换机的 HNV 组件是负责转发数据包。 但是，转发扩展可以将应用的入口和出口路径中其自身策略条件。 有关详细信息，请参阅[混合转发](hybrid-forwarding.md)。

     

2.  如果该扩展确定可以将数据包转发到一个或多个可扩展交换机端口，它必须将目标端口添加到 OOB 数据包。 有关此过程的详细信息，请参阅[添加可扩展交换机目标将数据转到数据包](adding-extensible-switch-destination-port-data-to-a-packet.md)。

    **请注意**  如果数据包，NVGRE 数据包转发扩展不需要添加目标端口。 有关详细信息，请参阅[混合转发](hybrid-forwarding.md)。

     

3.  如果扩展插件确定不能将数据包转发到任何可扩展交换机端口，它必须丢弃该数据包。

    **请注意**  这不是如果数据包 NVGRE 数据包，则返回 true。 有关详细信息，请参阅[混合转发](hybrid-forwarding.md)。

     

4.  如果该扩展添加了一个或多个数据包的目标端口，则必须调用[ **NdisFSendNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff562616)出口数据路径上的将数据包转发。

    **请注意**  数据包是否 NVGRE 数据包，可扩展交换机的 HNV 组件是负责转发数据包。 有关详细信息，请参阅[混合转发](hybrid-forwarding.md)。

     

有关可扩展交换机入口和出口数据路径的详细信息，请参阅[HYPER-V 可扩展交换机数据路径](hyper-v-extensible-switch-data-path.md)。

 

 






---
title: 将数据包转发到 Hyper-V 可扩展交换机端口
description: 将数据包转发到 Hyper-V 可扩展交换机端口
ms.assetid: C8DA9064-21EE-45F4-BE6D-D24851C5480B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e0be0155f20489369a10a0b472a84f586d41eba
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839648"
---
# <a name="forwarding-packets-to-hyper-v-extensible-switch-ports"></a>将数据包转发到 Hyper-V 可扩展交换机端口


本页介绍如何将 Hyper-v 可扩展交换机转发扩展转发到一个或多个端口。 这种类型的扩展还可以将数据包转发到连接到可扩展交换机外部网络适配器的各个网络适配器。

**请注意**  仅可扩展交换机转发扩展或可扩展交换机本身才能将数据包转发到可扩展交换机端口。

 

**请注意**  本页假设你熟悉[hyper-v 可扩展交换机](overview-of-the-hyper-v-extensible-switch.md)和[混合转发](hybrid-forwarding.md)概述中的信息和关系图。

 

**注意**  在可扩展交换机接口中，NDIS 筛选器驱动程序称为*可扩展交换机扩展*，驱动程序堆栈称为*可扩展交换机驱动程序堆栈*。 有关扩展的详细信息，请参阅[Hyper-v 可扩展交换机扩展](hyper-v-extensible-switch-extensions.md)。

 

如果在可扩展交换机驱动程序堆栈中安装并启用了转发扩展，则该扩展将负责为它在可扩展交换机入口数据路径上获取的每个数据包做出转发决定。 根据这些转发决策，扩展会将目标端口添加到数据包的[**NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)的带外（OOB）数据的目标端口数组中\_列表结构。 数据包完成可扩展交换机数据路径的遍历后，可扩展交换机接口会将数据包传递到指定的目标端口。

**请注意**  如果未安装或未启用转发扩展，则可扩展交换机将为它从入口数据路径获取的数据包做出转发决定。 此开关将目标端口添加到数据包的[**NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构的 OOB 数据，然后将该数据包转发到可扩展交换机传出数据路径。

 

**请注意**  如果数据包为 NVGRE 数据包，则转发扩展可以向目标端口数组添加目标端口。 但是，可扩展交换机的 Hyper-v 网络虚拟化（HNV）组件负责确定目标端口并转发数据包。 有关详细信息，请参阅[混合转发](hybrid-forwarding.md)。

 

转发扩展只能将端口目标添加到从入口数据路径获取的数据包。 在将数据包转发到传出的数据路径之后，筛选和转发扩展可将数据包传递排除到可扩展的交换机端口。 有关详细信息，请参阅[排除数据包传递到可扩展交换机目标端口](excluding-packet-delivery-to-extensible-switch-destination-ports.md)。

在数据包的[**网络\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构的 OOB 数据中，目标端口的数据包含在[**NDIS\_交换机\_转发\_目标\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)结构。 数组中的每个元素都定义一个目标端口，并将其格式化为[**NDIS\_交换机\_端口\_目标**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_port_destination)结构。

转发扩展插件可以调用以下 Hyper-v 可扩展交换机处理程序函数来管理[**NDIS\_交换机\_转发\_目标\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)结构，以及其[**NDIS\_交换机\_\_目标**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_port_destination)元素：

<a href="" id="addnetbufferlistdestination"></a>[*AddNetBufferListDestination*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_add_net_buffer_list_destination)  
此函数将单个目标端口添加到[**NDIS\_交换机\_转发\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)数据包的 OOB 数据中的\_数组结构。

<a href="" id="getnetbufferlistdestinations"></a>[*GetNetBufferListDestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_get_net_buffer_list_destinations)  
此函数返回一个指针，该指针指向[**NDIS\_交换机\_转发\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)数据包的 OOB 数据中的\_数组结构。

<a href="" id="grownetbufferlistdestinations"></a>[*GrowNetBufferListDestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_grow_net_buffer_list_destinations)  
此函数将更多的目标端口元素添加到[**NDIS\_交换机\_转发\_目标\_ARRAY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)数据的数组结构。

<a href="" id="updatenetbufferlistdestinations"></a>[*UpdateNetBufferListDestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_update_net_buffer_list_destinations)  
此函数提交扩展所做的修改，以便为数据包添加或排除一个或多个目标端口。 这些更改提交到[**NDIS\_交换机\_转发\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)数据包的 OOB 数据中的\_数组结构。

调用转发扩展的[*FilterSendNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_send_net_buffer_lists)函数时， *NetBufferList*参数包含指向[**网络\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)的链接列表的指针\_列表结构。 其中每个结构都指定从入口数据路径获取的数据包。

对于此列表中的每个[**网络\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构，转发扩展会按照以下步骤为数据包添加目标端口：

1.  扩展根据各种类型的条件，对数据包进行转发决定。 这些条件包括：

    -   基于数据包的源端口和网络适配器连接的策略条件。 转发扩展插件使用[**NET\_缓冲区\_列表获取此信息，\_开关\_转发\_详细信息**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-switch-forwarding-detail)宏。

    -   基于数据包的负载数据的可扩展交换机端口的策略条件。 例如，可扩展交换机端口的策略可能包含一个筛选器，以允许只传送 IP 版本4（IPv4）数据包。

    **请注意**  如果数据包为 NVGRE 数据包，则可扩展交换机的 HNV 组件负责转发数据包。 但是，转发扩展可以在入口和出口路径中应用自己的策略条件。 有关详细信息，请参阅[混合转发](hybrid-forwarding.md)。

     

2.  如果扩展确定数据包可以转发到一个或多个可扩展交换机端口，则必须将目标端口添加到数据包的 OOB 数据中。 有关此过程的详细信息，请参阅[将可扩展交换机目标端口数据添加到数据包](adding-extensible-switch-destination-port-data-to-a-packet.md)。

    **请注意**  如果数据包为 NVGRE 数据包，则不需要使用转发扩展添加目标端口。 有关详细信息，请参阅[混合转发](hybrid-forwarding.md)。

     

3.  如果扩展确定无法将数据包转发到任何可扩展交换机端口，则必须删除该数据包。

    **请注意**  如果数据包为 NVGRE 数据包，则不是这样。 有关详细信息，请参阅[混合转发](hybrid-forwarding.md)。

     

4.  如果扩展插件为数据包添加了一个或多个目标端口，则必须调用[**NdisFSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlists)来转发传出数据路径上的数据包。

    **请注意**  如果数据包为 NVGRE 数据包，则可扩展交换机的 HNV 组件负责转发数据包。 有关详细信息，请参阅[混合转发](hybrid-forwarding.md)。

     

有关可扩展交换机入口和出口数据路径的详细信息，请参阅[Hyper-v 可扩展交换机数据路径](hyper-v-extensible-switch-data-path.md)。

 

 






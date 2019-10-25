---
title: 将可扩展交换机目标端口数据添加到数据包
description: 将可扩展交换机目标端口数据添加到数据包
ms.assetid: C921D9F8-B6FB-4B53-8CC5-CC941720FF37
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd6dac07f83f234a043ca75a843c0a5134e35678
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838240"
---
# <a name="adding-extensible-switch-destination-port-data-to-a-packet"></a>将可扩展交换机目标端口数据添加到数据包


本主题介绍 Hyper-v 可扩展交换机转发扩展如何指定将数据包传递到一个或多个目标端口。 这些扩展还可以将数据包转发到绑定到可扩展交换机外部网络适配器的单个物理网络适配器。

**注意** 只有转发扩展或交换机本身才能将数据包转发到可扩展交换机端口或单个网络适配器。



下图显示了通过用于 NDIS 6.40 （Windows Server 2012 R2）和更高版本的可扩展交换机驱动程序堆栈的数据包流量的数据路径。 这两个图形还显示进出连接到可扩展交换机端口的网络适配器的数据包流量的数据路径。

![显示连接到网络适配器的数据包流量或来自连接到为 ndis 6.40 更新的可扩展交换机端口的数据路径的流程图](images/vswitchteam2-ndis640.png)

下图显示了通过用于 NDIS 6.30 的可扩展交换机驱动程序堆栈的数据包流量（Windows Server 2012）的数据路径。

![显示连接到可扩展交换机端口的网络适配器的数据包流量的数据路径的流程图](images/vswitchteam2.png)

每个可扩展交换机目标端口都是由 ndis [ **\_交换机\_端口\_目标**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_port_destination) [ **\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)元素指定的。 此数组包含在数据包的[**网络\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)的带外（OOB）转发上下文\_列表结构。 有关此上下文的详细信息，请参阅[Hyper-v 可扩展交换机转发上下文](hyper-v-extensible-switch-forwarding-context.md)。

如果在可扩展交换机驱动程序堆栈中绑定并启用了转发扩展，则该扩展将负责确定从可扩展交换机入口数据路径获取的每个数据包的目标端口，除非数据包为 NVGRE 数据包。 有关此数据路径的详细信息，请参阅[Hyper-v 可扩展交换机数据路径概述](overview-of-the-hyper-v-extensible-switch-data-path.md)。 有关 NVGRE 数据包的详细信息，请参阅[混合转发](hybrid-forwarding.md)。

**注意** 如果在驱动程序堆栈中未绑定或启用转发扩展，则可扩展交换机会确定它从入口数据路径获取的数据包的目标端口。



当转发扩展为在入口数据路径上获取的数据包确定目标端口时，必须遵循以下指导原则：

-   扩展必须初始化[**ndis\_交换机\_端口\_目标**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_port_destination)结构中的 NDIS [ **\_交换机\_使用目标端口转发\_目标\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)结构信息.

    如果目标端口未连接到外部网络适配器，则扩展必须将[**ndis\_交换机\_端口\_目标**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_port_destination)结构中的**NicIndex**成员设置为**NDIS\_switch\_默认值\_NIC\_索引**。

    如果目标端口连接到可扩展交换机外部网络适配器，则扩展可以指定要将发送请求转发到的基础物理网络适配器的索引。 此扩展通过将**NicIndex**成员设置为非零 NDIS\_交换机\_NIC\_索引值连接到外部网络适配器的目标网络适配器来实现此目的。

    有关详细信息，请参阅[将数据包转发到物理网络适配器](forwarding-packets-to-physical-network-adapters.md)。

-   扩展必须将目标端口仅添加到具有活动网络适配器连接的端口。 如果扩展插件转发了[OID\_交换机\_NIC\_断开](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-disconnect)请求，则它不能添加与断开连接的网络适配器关联的目标端口。

-   为了提高性能，扩展必须仅添加对数据包传递有效的端口目标。 在这种情况下，扩展必须将目标端口的[**NDIS\_交换机\_端口\_目标**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_port_destination)结构的**IsExcluded**成员设置为 FALSE。

-   若要在将 802.1 Q 虚拟局域网（VLAN）数据传递到端口之前将其保留在包中，该扩展会将**PreserveVLAN**成员设置为 TRUE。

    若要在将数据包传递到端口之前删除数据包中的 802.1 Q 虚拟局域网（VLAN）数据，该扩展将**PreserveVLAN**成员设置为 FALSE。

-   若要在将 802.1 Q 优先级数据传递到端口之前将其保留在包中，则该扩展将**PreservePriority**成员设置为 TRUE。

    若要在将数据包传递到端口之前删除数据包中的 802.1 Q 优先级数据，该扩展将**PreservePriority**成员设置为 FALSE。

-   如果转发扩展插件为数据包添加了多个目标端口，则必须执行以下步骤：

    1.  该扩展首先通过使用 Net\_BUFFER\_LIST\_\_\_LIST，访问数据包的[**NDIS\_交换机\_转发\_详细\_net\_buffer list INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_detail_net_buffer_list_info)结构[ **\_转发\_详细**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-switch-forwarding-detail)的宏。 然后，扩展插件读取**NumAvailableDestinations**成员，以确定目标端口数组中有多少个未使用的目标端口元素。 如果扩展需要的目标端口比数组中的可用目标端口多，则必须调用[*GrowNetBufferListDestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_grow_net_buffer_list_destinations)函数为数组中的其他目标端口分配空间。

        当扩展调用[*GrowNetBufferListDestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_grow_net_buffer_list_destinations)时，它会将*NumberOfNewDestinations*参数设置为要添加到包中的新目标端口数。

        扩展还将*NetBufferLists*参数设置为指向包的[**网络\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构的指针。

        **注意** 如果数组中有可用的目标端口，则扩展不应调用[*GrowNetBufferListDestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_grow_net_buffer_list_destinations)。

    2.  如果[*GrowNetBufferListDestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_grow_net_buffer_list_destinations)函数成功返回，则它已将其他目标端口添加到[**NDIS\_交换机\_转发\_目标\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)中的目标数组的末尾。构造. 在*目标*参数中返回指向此结构的指针。

        **注意** 如果[*GrowNetBufferListDestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_grow_net_buffer_list_destinations)函数无法分配请求数目的目标端口，则会\_资源返回 NDIS\_状态。

    3.  该扩展在[**NDIS\_交换机\_转发\_目标\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)结构中指定新的目标端口元素。 该扩展将每个新的目标端口初始化为[**NDIS\_交换机\_端口\_目标**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_port_destination)结构。

        此扩展将从**NumDestinations**偏移量开始将新的目标端口初始化为数组。 **NumDestinations**是[**NDIS\_交换机\_转发\_目标\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)结构的成员。

    4.  扩展完成添加或修改目标端口元素之后，必须调用[*UpdateNetBufferListDestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_update_net_buffer_list_destinations)来提交这些更改。

-   如果扩展插件为数据包添加了单个目标端口，则必须执行以下步骤：

    1.  此扩展在扩展分配的[**NDIS\_交换机\_端口\_目标**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_port_destination)结构中初始化数据包的目标端口信息。

    2.  该扩展调用[*AddNetBufferListDestination*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_add_net_buffer_list_destination) ，以将对[**网络\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)的更改提交到数据包\_列表结构。 该扩展在*destination*参数中传递[**NDIS\_交换机\_端口\_目标**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_port_destination)结构的地址。

        **注意** 扩展不应调用[*UpdateNetBufferListDestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_update_net_buffer_list_destinations)函数以将更改提交到只有一个目标端口的数据包。

-   当转发扩展调用[*AddNetBufferListDestination*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_add_net_buffer_list_destination)或[*UpdateNetBufferListDestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_update_net_buffer_list_destinations)来提交目标端口的更改时，可扩展交换机接口将不会删除在 NDIS 的元素中指定[ **\_交换机\_转发\_目标\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)结构。 数据包发送或接收操作完成后，如果需要，接口可以随意删除端口。

    **注意** 转发扩展将目标端口的更改提交到转发上下文后，不能删除目标端口，并且仅**IsExcluded**目标端口[**NDIS\_交换机\_端口\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_port_destination)可以更改目标结构。 有关详细信息，请参阅[排除数据包传递到可扩展交换机目标端口](excluding-packet-delivery-to-extensible-switch-destination-ports.md)。

-   转发扩展必须同步其对对象标识符（OID） set 请求的处理[\_交换机\_NIC\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-disconnect)与添加断开连接的网络适配器的目标端口的代码断开连接。

    如果为\_OID 调用转发扩展的[*FilterOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_oid_request) [\_NIC\_断开](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-disconnect)请求，则扩展可以执行下列操作之一：

    -   如果名为[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)的扩展插件请求转发此 OID 请求，则它不能将断开连接的网络适配器的端口指定为数据包的目标端口。

        **注意** 如果数据包的唯一目标端口是带有断开连接的网络适配器的目标端口，则该扩展必须丢弃数据包。

    -   此扩展可以返回 NDIS\_状态\_"挂起" 以异步完成请求。 这允许扩展添加端口，使其与断开连接的网络适配器作为数据包的目标端口。 这也允许该扩展调用[*AddNetBufferListDestination*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_add_net_buffer_list_destination)或[*UpdateNetBufferListDestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_update_net_buffer_list_destinations) ，并将目标端口添加到数据包。

        此扩展可能需要对其执行此操作的数据包进行处理，然后再将其关闭。

        **注意** 如果扩展返回 NDIS\_状态\_"挂起"，则它还可以调用[*ReferenceSwitchPort*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port) ，以将端口的引用计数器与断开连接的网络适配器递增。 但是，在调用[*DereferenceSwitchPort*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_dereference_switch_port)来减小端口的引用计数器之前，扩展无法转发 OID 请求。



-   如果目标端口数为零，则转发扩展必须调用[**NdisMSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete)以丢弃数据包。 扩展还必须调用[*ReportFilteredNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_report_filtered_net_buffer_lists) ，以通知有关已丢弃数据包的可扩展交换机接口。

    **注意** 如果转发扩展插件获取了[**网络\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)的链接列表，\_入口数据路径中的多个数据包的列表结构，则应创建一个单独的已删除数据包列表。 通过执行此操作，扩展只需调用[**NdisMSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete)和[*ReportFilteredNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_report_filtered_net_buffer_lists)一次。



-   如果目标端口数大于零，则转发扩展必须调用[**NdisFSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlists) ，将数据包转发到可扩展交换机的微型端口边缘的入口数据路径。

    **注意** 如果转发扩展插件获取了[**网络\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)的链接列表，\_入口数据路径中的多个数据包的列表结构，则应创建一个单独的转发数据包列表。 这样一来，扩展就可以调用[**NdisFSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlists)一次，以便转发数据包列表。 此外，扩展应维护单独的列表，以便转发具有相同目标端口的数据包。 有关详细信息，请参阅[Hyper-v 可扩展交换机发送和接收标志](hyper-v-extensible-switch-send-and-receive-flags.md)。
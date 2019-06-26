---
title: 将可扩展交换机目标端口数据添加到数据包
description: 将可扩展交换机目标端口数据添加到数据包
ms.assetid: C921D9F8-B6FB-4B53-8CC5-CC941720FF37
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d28f4128b54429938043ae82b885a96c1f61f19
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384736"
---
# <a name="adding-extensible-switch-destination-port-data-to-a-packet"></a>将可扩展交换机目标端口数据添加到数据包


本主题介绍如何转发扩展的 HYPER-V 可扩展交换机可以指定数据包传送到一个或多个目标端口。 这些扩展还可以将数据包转发到绑定到可扩展交换机外部网络适配器的单个物理网络适配器。

**请注意**仅转发扩展或开关本身可以将数据包转发到可扩展交换机端口或单个网络适配器。



下图显示了数据包流量通过可扩展交换机驱动程序堆栈 NDIS 6.40 (Windows Server 2012 R2) 和更高版本的数据路径。 这两个图还显示与已连接到可扩展交换机端口的网络适配器的数据包流量的数据路径。

![显示与已连接到更新 ndis 6.40 可扩展交换机端口的网络适配器的数据包流量的数据路径流程图](images/vswitchteam2-ndis640.png)

下图显示通过可扩展交换机驱动程序堆栈数据包流量的数据路径为 NDIS 6.30 (Windows Server 2012)。

![显示与已连接到可扩展交换机端口的网络适配器的数据包流量的数据路径流程图](images/vswitchteam2.png)

指定可扩展交换机的每个目标端口[ **NDIS\_切换\_端口\_目标**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_port_destination)中的元素[ **NDIS\_交换机\_转发\_目标\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)结构。 此数组包含在带外 (OOB) 转发的数据包的上下文[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构。 在此上下文的详细信息，请参阅[HYPER-V 可扩展交换机转发上下文](hyper-v-extensible-switch-forwarding-context.md)。

如果绑定和可扩展交换机驱动程序堆栈中启用转发扩展，它负责确定从可扩展交换机入口数据路径，获取每个数据包的目标端口，除非数据包是 NVGRE 数据包。 有关此数据路径的详细信息，请参阅[概述的 HYPER-V 可扩展交换机数据路径](overview-of-the-hyper-v-extensible-switch-data-path.md)。 有关 NVGRE 数据包的详细信息，请参阅[混合转发](hybrid-forwarding.md)。

**请注意**可扩展交换机未绑定或未在驱动程序堆栈中启用转发扩展，如果确定它将从传入数据路径获取的数据包的目标端口。



确定在获取入口数据路径上的数据包的目标端口转发扩展必须遵循以下准则：

-   扩展必须初始化[ **NDIS\_交换机\_端口\_目标**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_port_destination)结构内[ **NDIS\_交换机\_转发\_目标\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)的目标端口信息的结构。

    如果目标端口未连接到外部网络适配器，必须设置扩展**NicIndex**的成员[ **NDIS\_开关\_端口\_目标**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_port_destination)结构**NDIS\_交换机\_默认\_NIC\_索引**。

    如果目标端口连接到可扩展交换机外部网络适配器，该扩展可以指定将发送请求转发到基础物理网络适配器的索引。 通过设置的扩展插件实现这**NicIndex**成员添加到非零的 NDIS\_交换机\_NIC\_绑定到外部网络适配器的目标网络适配器的索引值。

    有关详细信息，请参阅[到物理网络适配器转发数据包](forwarding-packets-to-physical-network-adapters.md)。

-   扩展必须将目标端口添加到仅对具有活动的网络适配器连接这些端口的数据包的 OOB 数据。 如果有转发扩展[OID\_交换机\_NIC\_断开连接](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-disconnect)请求，则必须添加与断开连接的网络适配器相关联的目标端口。

-   若要提高性能，扩展必须仅添加数据包传递有效的端口目标。 在这种情况下，必须设置扩展**IsExcluded**成员的目标端口[ **NDIS\_开关\_端口\_目标**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_port_destination)为 FALSE 的结构。

-   要保留 802.1Q 前数据包中的虚拟局域网 (VLAN) 数据传送到的端口，该扩展集**PreserveVLAN**成员为 TRUE。

    若要删除 802.1Q 前数据包中的虚拟局域网 (VLAN) 数据传送到的端口，该扩展集**PreserveVLAN**成员为 FALSE。

-   若要保留 802.1Q 前数据包中的优先级数据传送到端口，该扩展集**PreservePriority**成员为 TRUE。

    若要删除 802.1Q 前数据包中的优先级数据传送到的端口，该扩展集**PreservePriority**成员为 FALSE。

-   如果转发扩展添加了多个目标端口的数据包，它必须执行以下步骤：

    1.  扩展第一次访问该数据包[ **NDIS\_交换机\_转发\_详细信息\_NET\_缓冲区\_列表\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_forwarding_detail_net_buffer_list_info)结构的[ **NET\_缓冲区\_列表\_开关\_转发\_详细**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-switch-forwarding-detail)宏。 然后，该扩展读取**NumAvailableDestinations**成员以确定目标端口数组中有多少未使用的目标端口元素。 如果此扩展需要更多的目标端口不是数组中可用，它必须调用[ *GrowNetBufferListDestinations* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_grow_net_buffer_list_destinations)函数以分配空间，对于其他目标端口数组。

        当扩展调用[ *GrowNetBufferListDestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_grow_net_buffer_list_destinations)，它会设置*NumberOfNewDestinations*参数的新的目标端口添加到数数据包。

        扩展还设置*NetBufferLists*参数为指向该数据包[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构。

        **请注意**数组中有可用目标端口，如果该扩展不应调用[ *GrowNetBufferListDestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_grow_net_buffer_list_destinations)。

    2.  如果[ *GrowNetBufferListDestinations* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_grow_net_buffer_list_destinations)函数将返回成功，它的其他目标端口添加到中的目标数组末尾[ **NDIS\_交换机\_转发\_目标\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)结构。 在返回指向此结构的指针*目标*参数。

        **请注意**如果[ *GrowNetBufferListDestinations* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_grow_net_buffer_list_destinations)函数无法分配请求的数目的目标端口，则返回 NDIS\_状态\_资源。

    3.  扩展指定可在中的新目标端口元素[ **NDIS\_交换机\_转发\_目标\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)结构。 扩展初始化每个新的目标端口作为[ **NDIS\_交换机\_端口\_目标**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_port_destination)结构。

        扩展初始化为起始位置的数组的新目标端口**NumDestinations**偏移量。 **NumDestinations**隶属[ **NDIS\_交换机\_转发\_目标\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)结构。

    4.  该扩展已完成添加或修改目标端口元素后，它必须调用[ *UpdateNetBufferListDestinations* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_update_net_buffer_list_destinations)以提交这些更改。

-   如果该扩展添加了数据包的单个目标端口，它必须执行以下步骤：

    1.  扩展初始化中扩展分配数据包的目标端口信息[ **NDIS\_交换机\_端口\_目标**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_port_destination)结构.

    2.  扩展调用[ *AddNetBufferListDestination* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_add_net_buffer_list_destination)提交对更改[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)数据包的结构。 该扩展将传递的地址[ **NDIS\_交换机\_端口\_目标**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_port_destination)结构*目标*参数。

        **请注意**该扩展不应调用[ *UpdateNetBufferListDestinations* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_update_net_buffer_list_destinations)函数以将更改提交到只有一个目标端口的数据包。

-   当转发扩展调用[ *AddNetBufferListDestination* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_add_net_buffer_list_destination)或[ *UpdateNetBufferListDestinations* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_update_net_buffer_list_destinations)提交目标端口的更改，可扩展交换机接口不会删除指定的元素中的可扩展交换机端口[ **NDIS\_切换\_转发\_目标\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)结构。 将数据包发送或接收后的操作已完成，该接口是随意删除该端口，如有必要。

    **请注意**转发扩展转发上下文提交的更改的目标端口后，目标端口不能为已删除和唯一**IsExcluded**成员的目标端口的[**NDIS\_交换机\_端口\_目标**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_port_destination)结构可以进行更改。 有关详细信息，请参阅[可扩展交换机目标端口不包括数据包传递](excluding-packet-delivery-to-extensible-switch-destination-ports.md)。

-   转发扩展必须同步的对象标识符 (OID) 组请求其处理[OID\_交换机\_NIC\_断开连接](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-disconnect)，其将用于目标端口添加的代码断开连接的网络适配器。

    如果转发扩展[ *FilterOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_oid_request)为调用[OID\_开关\_NIC\_断开连接](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-disconnect)请求，该扩展可以执行以下操作：

    -   如果该扩展调用[ **NdisFOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfoidrequest)转发此 OID 请求，它必须将该端口指定与断开连接的网络适配器用作数据包的目标端口。

        **请注意**如果数据包的唯一目标端口是具有断开连接的网络适配器，该扩展必须丢弃该数据包。

    -   扩展可以返回 NDIS\_状态\_PENDING 来以异步方式完成该请求。 这允许用作数据包的目标端口与断开连接的网络适配器添加端口的扩展。 这也允许要调用的扩展[ *AddNetBufferListDestination* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_add_net_buffer_list_destination)或[ *UpdateNetBufferListDestinations* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_update_net_buffer_list_destinations)和完成添加了数据包的目标端口。

        该扩展可能想要为它具有之前它，则将调用转发到端口的数据包执行此操作。

        **请注意**如果扩展插件可以返回 NDIS\_状态\_挂起状态，它可以调用[ *ReferenceSwitchPort* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_reference_switch_port)增加使用的端口的引用计数器断开连接的网络适配器。 但是，该扩展不能转发 OID 请求直到后它会调用[ *DereferenceSwitchPort* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_dereference_switch_port)要递减的端口的引用计数器。



-   如果目标端口数为零，则转发扩展必须调用[ **NdisMSendNetBufferListsComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsendnetbufferlistscomplete)丢弃该数据包。 扩展还必须调用[ *ReportFilteredNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_report_filtered_net_buffer_lists)以通知有关已丢弃的数据包的可扩展交换机接口。

    **请注意**如果转发扩展中获得的链接的列表[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)入口数据路径中的多个数据包的结构，它应创建一个单独丢弃的数据包的列表。 通过执行此操作，该扩展可以调用[ **NdisMSendNetBufferListsComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsendnetbufferlistscomplete)并[ *ReportFilteredNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_report_filtered_net_buffer_lists)只需一次。



-   转发扩展的目标端口数是否大于零，必须调用[ **NdisFSendNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfsendnetbufferlists)将数据包转发通过入口数据路径的微型端口边缘可扩展交换机。

    **请注意**如果转发扩展中获得的链接的列表[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)入口数据路径中的多个数据包的结构，它应创建一个单独的转发的数据包列表。 通过执行此操作，该扩展可以调用[ **NdisFSendNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfsendnetbufferlists)只需一次转发的数据包的列表。 此外，该扩展应维护单独的列表将具有相同目标的数据包转发端口。 有关详细信息，请参阅[HYPER-V 可扩展交换机发送和接收标志](hyper-v-extensible-switch-send-and-receive-flags.md)。
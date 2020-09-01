---
title: 将可扩展交换机目标端口数据添加到数据包
description: 将可扩展交换机目标端口数据添加到数据包
ms.assetid: C921D9F8-B6FB-4B53-8CC5-CC941720FF37
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cebfc9496aec637387dd2518b7a3c80056514ed7
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216010"
---
# <a name="adding-extensible-switch-destination-port-data-to-a-packet"></a>将可扩展交换机目标端口数据添加到数据包


本主题介绍 Hyper-v 可扩展交换机转发扩展如何指定将数据包传递到一个或多个目标端口。 这些扩展还可以将数据包转发到绑定到可扩展交换机外部网络适配器的单个物理网络适配器。

**注意**  只有转发扩展或交换机本身才能将数据包转发到可扩展交换机端口或单个网络适配器。



下图显示了通过用于 NDIS 6.40 (Windows Server 2012 R2) 和更高版本的可扩展交换机驱动程序堆栈的数据包流量的数据路径。 这两个图形还显示进出连接到可扩展交换机端口的网络适配器的数据包流量的数据路径。

![显示连接到网络适配器的数据包流量或来自连接到为 ndis 6.40 更新的可扩展交换机端口的数据路径的流程图](images/vswitchteam2-ndis640.png)

下图显示了通过用于 NDIS 6.30 (Windows Server 2012) 的可扩展交换机驱动程序堆栈的数据包流量的数据路径。

![显示连接到可扩展交换机端口的网络适配器的数据包流量的数据路径的流程图](images/vswitchteam2.png)

每个可扩展交换机目标端口都是在[**ndis \_ 交换机 \_ 转发 \_ 目标 \_ 数组**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)结构内由[**ndis \_ 交换机 \_ 端口 \_ 目标**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_port_destination)元素指定的。 此数组包含在数据包的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构的带外 (OOB) 转发上下文中。 有关此上下文的详细信息，请参阅 [Hyper-v 可扩展交换机转发上下文](hyper-v-extensible-switch-forwarding-context.md)。

如果在可扩展交换机驱动程序堆栈中绑定并启用了转发扩展，则该扩展将负责确定从可扩展交换机入口数据路径获取的每个数据包的目标端口，除非数据包为 NVGRE 数据包。 有关此数据路径的详细信息，请参阅 [Hyper-v 可扩展交换机数据路径概述](overview-of-the-hyper-v-extensible-switch-data-path.md)。 有关 NVGRE 数据包的详细信息，请参阅 [混合转发](hybrid-forwarding.md)。

**注意**  如果在驱动程序堆栈中未绑定或启用转发扩展，则可扩展交换机会确定它从入口数据路径获取的数据包的目标端口。



当转发扩展为在入口数据路径上获取的数据包确定目标端口时，必须遵循以下指导原则：

-   扩展必须使用目标端口信息初始化[**ndis 交换机 \_ \_ 转发 \_ 目标 \_ 数组**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)结构内的[**ndis \_ 交换机 \_ 端口 \_ 目标**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_port_destination)结构。

    如果目标端口未连接到外部网络适配器，则扩展必须将[**ndis \_ 交换机 \_ 端口 \_ 目标**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_port_destination)结构的**NicIndex**成员设置为**ndis \_ 交换机 \_ 默认 \_ NIC \_ 索引**。

    如果目标端口连接到可扩展交换机外部网络适配器，则扩展可以指定要将发送请求转发到的基础物理网络适配器的索引。 此扩展通过将 **NicIndex** 成员设置为 \_ \_ \_ 绑定到外部网络适配器的目标网络适配器的非零 NDIS 交换机 NIC 索引值来实现此目的。

    有关详细信息，请参阅 [将数据包转发到物理网络适配器](forwarding-packets-to-physical-network-adapters.md)。

-   扩展必须将目标端口仅添加到具有活动网络适配器连接的端口。 如果扩展插件转发了 [OID \_ 交换机 \_ NIC \_ 断开连接](./oid-switch-nic-disconnect.md) 请求，则它不能添加与断开连接的网络适配器关联的目标端口。

-   为了提高性能，扩展必须仅添加对数据包传递有效的端口目标。 在这种情况下，扩展必须将目标端口的[**NDIS \_ 交换机 \_ 端口 \_ 目标**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_port_destination)结构的**IsExcluded**成员设置为 FALSE。

-   若要保留 802.1 Q 虚拟局域网 (VLAN) 数据传递到端口之前，该扩展会将 **PreserveVLAN** 成员设置为 TRUE。

    若要删除 802.1 Q 虚拟局域网 (VLAN 在将数据包传递到端口之前) 数据，该扩展会将 **PreserveVLAN** 成员设置为 FALSE。

-   若要在将 802.1 Q 优先级数据传递到端口之前将其保留在包中，则该扩展将 **PreservePriority** 成员设置为 TRUE。

    若要在将数据包传递到端口之前删除数据包中的 802.1 Q 优先级数据，该扩展将 **PreservePriority** 成员设置为 FALSE。

-   如果转发扩展插件为数据包添加了多个目标端口，则必须执行以下步骤：

    1.  该扩展首先使用[**网络 \_ 缓冲区 \_ 列表 \_ 开关 \_ 转发 \_ 详细**](/windows-hardware/drivers/ddi/ndis/nf-ndis-net_buffer_list_switch_forwarding_detail)信息宏访问数据包的[**NDIS \_ 交换机 \_ 转发 \_ 详细信息 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_detail_net_buffer_list_info)结构。 然后，扩展插件读取 **NumAvailableDestinations** 成员，以确定目标端口数组中有多少个未使用的目标端口元素。 如果扩展需要的目标端口比数组中的可用目标端口多，则必须调用 [*GrowNetBufferListDestinations*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_grow_net_buffer_list_destinations) 函数为数组中的其他目标端口分配空间。

        当扩展调用 [*GrowNetBufferListDestinations*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_grow_net_buffer_list_destinations)时，它会将 *NumberOfNewDestinations* 参数设置为要添加到包中的新目标端口数。

        扩展还将 *NetBufferLists* 参数设置为指向包的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构的指针。

        **注意**  如果数组中有可用的目标端口，则扩展不应调用 [*GrowNetBufferListDestinations*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_grow_net_buffer_list_destinations)。

    2.  如果 [*GrowNetBufferListDestinations*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_grow_net_buffer_list_destinations) 函数成功返回，它已将其他目标端口添加到 [**NDIS \_ 切换 \_ 转发 \_ 目标 \_ 数组**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_destination_array) 结构中目标数组的末尾。 在 *目标* 参数中返回指向此结构的指针。

        **注意**  如果 [*GrowNetBufferListDestinations*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_grow_net_buffer_list_destinations) 函数无法分配请求的目标端口数量，则将返回 NDIS \_ 状态 \_ 资源。

    3.  此扩展在 [**NDIS \_ 交换机 \_ 转发 \_ 目标 \_ 数组**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_destination_array) 结构中指定新的目标端口元素。 此扩展将每个新的目标端口初始化为 [**NDIS \_ 交换机 \_ 端口 \_ 目标**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_port_destination) 结构。

        此扩展将从 **NumDestinations** 偏移量开始将新的目标端口初始化为数组。 **NumDestinations** 是 [**NDIS \_ 交换机 \_ 转发 \_ 目标 \_ 数组**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_destination_array) 结构的成员。

    4.  扩展完成添加或修改目标端口元素之后，必须调用 [*UpdateNetBufferListDestinations*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_update_net_buffer_list_destinations) 来提交这些更改。

-   如果扩展插件为数据包添加了单个目标端口，则必须执行以下步骤：

    1.  此扩展在已分配扩展的 [**NDIS \_ 交换机 \_ 端口 \_ 目标**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_port_destination) 结构中初始化数据包的目标端口信息。

    2.  此扩展调用 [*AddNetBufferListDestination*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_add_net_buffer_list_destination) ，以将更改提交到数据包的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构。 此扩展在*DESTINATION*参数中传递[**NDIS \_ 交换机 \_ 端口 \_ 目标**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_port_destination)结构的地址。

        **注意**  扩展不应调用 [*UpdateNetBufferListDestinations*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_update_net_buffer_list_destinations) 函数以将更改提交到只有一个目标端口的数据包。

-   当转发扩展插件调用 [*AddNetBufferListDestination*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_add_net_buffer_list_destination) 或 [*UpdateNetBufferListDestinations*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_update_net_buffer_list_destinations) 来提交目标端口的更改时，可扩展交换机接口将不会删除在 [**NDIS \_ 交换机 \_ 转发 \_ 目标 \_ 数组**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_destination_array) 结构的元素中指定的可扩展交换机端口。 数据包发送或接收操作完成后，如果需要，接口可以随意删除端口。

    **注意** 转发扩展将目标端口的更改提交到转发上下文后，不能删除目标端口，并且只能更改目标端口的[**NDIS \_ 交换机 \_ 端口 \_ 目标**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_port_destination)结构的**IsExcluded**成员。 有关详细信息，请参阅 [排除数据包传递到可扩展交换机目标端口](excluding-packet-delivery-to-extensible-switch-destination-ports.md)。

-   转发扩展必须同步其对对象标识符的处理 (OID) 设置 [oid \_ 交换机 \_ NIC \_ 断开连接](./oid-switch-nic-disconnect.md) 的请求以及为断开连接的网络适配器添加目标端口的代码。

    如果为[OID \_ 交换机 \_ NIC \_ 断开](./oid-switch-nic-disconnect.md)请求调用转发扩展的[*FilterOidRequest*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_oid_request) ，则扩展可以执行以下操作之一：

    -   如果名为 [**NdisFOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest) 的扩展插件请求转发此 OID 请求，则它不能将断开连接的网络适配器的端口指定为数据包的目标端口。

        **注意**  如果数据包的唯一目标端口是带有断开连接的网络适配器的目标端口，则该扩展必须丢弃数据包。

    -   扩展可以返回 NDIS \_ 状态 " \_ 挂起" 以异步完成请求。 这允许扩展添加端口，使其与断开连接的网络适配器作为数据包的目标端口。 这也允许该扩展调用 [*AddNetBufferListDestination*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_add_net_buffer_list_destination) 或 [*UpdateNetBufferListDestinations*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_update_net_buffer_list_destinations) ，并将目标端口添加到数据包。

        此扩展可能需要对其执行此操作的数据包进行处理，然后再将其关闭。

        **注意**  如果扩展返回 NDIS \_ 状态 \_ "挂起"，则它还可以调用 [*ReferenceSwitchPort*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port) ，以将端口的引用计数器与断开连接的网络适配器递增。 但是，在调用 [*DereferenceSwitchPort*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_dereference_switch_port) 来减小端口的引用计数器之前，扩展无法转发 OID 请求。



-   如果目标端口数为零，则转发扩展必须调用 [**NdisMSendNetBufferListsComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete) 以丢弃数据包。 扩展还必须调用 [*ReportFilteredNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_report_filtered_net_buffer_lists) ，以通知有关已丢弃数据包的可扩展交换机接口。

    **注意**  如果转发扩展插件从入口数据路径获取了多个数据包的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构的链接列表，则应创建一个单独的已删除数据包列表。 通过执行此操作，扩展只需调用 [**NdisMSendNetBufferListsComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete) 和 [*ReportFilteredNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_report_filtered_net_buffer_lists) 一次。



-   如果目标端口数大于零，则转发扩展必须调用 [**NdisFSendNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlists) ，将数据包转发到可扩展交换机的微型端口边缘的入口数据路径。

    **注意**  如果转发扩展插件为传入数据路径中的多个数据包获取了 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构的链接列表，则应创建一个单独的转发数据包列表。 这样一来，扩展就可以调用 [**NdisFSendNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlists) 一次，以便转发数据包列表。 此外，扩展应维护单独的列表，以便转发具有相同目标端口的数据包。 有关详细信息，请参阅 [Hyper-v 可扩展交换机发送和接收标志](hyper-v-extensible-switch-send-and-receive-flags.md)。
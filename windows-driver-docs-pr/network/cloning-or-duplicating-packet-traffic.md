---
title: 克隆数据包流量
description: 克隆数据包流量
ms.assetid: 6BAE348D-B5BA-4B74-8D9B-79B146427D8C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f4e4b3e556a318ff6c0259391fe18b9079faa320
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89218173"
---
# <a name="cloning-packet-traffic"></a>克隆数据包流量


本主题介绍 Hyper-v 可扩展交换机扩展如何克隆或复制数据包，以及如何将它们注入可扩展交换机数据路径。 有关克隆数据包的详细信息，请参阅 [克隆的网络 \_ 缓冲区 \_ 列表结构](cloned-net-buffer-list-structures.md)。

**注意**  本页假设你熟悉 [Hyper-v 可扩展交换机](overview-of-the-hyper-v-extensible-switch.md) 和 [混合转发](hybrid-forwarding.md)概述中的信息和关系图。

**注意**  在可扩展交换机接口中，NDIS 筛选器驱动程序称为 *可扩展交换机扩展* ，驱动程序堆栈称为 *可扩展交换机驱动程序堆栈*。 有关扩展的详细信息，请参阅 [Hyper-v 可扩展交换机扩展](hyper-v-extensible-switch-extensions.md)。

可扩展的交换机筛选和转发扩展可遵循以下准则，将克隆的数据包注入到可扩展的交换机入口或出口数据路径：

-   扩展必须首先为克隆的数据包分配 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context) 结构。 然后，该扩展必须将原始数据包中的数据包数据复制到克隆的数据包中。 有关如何克隆数据包的详细信息，请参阅 [派生网络 \_ 缓冲区 \_ 列表结构](derived-net-buffer-list-structures.md)。

-   扩展分配 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context) 结构后，必须调用 [*AllocateNetBufferListForwardingContext*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_allocate_net_buffer_list_forwarding_context) 处理程序函数，以便为数据包分配可扩展的 switch 转发上下文。

    转发上下文位于数据包的带外 (OOB) 数据。 它包含数据包的转发信息，如其源端口和一个或多个目标端口的数组。

    有关转发上下文的详细信息，请参阅 [Hyper-v 可扩展交换机转发上下文](hyper-v-extensible-switch-forwarding-context.md)。

-   此扩展必须通过调用 [*CopyNetBufferListInfo*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_copy_net_buffer_list_info)将 OOB 数据（包括现有源端口）从原始数据包复制到克隆的数据包。 如果扩展插件计划将数据包注入入入口数据路径，则它还必须从原始数据包的 OOB 数据复制目标端口。

    复制 OOB 数据时，扩展必须遵循以下准则：

    -   如果筛选扩展插件计划将数据包注入入入口数据路径，则它必须调用 [*CopyNetBufferListInfo*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_copy_net_buffer_list_info) ，并将 NDIS \_ SWITCH \_ COPY \_ NBL \_ INFO \_ 标志 \_ 保留 \_ 目标标志指定为未指定。 这会导致原始数据包的目标端口不会复制到克隆的数据包中。 当筛选扩展将此数据包注入到入口数据路径中时，如果在驱动程序堆栈) 或可扩展交换机的小型端口边缘中启用，则会将目标端口添加到数据包中 (。

    -   如果筛选扩展插件计划将数据包注入传出数据路径，则它必须调用 [*CopyNetBufferListInfo*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_copy_net_buffer_list_info) ，并在指定的 NDIS \_ SWITCH \_ COPY \_ NBL \_ INFO \_ 标志 \_ PRESERVE \_ 目标标志。 这会导致原始数据包的目标端口被复制到克隆的数据包中。

-   如果筛选扩展正在克隆或复制从出口数据路径获取的数据包，则它可以在调用 [*CopyNetBufferListInfo*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_copy_net_buffer_list_info) 并指定了 NDIS \_ SWITCH \_ COPY \_ NBL \_ INFO \_ 标志 \_ 保留 \_ 目标标志后，更改数据包的目标端口。 有关此过程的详细信息，请参阅 [修改数据包的可扩展交换机源端口数据](modifying-a-packet-s-extensible-switch-source-port-data.md)。

-   如果转发扩展正在克隆或复制从入口数据路径获取的数据包，则它必须为数据包添加新的目标端口，然后才能将数据包注入到入口数据路径。 有关此过程的详细信息，请参阅 [将可扩展交换机目标端口数据添加到数据包](adding-extensible-switch-destination-port-data-to-a-packet.md)。

-   扩展调用 [*CopyNetBufferListInfo*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_copy_net_buffer_list_info)后，将为数据包分配原始数据包中包含的相同源端口信息。

    扩展可以调用 [*SetNetBufferListSource*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_set_net_buffer_list_source) 来更改数据包的带外 (OOB) 数据中的源端口信息。

    扩展可能需要将数据包视为来自特定端口。 这允许将该端口的策略应用到该数据包。 该扩展调用 [*SetNetBufferListSource*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_set_net_buffer_list_source) 来更改数据包的源端口。

    但在某些情况下，扩展可能需要将数据包的源端口标识符分配给 **NDIS \_ 交换机 \_ 默认 \_ 端口 \_ ID**。 例如，对于发送到外部网络上的设备的专有控制数据包，扩展可能需要将源端口标识符设置为 **NDIS \_ 交换机 \_ 默认 \_ 端口 \_ ID** 。

-   在标准 NDIS 数据路径中，非可扩展交换机 OOB 数据通常具有不同的值，具体取决于数据包是否被指示为发送或接收。 例如， [**NDIS \_ IPSEC \_ 卸载 \_ V2 \_ 标头 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v2_header_net_buffer_list_info) OOB 数据是发送和接收特定结构的联合

    在可扩展交换机数据路径中，所有数据包都将通过扩展驱动程序堆栈，同时作为发送和接收。 因此，数据包的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构内的非可扩展 switch OOB 数据将在流通过驱动程序堆栈的整个持续时间内通过发送或接收格式进行。

    此 OOB 数据的格式取决于源可扩展交换机端口，数据包从该端口传入可扩展交换机。 如果源端口已连接到外部网络适配器，则非可扩展交换机 OOB 数据将采用接收格式。 对于其他端口，此 OOB 数据将为发送格式。

    源端口信息存储在包的[**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构的 OOB 数据中[**NDIS \_ 交换机 \_ 转发 \_ 详细 \_ \_ \_ \_ **](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_detail_net_buffer_list_info)信息联合。 扩展通过使用 [**网络 \_ 缓冲区 \_ 列表 \_ 开关 \_ 转发 \_ 详细信息**](/windows-hardware/drivers/ddi/ndis/nf-ndis-net_buffer_list_switch_forwarding_detail) 宏获取数据。

    **注意**  如果扩展克隆了数据包的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构，则在添加或修改 oob 数据时，必须考虑不可扩展的 oob 数据。 此扩展可以调用 [*CopyNetBufferListInfo*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_copy_net_buffer_list_info) 将所有 OOB 数据从源数据包复制到克隆的数据包。 将数据复制到数据包时，此函数将维护 OOB 发送或接收格式。



-   当扩展克隆数据包时，克隆的数据包数据位于 Hyper-v 父分区的父操作系统中的 "本地" 或 " *受信任*的内存" 中。 子分区无法访问此内存。 因此，在该分区中运行的来宾操作系统不同步更新将其视为 "安全"。

    克隆原始数据包后，扩展必须使用[**网络 \_ 缓冲区 \_ 列表 \_ 开关 \_ 转发 \_ 详细信息**](/windows-hardware/drivers/ddi/ndis/nf-ndis-net_buffer_list_switch_forwarding_detail)宏获取克隆的数据包中的[**NDIS \_ 交换机 \_ 转发 \_ 详细信息 \_ \_ \_ \_ **](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_detail_net_buffer_list_info)联合。 扩展必须将 **IsPacketDataSafe** 成员设置为 TRUE。 这指定所有数据包数据都位于受信任的内存中。

筛选和转发扩展必须遵循以下准则，将克隆的数据包注入入入口或传出数据路径：

-   扩展必须调用 [**NdisFSendNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlists) ，以将克隆的数据包注入到入口数据路径。 扩展必须设置具有适当的可扩展开关标志设置的 *SendFlags* 参数。 有关这些标志设置的详细信息，请参阅 [Hyper-v 可扩展交换机发送和接收标志](hyper-v-extensible-switch-send-and-receive-flags.md)。

    当 NDIS 调用扩展的 [*FilterSendNetBufferListsComplete*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_send_net_buffer_lists_complete) 函数来完成克隆数据包的发送请求时，扩展必须调用 [*FreeNetBufferListForwardingContext*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_free_net_buffer_list_forwarding_context) 以释放已分配的转发上下文。 扩展必须在释放之前执行此操作，或重复用于数据包的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context) 结构。

    **注意**  如果该扩展修改了从出口数据路径获取的数据包数据或源端口，则该扩展必须将克隆的数据包注入到入口数据路径中。 如果未保留数据包的目标端口，还必须将克隆的数据包注入到入口数据路径中。



-   扩展必须调用 [**NdisFIndicateReceiveNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatereceivenetbufferlists) ，以将克隆的数据包注入传出数据路径。 扩展必须设置具有适当的可扩展开关标志设置的 *ReceiveFlags* 参数。

    当 NDIS 调用扩展的 [*FilterReturnNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_return_net_buffer_lists) 函数来完成克隆数据包的接收请求时，该扩展插件必须先调用 [*FreeNetBufferListForwardingContext*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_free_net_buffer_list_forwarding_context) ，然后才能释放或重复用于数据包的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context) 结构。

    **注意**  在转发扩展调用 [**NdisFIndicateReceiveNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatereceivenetbufferlists)之前，它必须已确定克隆的数据包的目标端口，并将此数据添加到数据包的 OOB 数据中。



-   如果扩展克隆了数据包的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context) 结构，则在克隆的发送或接收请求完成之前，必须保留原始数据包的 **网络 \_ 缓冲区 \_ 列表** 结构的所有权。 扩展必须使用克隆数据包的**网络 \_ 缓冲区 \_ 列表**结构的**ParentNetBufferList**成员链接到原始数据包的**网络 \_ 缓冲区 \_ 列表**结构。

    **注意**  在 NDIS 6.30 (Windows Server 2012) 中，扩展可以使用 **ParentNetBufferList** 成员链接到原始数据包，但这不是必需的。 在 NDIS 6.40 (Windows Server 2012 R2) 及更高版本中，需要使用 **ParentNetBufferList** 成员链接到原始数据包。

    克隆的数据包的发送或接收请求完成后，该扩展必须完成原始数据包的发送或接收请求。

    **注意**  如果扩展克隆了数据包的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context) 结构，则它可以在克隆后完成原始数据包的发送或接收请求。

-   如果扩展克隆了数据包，则它可以在克隆后立即完成原始数据包的发送或接收请求。

如果转发或筛选扩展在出口数据路径中获取了数据包，并且该扩展修改了数据包数据或更改了源端口，则无法在此数据路径中注入数据包的克隆版本。 但是，该扩展可以将这些数据包注入到入口数据路径中。 这样，便可以通过可扩展交换机数据路径正确转发和筛选数据包。

**注意**  如果未保留数据包的目标端口，筛选扩展只能将克隆的数据包注入到入口数据路径中。

例如，假设有多个目标端口的数据包是在可扩展交换机出口数据路径中获得的。 如果一个目标端口需要特殊处理（如数据封装），则转发或筛选扩展会按照以下步骤处理此操作：

1.  将数据包传递到需要特殊处理的端口。 此扩展通过将目标端口的[**NDIS \_ 交换机 \_ 端口 \_ 目标**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_port_destination)结构的**IsExcluded**成员设置为1的值来实现此目的。 有关此过程的详细信息，请参阅 [排除数据包传递到可扩展交换机目标端口](excluding-packet-delivery-to-extensible-switch-destination-ports.md)。

2.  克隆原始数据包，并执行所需的数据包数据处理。

    **注意**  筛选扩展不得为克隆的数据包添加目标端口。 此数据稍后将由可扩展交换机的转发扩展或微型端口边缘添加。

3.  通过调用 [**NdisMIndicateReceiveNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)，将源包转发到出口数据路径。

4.  通过调用 [**NdisFSendNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlists)，将克隆的数据包注入到入口数据路径。

有关可扩展交换机入口和出口数据路径的详细信息，请参阅 [Hyper-v 可扩展交换机数据路径](hyper-v-extensible-switch-data-path.md)。

**注意**  捕获扩展无法克隆数据包通信。 但是，它们可能会产生数据包流量。 有关详细信息，请参阅 [发起数据包流量](originating-packet-traffic.md)。
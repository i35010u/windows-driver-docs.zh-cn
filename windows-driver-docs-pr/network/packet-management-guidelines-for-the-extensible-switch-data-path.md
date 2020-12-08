---
title: 可扩展交换机数据路径的数据包管理指导原则
description: 可扩展交换机数据路径的数据包管理指导原则
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 73953f13ecca31031ca69694ed8989e615769414
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815915"
---
# <a name="packet-management-guidelines-for-the-extensible-switch-data-path"></a>可扩展交换机数据路径的数据包管理指导原则


本主题介绍 Hyper-v 可扩展交换机扩展必须遵循的指导原则，以便管理在可扩展交换机数据路径上获取的数据包。

**注意**  在可扩展交换机接口中，NDIS 筛选器驱动程序称为 *可扩展交换机扩展* ，驱动程序堆栈称为 *可扩展交换机驱动程序堆栈*。 有关扩展的详细信息，请参阅 [Hyper-v 可扩展交换机扩展](hyper-v-extensible-switch-extensions.md)。

 

**注意**  本页假设你熟悉 [Hyper-v 可扩展交换机](overview-of-the-hyper-v-extensible-switch.md) 和 [混合转发](hybrid-forwarding.md)概述中的信息和关系图。

 

对于可扩展交换机数据路径中的数据包管理，扩展必须遵循以下准则：

-   发起数据包的扩展必须调用 [**NdisFSendNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlists) ，以便在入口数据路径上启动发送请求。 必须以这种方式完成此操作，以允许通过可扩展交换机正确转发数据包。

-   捕获扩展可以监视可扩展交换机入口和出口数据路径上的数据包。 但是，这种类型的扩展必须始终转发数据包，并且不得丢弃数据包。 此外，捕获扩展不能在转发数据包之前修改包数据。

-   在可扩展交换机入口数据路径上，筛选和转发扩展可以执行以下操作：

    -   筛选扩展可以筛选数据包流量，并仅强制使用自定义端口或交换机策略来通过可扩展交换机进行数据包传送。 当扩展筛选入站数据路径中的数据包时，它只能基于源端口和数据包来源的网络适配器连接应用筛选规则。 此信息存储在数据包的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构的 OOB 数据中，可以通过使用 [**网络 \_ 缓冲区 \_ 列表 \_ 开关 \_ 转发 \_ 详细信息**](/windows-hardware/drivers/ddi/ndis/nf-ndis-net_buffer_list_switch_forwarding_detail) 宏获得。

        **注意**  在入口数据路径上获取的数据包不包含目标端口。 只能对在出口数据路径上获取的数据包进行基于目标端口的筛选包的筛选。

         

    -   转发扩展可以筛选数据包流量，并强制实施自定义和标准端口，或者通过可扩展交换机进行数据包传递的交换机策略。 当转发扩展筛选入站数据路径中的数据包时，它将基于源端口以及转发扩展分配给数据包的目标端口应用筛选规则。

-   在可扩展交换机出口数据路径上，筛选和转发扩展可以执行以下操作：

    -   筛选扩展可以筛选数据包流量，并仅强制使用自定义端口或交换机策略来通过可扩展交换机进行数据包传送。 当筛选扩展筛选出口数据路径中的数据包时，它只能基于数据包的目标端口应用筛选规则。

        目标端口数据存储在数据包的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构的 OOB 数据中。 扩展通过调用 [*GetNetBufferListDestinations*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_get_net_buffer_list_destinations) 函数获取此信息。

    -   转发扩展可以筛选数据包流量，并强制实施自定义和标准端口，或者通过可扩展交换机进行数据包传递的交换机策略。 当转发扩展筛选出口数据路径中的数据包时，它可以根据数据包的源或目标端口应用筛选规则。

    -   根据包上强制实施的策略，筛选或转发扩展可以排除将数据包传递到一个或多个目标。 有关此过程的详细信息，请参阅 [排除数据包传递到可扩展交换机目标端口](excluding-packet-delivery-to-extensible-switch-destination-ports.md)。

        根据包上强制实施的策略，转发扩展可以排除将数据包传递到一个或多个目标。 有关详细信息，请参阅 [混合转发](hybrid-forwarding.md)。

-   在可扩展交换机传出数据路径上，筛选和转发扩展不能执行以下操作：

    -   请在将数据包转发到出口数据路径之前修改数据包数据。

        如果筛选扩展需要修改数据包中的数据，则必须先克隆数据包，而不保留端口目标。 然后，该扩展插件必须将已修改的数据包注入入入口数据路径。 这允许基础扩展在已修改的数据包上强制实施策略，转发扩展可以添加端口目标。

        如果转发扩展需要修改数据包中的数据，则必须先克隆数据包，然后再分配端口目标。 在修改了数据包并分配了端口目标后，扩展必须将已修改的数据包注入到入口数据路径中。

        有关详细信息，请参阅 [克隆数据包通信](cloning-or-duplicating-packet-traffic.md)。

        **注意**  如果扩展克隆了在出口数据路径上获取的数据包，则只有在数据未更改数据包数据并保留原始目标端口数据的情况下，才能将新的数据包注入传出数据路径。

         

    -   转发数据包之前，将目标端口添加到数据包。

        **注意**  允许转发扩展将目标端口添加到在入口数据路径上获取的数据包。

         

    -   将新的或克隆的数据包插入传出数据路径。

-   在标准 NDIS 数据路径中，非可扩展交换机 OOB 数据通常具有不同的格式，具体取决于数据包是否被指示为发送或接收。 例如， [**NDIS \_ IPSEC \_ 卸载 \_ V2 \_ 标头 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v2_header_net_buffer_list_info) OOB 数据是发送和接收特定结构的联合。

    在可扩展交换机数据路径中，所有数据包都将通过扩展驱动程序堆栈，同时作为发送和接收。 因此，数据包的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构内的非可扩展 switch OOB 数据将在流通过驱动程序堆栈的整个持续时间内通过发送或接收格式进行。

    此 OOB 数据的格式取决于源可扩展交换机端口，数据包从该端口到达可扩展交换机。 如果源端口已连接到外部网络适配器，则非可扩展交换机 OOB 数据将采用接收格式。 对于其他端口，此 OOB 数据将为发送格式。

    **注意**  如果扩展克隆了数据包的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构，则在添加或修改 oob 数据时，必须考虑不可扩展的 oob 数据。 此扩展必须调用 [*CopyNetBufferListInfo*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_copy_net_buffer_list_info) ，将与可扩展交换机数据路径关联的 OOB 数据从源数据包复制到克隆的数据包。 将数据复制到克隆的数据包时，此函数将维护 OOB 发送或接收格式。

     

-   如果扩展从传出数据路径的入口中删除数据包，则必须调用 [*ReportFilteredNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_report_filtered_net_buffer_lists)。 调用此函数时，可扩展交换机接口会为删除或排除的数据包递增计数器和日志事件。

 


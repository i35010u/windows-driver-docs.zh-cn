---
title: 将数据包转发到物理网络适配器
description: 将数据包转发到物理网络适配器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e276fb87b7c388eae8569a4e82e01631a0755c9a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782265"
---
# <a name="forwarding-packets-to-physical-network-adapters"></a>将数据包转发到物理网络适配器


**注意**  本页假设你熟悉以下页面中的信息和关系图：
-   [转发扩展](forwarding-extensions.md)
-   [混合转发](hybrid-forwarding.md)
-   [Hyper-V 可扩展交换机扩展](hyper-v-extensible-switch-extensions.md)
-   [Hyper-V 可扩展交换机概述](overview-of-the-hyper-v-extensible-switch.md)
-   [组合提供程序扩展](teaming-provider-extensions.md)

 

本页介绍如何将 Hyper-v 可扩展交换机转发扩展转发到基础物理适配器的数据包发送请求。 一个或多个物理网络适配器可以绑定到可扩展交换机外部网络适配器。

例如，可扩展交换机外部网络适配器可以绑定到 NDIS 多路复用器 (MUX) 中间驱动程序的虚拟端口边缘。 MUX 中间驱动程序本身可以绑定到主机上一个或多个物理网络的团队。 此配置称为 *可扩展交换机团队*。 有关可扩展交换机团队的详细信息，请参阅 [物理网络适配器配置的类型](types-of-physical-network-adapter-configurations.md)。

在此配置中，可扩展交换机扩展会公开给可扩展交换机团队中的每个网络适配器。 这允许在可扩展交换机驱动程序堆栈中使用转发扩展来管理团队中单个网络适配器的配置和使用。 例如，扩展可以通过将传出数据包转发到各个适配器，为负载平衡故障转移 (LBFO) 解决方案提供支持。 例如，扩展称为 *组合提供程序*。 有关组合提供程序的详细信息，请参阅 [组合提供程序扩展](teaming-provider-extensions.md)。

如果在可扩展交换机驱动程序堆栈中安装并启用了转发扩展，则该扩展将负责为它在可扩展交换机入口数据路径上获取的每个数据包做出转发决策，除非数据包是 NVGRE 的数据包。  (有关 NVGRE 数据包的详细信息，请参阅 [混合转发](hybrid-forwarding.md)。 ) 根据这些转发决策，扩展可将目标端口添加到数据包的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构的带外 (OOB) 数据。 数据包完成可扩展交换机数据路径的遍历后，可扩展交换机接口会将数据包传递到指定的目标端口。

**注意**  如果未安装或启用转发扩展，则可扩展交换机本身会为它从入口数据路径获取的数据包做出转发决策。 此开关将目标端口添加到数据包的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构的 OOB 数据，然后将数据包上滚到可扩展的交换机传出数据路径。

 

调用转发扩展的 [*FilterSendNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_send_net_buffer_lists) 函数时， *NetBufferList* 参数包含指向 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构的链接列表的指针。 其中每个结构都指定从入口数据路径获取的数据包。 在每个数据包的 **网络 \_ 缓冲区 \_ 列表** 结构的 OOB 数据内，目标端口的数据包含在 [**NDIS \_ 交换机 \_ 转发 \_ 目标 \_ 数组**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_destination_array) 结构中。 扩展通过调用 [*GetNetBufferListDestinations*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_get_net_buffer_list_destinations)来获取 **NDIS \_ 交换机 \_ 转发 \_ 目标 \_ 数组** 结构及其元素。

**注意**  为了提高性能，转发扩展可以调用 [*GrowNetBufferListDestinations*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_grow_net_buffer_list_destinations) 函数而不是 [*GetNetBufferListDestinations*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_get_net_buffer_list_destinations) 来获取指向 [**NDIS \_ 交换机 \_ 转发 \_ 目标 \_ 数组**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_destination_array) 结构的指针。 如果扩展确定它需要数据包的 OOB 数据中的目标端口的其他数组元素，则扩展将执行此项。 有关详细信息，请参阅 [将可扩展交换机目标端口数据添加到数据包](adding-extensible-switch-destination-port-data-to-a-packet.md)。

 

[**Ndis \_ 交换机 \_ 转发 \_ 目标 \_ 数组**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)数组中的每个元素都定义一个目标端口，并将其格式化为 [**NDIS \_ 交换机 \_ 端口 \_ 目标**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_port_destination)结构。 此结构包含以下成员：

-   **PortId** 成员包含一个值，该值指定可扩展交换机上的目标端口。

-   **NicIndex** 成员指定连接到 **PortId** 成员指定的可扩展交换机端口的网络适配器的索引。

    有关这些索引值的详细信息，请参阅 [网络适配器索引值](network-adapter-index-values.md)。

如果转发扩展插件添加了连接到外部网络适配器的目标端口，则该扩展可以指定底层物理网络适配器的索引。 例如，扩展可以作为组合提供程序在可扩展交换机团队上的 LBFO 支持下运行。 这使该扩展可以通过将发送请求转发到团队的不同适配器来平衡流量开销。

当转发扩展添加或修改 [**NDIS \_ 交换机 \_ 端口 \_ 目标**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_port_destination) 结构以将发送请求转发到基础物理网络适配器时，必须遵循以下指导原则：

-   如果 **PortId** 成员指定将外部网络适配器连接到的可扩展交换机端口，则扩展必须将 **NicIndex** 成员设置为以下索引值之一：

    -   如果仅有一个物理网络适配器绑定到外部网络适配器，则扩展必须将 **NicIndex** 成员设置为 **NDIS \_ 切换 \_ 默认 \_ NIC \_ 索引** 或一个。

    -   如果将多个物理网络适配器绑定到外部网络适配器，则扩展必须将 **NicIndex** 成员设置为可扩展交换机团队中目标网络适配器的非零索引值。

    **注意**  如果 **PortId** 成员未指定将外部网络适配器连接到的可扩展交换机端口，则扩展必须将 **NicIndex** 成员设置为 **NDIS \_ 交换机 \_ 默认 \_ NIC \_ 索引**。

     

-   扩展添加了包的所有目标端口之后，必须调用 [**NdisFSendNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlists) ，将数据包转发到入口数据路径。

有关如何将目标端口添加到数据包的详细信息，请参阅将 [数据包转发到 Hyper-v 可扩展交换机端口](forwarding-packets-to-hyper-v-extensible-switch-ports.md)。

有关出口数据路径的详细信息，请参阅 [Hyper-v 可扩展交换机数据路径](hyper-v-extensible-switch-data-path.md)。

 


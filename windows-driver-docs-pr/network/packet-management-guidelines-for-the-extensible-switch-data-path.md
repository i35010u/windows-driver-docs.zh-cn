---
title: 可扩展交换机数据路径的数据包管理指导原则
description: 可扩展交换机数据路径的数据包管理指导原则
ms.assetid: 18B2BCBA-8428-45CF-93A0-8F7182DBCAA2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 937d44e9225782b64a67577c288c72bb1b61875f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67357602"
---
# <a name="packet-management-guidelines-for-the-extensible-switch-data-path"></a>可扩展交换机数据路径的数据包管理指导原则


本主题介绍 HYPER-V 可扩展交换机扩展用于管理在可扩展交换机数据路径上获得的数据包必须遵循的准则。

**请注意**  可扩展交换机接口，在 NDIS 筛选器驱动程序被称为*可扩展交换机扩展*驱动程序堆栈称为*可扩展交换机驱动程序堆栈*. 有关扩展的详细信息，请参阅[HYPER-V 可扩展交换机扩展](hyper-v-extensible-switch-extensions.md)。

 

**请注意**  此页面假定您熟悉的信息和中的关系图[概述的 HYPER-V 可扩展交换机](overview-of-the-hyper-v-extensible-switch.md)并[混合转发](hybrid-forwarding.md)。

 

扩展必须遵循这些准则以可扩展交换机数据路径中的包管理：

-   源自数据包的扩展必须调用[ **NdisFSendNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfsendnetbufferlists)启动入口数据路径上的发送请求。 这必须实现这种方式，以便正确转发的数据包通过可扩展的交换机。

-   捕获扩展可以监视可扩展交换机入口和出口数据路径上的数据包。 但是，此类型的扩展必须始终转发数据包，并且必须不丢弃数据包。 此外，捕获扩展不能修改数据包数据之前它将数据包转发。

-   可扩展交换机入口数据路径，在筛选和转发扩展可以执行以下操作：

    -   筛选扩展时，可以筛选数据包流量和强制实施仅自定义端口或切换通过可扩展交换机的数据包传递的策略。 当扩展筛选器中的入口数据路径的数据包时，它仅可应用仅根据数据包的起源的源端口和网络适配器连接的筛选规则。 此信息存储在数据包的 OOB 数据[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构并且可以通过使用获取[ **NET\_缓冲区\_列表\_交换机\_转发\_详细信息**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-switch-forwarding-detail)宏。

        **请注意**  获取入口数据路径上的数据包不包含目标端口。 筛选基于目标端口的数据包只能获取出口数据路径上的数据包上完成。

         

    -   转发扩展时，可以筛选数据包流量和强制实施自定义和标准端口或切换通过可扩展交换机的数据包传递的策略。 当转发扩展筛选器中的入口数据路径的数据包时，则会应用基于源端口，以及转发扩展将分配给该数据包的目标端口的筛选规则。

-   可扩展交换机出口数据路径，在筛选和转发扩展可以执行以下操作：

    -   筛选扩展时，可以筛选数据包流量和强制实施仅自定义端口或切换通过可扩展交换机的数据包传递的策略。 筛选扩展筛选器的出口数据路径中的数据包，它可以应用筛选规则仅基于数据包的目标端口。

        目标端口数据存储在数据包的 OOB 数据[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构。 扩展插件获取此信息通过调用[ *GetNetBufferListDestinations* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_get_net_buffer_list_destinations)函数。

    -   转发扩展时，可以筛选数据包流量和强制实施自定义和标准端口或切换通过可扩展交换机的数据包传递的策略。 转发扩展筛选器的出口数据路径中的数据包，它可以应用基于数据包的源或目标端口的筛选规则。

    -   根据数据包上强制执行的策略，则可以将筛选或转发扩展排除数据包传递到一个或多个目标。 此过程的详细信息，请参阅[可扩展交换机目标端口不包括数据包传递](excluding-packet-delivery-to-extensible-switch-destination-ports.md)。

        根据数据包上强制执行的策略，转发扩展可以排除数据包传递到一个或多个目标。 有关详细信息，请参阅[混合转发](hybrid-forwarding.md)。

-   可扩展交换机出口数据路径上筛选和转发扩展必须执行以下操作：

    -   转发的出口数据路径上的数据包之前修改的数据包数据。

        如果筛选扩展需要修改在包中的数据，必须先克隆数据包而无需保留端口的目标。 然后，该扩展必须将修改后的数据包注入到入口数据路径。 这允许修改数据包上强制实施策略的基础扩展并转发扩展可以添加端口的目标。

        如果转发扩展需要修改在包中的数据，必须先克隆该数据包之前它将分配端口的目标。 该数据包已分配的已修改和端口目标后，该扩展必须将修改后的数据包注入到入口数据路径。

        有关详细信息，请参阅[克隆数据包流量](cloning-or-duplicating-packet-traffic.md)。

        **请注意**  如果扩展克隆的数据包，出口数据路径上获得，它可以注入新的数据包的出口数据路径仅当它未更改的数据包数据，并且已保留原始的目标端口数据。

         

    -   转发数据包之前将目标端口添加到该数据包。

        **请注意**  转发扩展允许将目标端口添加到获取入口数据路径上的数据包。

         

    -   出口数据路径中注入新的或克隆的数据包。

-   在标准的 NDIS 数据路径中，非可扩展交换机 OOB 数据通常具有不同的格式，具体取决于是否指示为发送或接收数据包。 例如， [ **NDIS\_IPSEC\_卸载\_V2\_标头\_NET\_缓冲区\_列表\_信息** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_ipsec_offload_v2_header_net_buffer_list_info) OOB 数据是发送一个联合的和特定于接收的结构。

    在可扩展交换机数据路径中，所有数据包移动到每个扩展驱动程序堆栈上为同时发送和接收。 因此，非可扩展交换机 OOB 数据中的数据包[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构将在发送或接收的格式通过驱动程序堆栈的流。

    此 OOB 数据的格式取决于源可扩展交换机端口从该数据包到达可扩展交换机。 如果源端口连接到外部网络适配器，非可扩展交换机 OOB 数据将为接收格式。 对于其他端口，此 OOB 数据将发送格式。

    **请注意**  如果扩展克隆的数据包[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构，它必须执行非可扩展交换机 OOB 数据插入如果它将添加或修改 OOB 数据中不考虑。 扩展必须调用[ *CopyNetBufferListInfo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_copy_net_buffer_list_info)克隆数据包从一个源数据包的可扩展交换机数据路径与相关联的 OOB 数据复制。 此函数将维护 OOB 发送或接收格式时将数据复制到克隆的数据包。

     

-   如果扩展从出口数据路径入口中删除一个数据包，它必须调用[ *ReportFilteredNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_report_filtered_net_buffer_lists)。 当调用此函数时，可扩展交换机接口递增计数器和日志的已删除或排除数据包的事件。

 

 






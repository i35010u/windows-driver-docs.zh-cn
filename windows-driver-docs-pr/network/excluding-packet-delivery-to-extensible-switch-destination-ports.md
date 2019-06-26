---
title: 排除将数据包传送到可扩展交换机目标端口
description: 排除将数据包传送到可扩展交换机目标端口
ms.assetid: 04BF02A6-360F-482E-A86B-31232AFCB778
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ceec5f4fd29ef389d3abbdde5cd832c207d835b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353758"
---
# <a name="excluding-packet-delivery-to-extensible-switch-destination-ports"></a>排除将数据包传送到可扩展交换机目标端口


本主题介绍 HYPER-V 可扩展交换机扩展可以如何排除数据包传送到可扩展的交换机端口。 带外 (OOB) 转发的数据包内的上下文内指定数据包的目标端口[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构。 在此上下文的详细信息，请参阅[HYPER-V 可扩展交换机转发上下文](hyper-v-extensible-switch-forwarding-context.md)。

**请注意**此页面假定您熟悉的信息和中的关系图[概述的 HYPER-V 可扩展交换机](overview-of-the-hyper-v-extensible-switch.md)并[混合转发](hybrid-forwarding.md)。


**请注意**可扩展交换机接口，在 NDIS 筛选器驱动程序被称为*可扩展交换机扩展*驱动程序堆栈称为*可扩展交换机驱动程序堆栈*。 有关扩展的详细信息，请参阅[HYPER-V 可扩展交换机扩展](hyper-v-extensible-switch-extensions.md)。

筛选和转发扩展可以排除在可扩展交换机入口或出口数据路径上获得的数据包的传递。 可通过以下方式不包括的数据包发送：

-   该扩展可以通过完成数据包请求或指示丢弃该数据包。 这不包括任何可扩展交换机端口的数据包传送。 此方法可以有一个或多个目标端口的数据包上使用。

    对于在可扩展交换机入口数据路径上获得的数据包，该扩展将通过调用完成数据包发送请求[ **NdisFSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfsendnetbufferlistscomplete)。

    对于在可扩展交换机出口数据路径上获得的数据包，该扩展完成数据包通过调用会收到指示[ **NdisFReturnNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreturnnetbufferlists)。

-   在具有多个目标端口的出口数据路径上获得的数据包，扩展可以通过修改一个或多个目标端口的数据中排除的数据包发送。 通过设置的扩展插件实现这**IsExcluded**成员的目标端口[ **NDIS\_开关\_端口\_目标**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_port_destination)结构的值。 此方法允许要发送到这些端口的数据包**IsExcluded**值设置为零。

    **请注意**获取入口数据路径上的数据包不包含目标端口。 可扩展交换机将向上出口数据路径数据包转发后，此数据才可用。

该扩展已修改的目标端口后**IsExcluded**值，它必须将数据包转发到过量扩展的出口数据路径中。 但是，如果**IsExcluded**数据包的目标端口的数据设置为 1，该扩展应放置通过完成数据包的数据包会收到指示而不是将其转发。

**请注意**扩展已设置的目标端口后**IsExcluded**过量的出口数据路径上的扩展的值为 1，不能更改此值为零。

**请注意**捕获扩展不能排除数据包传送到可扩展的交换机端口。

筛选和转发扩展必须遵循以下准则，以便不包括到可扩展交换机端口的数据包发送：

-   在可扩展交换机入口数据路径上筛选和转发扩展可以排除基于策略条件的数据包的源端口或数据的数据包发送。

    源端口信息存储在[ **NDIS\_交换机\_转发\_详细信息\_NET\_缓冲区\_列表\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_forwarding_detail_net_buffer_list_info)数据包的 OOB 数据中联合[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构。 该扩展使用获取数据[ **NET\_缓冲区\_列表\_开关\_转发\_详细**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-switch-forwarding-detail)宏。

    如果扩展不包括从入口数据路径获取的数据包的传递，它必须通过完成数据包发送请求来丢弃该数据包。

-   可扩展交换机入口数据路径上转发扩展确定数据包的目标端口，并将此信息添加到 OOB 数据包。 基于策略条件的扩展插件强制执行，它可以通过不将其目标端口信息添加到 OOB 数据中排除的数据包发送到端口。

    有关此过程的详细信息，请参阅[添加可扩展交换机目标将数据转到数据包](adding-extensible-switch-destination-port-data-to-a-packet.md)。

-   在可扩展交换机出口数据路径上筛选和转发扩展可以排除策略条件的数据包的传递。 例如，筛选扩展可以排除基于策略条件的数据包的源端口或多个目标端口的数据包发送。

    扩展排除数据包传递到目标端口按照以下步骤：

    1.  该扩展通过调用获取数据包的目标端口[ *GetNetBufferListDestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_get_net_buffer_list_destinations)。 如果调用返回 NDIS\_状态\_成功后，*目标*参数包含一个指向[ **NDIS\_交换机\_转发\_目标\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)结构。 此结构指定数据包的可扩展交换机目标端口。 每个目标端口的格式设置为[ **NDIS\_交换机\_端口\_目标**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_port_destination)结构。

        **请注意**如果**NumDestinations**的成员[ **NDIS\_开关\_转发\_目标\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)结构包含的值为零，数据包的目标端口的任何数据。

2.  该扩展通过设置排除可扩展交换机端口的数据包交付**IsExcluded**成员的目标端口[ **NDIS\_切换\_端口\_目标**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_port_destination)为其中一个的值的结构。

    **请注意**如果扩展不包括数据包传递到所有其目标端口，该扩展必须丢弃该数据包通过完成的数据包会收到指示。

3.  如果扩展不包括传递到在包中的一个或所有目标端口，它必须执行以下操作：

    -   扩展必须调用[ *UpdateNetBufferListDestinations* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_update_net_buffer_list_destinations)来提交这些更改对数据包的 OOB 数据。

    -   扩展必须调用[ *ReportFilteredNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_report_filtered_net_buffer_lists)。 当调用此函数时，可扩展交换机接口递增计数器和日志对于排除数据包的事件。 扩展必须进行此调用之前将转发它从中获取数据包的可扩展交换机数据路径中的数据包。

    同样，如果要排除传递到数据包的所有端口的数据包发送请求或指示，该扩展完成后，它还必须调用[ *ReportFilteredNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_report_filtered_net_buffer_lists)。

    **请注意**扩展可创建的链接的列表[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)不包括该扩展的数据包的结构。 当扩展调用[ *ReportFilteredNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_report_filtered_net_buffer_lists)，它会设置*NetBufferLists*为指向链接列表的参数。

有关可扩展交换机入口和出口数据路径的详细信息，请参阅[HYPER-V 可扩展交换机数据路径](hyper-v-extensible-switch-data-path.md)。
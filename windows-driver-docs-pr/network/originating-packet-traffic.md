---
title: 发起数据包流量
description: 发起数据包流量
ms.assetid: 613C7E82-387D-47AE-A699-A799087D3C1D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50081c0012b757f426b66c5e600910df1b7897c6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843758"
---
# <a name="originating-packet-traffic"></a>发起数据包流量


本主题介绍了 Hyper-v 扩展如何产生新的数据包并将其注入可扩展交换机数据路径。

**请注意**  本页假设你熟悉[hyper-v 可扩展交换机](overview-of-the-hyper-v-extensible-switch.md)和[混合转发](hybrid-forwarding.md)概述中的信息和关系图。

 

**注意**  在可扩展交换机接口中，NDIS 筛选器驱动程序称为*可扩展交换机扩展*，驱动程序堆栈称为*可扩展交换机驱动程序堆栈*。 有关扩展的详细信息，请参阅[Hyper-v 可扩展交换机扩展](hyper-v-extensible-switch-extensions.md)。

 

可扩展交换机扩展只能将新的数据包注入到可扩展的交换机入口数据路径。 这可确保可扩展交换机接口可以正确地筛选和转发这些数据包。 扩展必须遵循以下准则，将新的数据包注入到入口数据路径：

-   扩展必须首先为新数据包分配一个[**网络\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context)结构。

-   扩展为新的数据包分配了[**网络\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context)结构后，它必须调用[*AllocateNetBufferListForwardingContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_allocate_net_buffer_list_forwarding_context)处理程序函数，以便为数据包分配可扩展的切换转发上下文。

    转发上下文位于数据包的带外（OOB）数据中。 它包含数据包的转发信息，如其源端口和一个或多个目标端口的数组。

    有关转发上下文的详细信息，请参阅[Hyper-v 可扩展交换机转发上下文](hyper-v-extensible-switch-forwarding-context.md)。

-   扩展调用[*AllocateNetBufferListForwardingContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_allocate_net_buffer_list_forwarding_context)后，数据包的源端口将设置为**NDIS\_交换机\_默认\_端口\_ID**。 具有 NDIS\_交换机的源端口标识符的数据包 **\_默认\_端口\_ID**是受信任的，并且会绕过可扩展交换机端口策略，如访问控制列表（acl）和服务质量（QoS）。

    扩展可能需要将数据包视为来自特定端口。 这允许将该端口的策略应用到该数据包。 该扩展调用[*SetNetBufferListSource*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_set_net_buffer_list_source)来更改数据包的源端口。

    但在某些情况下，扩展可能需要将数据包的源端口标识符分配给**NDIS\_交换机\_默认\_端口\_ID**。 例如，扩展可能需要将源端口标识符设置为**NDIS\_交换机\_默认\_端口\_ID**发送到外部网络上的设备的专用控制数据包。

-   如果转发扩展在入口数据路径上发送新的数据包，则必须确定数据包的目标端口。 有关此过程的详细信息，请参阅[将可扩展交换机目标端口数据添加到数据包](adding-extensible-switch-destination-port-data-to-a-packet.md)。

    **请注意**  捕获或筛选扩展不能将新的目标端口添加到新的包。

     

-   当扩展创建新数据包时，数据包数据位于 Hyper-v 父分区的父操作系统中的 "本地" 或 "*受信任*的内存" 中。 子分区无法访问此内存。 因此，在该分区中运行的来宾操作系统不同步更新将其视为 "安全"。

    该扩展必须获取[**NDIS\_交换机\_转发\_详细信息\_net\_buffer\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_detail_net_buffer_list_info)使用[**net\_buffer\_list\_\_转发\_详细**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-switch-forwarding-detail)的宏。 扩展必须将**IsPacketDataSafe**成员设置为 TRUE。 这指定所有数据包数据都位于受信任的内存中。

-   当扩展调用[**NdisFSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlists)将数据包注入入入口数据路径时，它必须设置*标志*参数和相应的可扩展开关标志设置。 有关这些标志设置的详细信息，请参阅[Hyper-v 可扩展交换机发送和接收标志](hyper-v-extensible-switch-send-and-receive-flags.md)。

-   当 NDIS 调用扩展的[*FilterSendNetBufferListsComplete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_send_net_buffer_lists_complete)函数来完成新包的发送请求时，扩展必须调用[*FreeNetBufferListForwardingContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_free_net_buffer_list_forwarding_context)以释放已分配的转发上下文。 扩展必须在释放之前执行此操作，或重用包的[**NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context)结构。

有关可扩展交换机入口和出口数据路径的详细信息，请参阅[Hyper-v 可扩展交换机数据路径](hyper-v-extensible-switch-data-path.md)。

 

 






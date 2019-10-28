---
title: 管理 Hyper-V 可扩展交换机转发上下文
description: 管理 Hyper-V 可扩展交换机转发上下文
ms.assetid: 63FBEBFA-BD57-4350-89C3-9F0FAAA18973
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6585863b7de553d8df2e4cb866f27668eebf42ca
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844110"
---
# <a name="managing-the-hyper-v-extensible-switch-forwarding-context"></a>管理 Hyper-V 可扩展交换机转发上下文


**注意** 本页假设你熟悉[Hyper-v 可扩展交换机](overview-of-the-hyper-v-extensible-switch.md)和[混合转发](hybrid-forwarding.md)概述中的信息和关系图。



遍历 Hyper-v 可扩展交换机数据路径的每个数据包的[**NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构包含带外（OOB）数据。 此数据指定从其发起数据包的源端口，以及用于数据包传递的一个或多个目标端口。 此 OOB 数据称为*可扩展交换机转发上下文*。

**注意** 可扩展交换机转发上下文不同于[**NET\_缓冲区\_列表\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context)结构。 这允许扩展分配其自己的上下文结构，而不会影响转发上下文。

可扩展交换机转发上下文的分配和释放方式如下：

-   当数据包到达网络适配器的可扩展交换机时，可扩展交换机接口会分配转发上下文，并将其与数据包的[**网络\_缓冲区关联\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构。

    当数据包传送到其目标端口时，接口将从数据包的[**NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)中释放转发上下文\_列表结构。

-   如果可扩展交换机扩展将新的或克隆的数据包注入到可扩展交换机数据路径，则必须在调用[**NdisFSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlists)之前分配转发上下文。

    扩展为新的或克隆的数据包分配了[**网络\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context)结构后，它必须调用[*AllocateNetBufferListForwardingContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_allocate_net_buffer_list_forwarding_context)函数来为数据包分配转发上下文。 发送数据包请求完成后，扩展必须先调用[*FreeNetBufferListForwardingContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_free_net_buffer_list_forwarding_context) ，然后才能释放或重用**NET\_缓冲区\_列表**结构。

    **注意** 当扩展调用[*AllocateNetBufferListForwardingContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_allocate_net_buffer_list_forwarding_context)时，数据包的源端口将设置为**NDIS\_交换机\_默认\_端口\_ID**。 这会指定数据包源自扩展，而不是到达可扩展的交换机端口。 在某些情况下，扩展可能需要更改数据包的源端口。 有关详细信息，请参阅[修改数据包的可扩展交换机源端口数据](modifying-a-packet-s-extensible-switch-source-port-data.md)。

    有关详细信息，请参阅[Hyper-v 可扩展交换机发送和接收操作](hyper-v-extensible-switch-send-and-receive-operations.md)。

所有可扩展交换机扩展都可以调用以下可扩展交换机处理程序函数来访问数据包转发上下文中的数据：

<a href="" id="allocatenetbufferlistforwardingcontext"></a>[*AllocateNetBufferListForwardingContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_allocate_net_buffer_list_forwarding_context)  
分配可扩展交换机转发上下文并为可扩展交换机内的发送或接收操作准备[**NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构。

<a href="" id="copynetbufferlistinfo"></a>[*CopyNetBufferListInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_copy_net_buffer_list_info)  
将源包的[**网络\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context)结构的转发上下文复制到目标数据包的**网络\_缓冲区\_列表**结构。 此数据包括可扩展的交换机源端口和网络适配器信息。 可扩展交换机目标端口信息也可以复制到目标数据包。

<a href="" id="freenetbufferlistforwardingcontext"></a>[*FreeNetBufferListForwardingContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_free_net_buffer_list_forwarding_context)  
在[**网络\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)的可扩展交换机转发上下文中释放资源\_列表结构。 此数据用于 Hyper-v 可扩展交换机中的发送或接收操作，以前通过调用[*AllocateNetBufferListForwardingContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_allocate_net_buffer_list_forwarding_context)函数进行了分配。

<a href="" id="getnetbufferlistdestinations"></a>[*GetNetBufferListDestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_get_net_buffer_list_destinations)  
从数据包的[**网络\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context)结构的转发上下文返回目标端口。

转发扩展负责为数据包添加目标端口，除非数据包为 NVGRE 数据包。 （有关详细信息，请参阅[混合转发](hybrid-forwarding.md)。）该扩展调用下列可扩展的 switch 处理程序函数来添加或更新数据包转发上下文中的目标端口：

<a href="" id="addnetbufferlistdestination"></a>[*AddNetBufferListDestination*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_add_net_buffer_list_destination)  
将单个目标添加到[**网络\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context)结构指定的数据包的可扩展交换机转发上下文区域。

**注意** 此调用会将更改提交到转发上下文区域。 在这种情况下，转发扩展不需要调用[*UpdateNetBufferListDestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_update_net_buffer_list_destinations)。

<a href="" id="grownetbufferlistdestinations"></a>[*GrowNetBufferListDestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_grow_net_buffer_list_destinations)  
增加数据包的[**网络\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context)结构的转发上下文区域中目标端口数组的大小。

<a href="" id="updatenetbufferlistdestinations"></a>[*UpdateNetBufferListDestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_update_net_buffer_list_destinations)  
提交扩展对包的一个或多个可扩展交换机目标端口所做的修改。 此函数使用这些更改来更新包的[**网络\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context)结构的转发上下文。

**注意** 转发扩展将目标端口的更改提交到转发上下文后，不能删除目标端口，并且仅**IsExcluded**目标端口[**NDIS\_交换机\_端口\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_port_destination)可以更改目标结构。 有关详细信息，请参阅[排除数据包传递到可扩展交换机目标端口](excluding-packet-delivery-to-extensible-switch-destination-ports.md)。

## <a name="related-topics"></a>相关主题


[Hyper-v 可扩展交换机转发上下文](hyper-v-extensible-switch-forwarding-context.md)

[Hyper-v 可扩展交换机转发上下文数据类型](hyper-v-extensible-switch-forwarding-context-data-types.md)











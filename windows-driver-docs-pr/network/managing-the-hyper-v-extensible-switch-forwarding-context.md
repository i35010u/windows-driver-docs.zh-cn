---
title: 管理 Hyper-V 可扩展交换机转发上下文
description: 管理 Hyper-V 可扩展交换机转发上下文
ms.assetid: 63FBEBFA-BD57-4350-89C3-9F0FAAA18973
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8731474d11f5d40b98e1f1136466a6bf82e16f8b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369185"
---
# <a name="managing-the-hyper-v-extensible-switch-forwarding-context"></a>管理 Hyper-V 可扩展交换机转发上下文


**请注意**此页面假定您熟悉的信息和中的关系图[概述的 HYPER-V 可扩展交换机](overview-of-the-hyper-v-extensible-switch.md)并[混合转发](hybrid-forwarding.md)。



[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构为每个数据包的传输的 HYPER-V 可扩展交换机数据路径包含带外 (OOB) 数据。 此数据指定从数据包源于何处，以及数据包传递的一个或多个目标端口的源端口。 此 OOB 数据被称为*可扩展交换机转发上下文*。

**请注意**可扩展交换机转发上下文是不同于[ **NET\_缓冲区\_列表\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list_context)结构。 这允许扩展而不会影响转发上下文分配他们自己的上下文结构。

可扩展交换机转发上下文进行分配和释放如下所示：

-   当数据包到达从网络适配器的可扩展交换机时，可扩展交换机接口分配转发上下文，并将其与数据包的关联[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构。

    该接口时将数据包发送到其目标端口，释放来自数据包转发上下文[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构。

-   如果可扩展交换机扩展将新的或克隆数据包注入到可扩展交换机数据路径，它必须分配转发上下文调用之前[ **NdisFSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfsendnetbufferlists)。

    扩展分配后[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list_context)结构对于新的或克隆数据包时，它必须调用[ *AllocateNetBufferListForwardingContext* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_allocate_net_buffer_list_forwarding_context)函数以分配为数据包转发上下文。 该扩展时发送数据包请求完成时，必须调用[ *FreeNetBufferListForwardingContext* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_free_net_buffer_list_forwarding_context)它释放或重新使用之前**NET\_缓冲区\_列表**结构。

    **请注意**则扩展将调用时[ *AllocateNetBufferListForwardingContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_allocate_net_buffer_list_forwarding_context)，数据包的源端口设置为**NDIS\_交换机\_默认\_端口\_ID**。 这将指定数据包源自而不是传入到可扩展交换机端口的扩展。 某些情况下，该扩展可能需要更改数据包的源端口。 有关详细信息，请参阅[修改数据包的可扩展交换机的源端口数据](modifying-a-packet-s-extensible-switch-source-port-data.md)。

    有关详细信息，请参阅[HYPER-V 可扩展交换机发送和接收操作](hyper-v-extensible-switch-send-and-receive-operations.md)。

所有可扩展交换机扩展可以调用以下可扩展交换机访问内部的数据包转发上下文数据的处理程序函数：

<a href="" id="allocatenetbufferlistforwardingcontext"></a>[*AllocateNetBufferListForwardingContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_allocate_net_buffer_list_forwarding_context)  
分配可扩展交换机转发上下文，并准备[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构发送或接收可扩展交换机中的操作。

<a href="" id="copynetbufferlistinfo"></a>[*CopyNetBufferListInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_copy_net_buffer_list_info)  
从一个源数据包将转发上下文[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list_context)目标数据包的结构**NET\_缓冲区\_列表**结构。 此数据包括可扩展交换机源端口和网络适配器信息。 可扩展交换机目标端口信息也可以复制到目标数据包。

<a href="" id="freenetbufferlistforwardingcontext"></a>[*FreeNetBufferListForwardingContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_free_net_buffer_list_forwarding_context)  
释放的可扩展交换机转发上下文中的资源[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构。 此数据用于发送或接收操作中的 HYPER-V 可扩展交换机，并通过调用以前分配[ *AllocateNetBufferListForwardingContext* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_allocate_net_buffer_list_forwarding_context)函数。

<a href="" id="getnetbufferlistdestinations"></a>[*GetNetBufferListDestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_get_net_buffer_list_destinations)  
返回目标端口转发的数据包的上下文中[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list_context)结构。

转发扩展负责添加目标端口的数据包，除非该数据包是 NVGRE 数据包。 (有关详细信息，请参阅[混合转发](hybrid-forwarding.md)。)扩展将调用以下可扩展交换机处理程序函数来添加或更新的数据包转发上下文中的目标端口：

<a href="" id="addnetbufferlistdestination"></a>[*AddNetBufferListDestination*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_add_net_buffer_list_destination)  
将单个目标添加到转发的数据包，由指定的上下文区域的可扩展交换机[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list_context)结构。

**请注意**此调用将更改提交给转发上下文区域。 在这种情况下，转发扩展不需要调用[ *UpdateNetBufferListDestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_update_net_buffer_list_destinations)。

<a href="" id="grownetbufferlistdestinations"></a>[*GrowNetBufferListDestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_grow_net_buffer_list_destinations)  
在转发的目标端口数组的大小增加的数据包的上下文区域[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list_context)结构。

<a href="" id="updatenetbufferlistdestinations"></a>[*UpdateNetBufferListDestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_update_net_buffer_list_destinations)  
提交对一个或多个可扩展交换机目标端口的数据包的扩展所做的修改。 此函数会更新的数据包转发上下文[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list_context)结构使用这些更改。

**请注意**转发扩展转发上下文提交的更改的目标端口后，目标端口不能为已删除和唯一**IsExcluded**成员的目标端口的[**NDIS\_交换机\_端口\_目标**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_port_destination)结构可以进行更改。 有关详细信息，请参阅[可扩展交换机目标端口不包括数据包传递](excluding-packet-delivery-to-extensible-switch-destination-ports.md)。

## <a name="related-topics"></a>相关主题


[HYPER-V 可扩展交换机转发上下文](hyper-v-extensible-switch-forwarding-context.md)

[HYPER-V 可扩展交换机转发上下文数据类型](hyper-v-extensible-switch-forwarding-context-data-types.md)











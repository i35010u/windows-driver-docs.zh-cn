---
title: 查询数据包的可扩展交换机目标端口数据
description: 查询数据包的可扩展交换机目标端口数据
ms.assetid: 57D82C5E-3758-492C-A1DA-B7BC3DBE2E7A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16fea316b83e7afb98a77983a91edf4d1d15d0a5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385440"
---
# <a name="querying-a-packets-extensible-switch-destination-port-data"></a>查询数据包的可扩展交换机目标端口数据


通过指定每个 HYPER-V 可扩展交换机目标端口[ **NDIS\_切换\_端口\_目标**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_port_destination)中的元素[ **NDIS\_交换机\_转发\_目标\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)结构。 此数组包含在带外 (OOB) 转发的数据包的上下文[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构。 在此上下文的详细信息，请参阅[HYPER-V 可扩展交换机转发上下文](hyper-v-extensible-switch-forwarding-context.md)。

可扩展交换机扩展调用[ *GetNetBufferListDestinations* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_get_net_buffer_list_destinations)函数来获取的指针[ **NDIS\_切换\_转发\_目标\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)中的数据包的结构[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构。 各个[ **NDIS\_交换机\_端口\_目标**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_port_destination)可以通过访问此结构中的元素[ **NDIS\_交换机\_端口\_目标\_处\_数组\_索引**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-switch-port-destination-at-array-index)宏。

若要提高性能，转发扩展可以调用[ *GrowNetBufferListDestinations* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_grow_net_buffer_list_destinations)函数而不是[ *GetNetBufferListDestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_get_net_buffer_list_destinations)若要获取的指针[ **NDIS\_交换机\_转发\_目标\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)结构. 扩展执行此操作如果确定它需要为目标端口的数据包的 OOB 数据中的其他数组元素。 有关详细信息，请参阅[添加可扩展交换机目标将数据转到数据包](adding-extensible-switch-destination-port-data-to-a-packet.md)。

**请注意**  只有数据包从此可扩展交换机出口数据路径将包含目标端口信息。 有关详细信息，请参阅[HYPER-V 可扩展交换机数据路径](hyper-v-extensible-switch-data-path.md)。

 

 

 






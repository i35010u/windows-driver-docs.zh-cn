---
title: 查询数据包的可扩展交换机目标端口数据
description: 查询数据包的可扩展交换机目标端口数据
ms.assetid: 57D82C5E-3758-492C-A1DA-B7BC3DBE2E7A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5dd5ed6fc79176bc7568dd65c37ab991320608d4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844888"
---
# <a name="querying-a-packets-extensible-switch-destination-port-data"></a>查询数据包的可扩展交换机目标端口数据


每个 Hyper-v 可扩展交换机目标端口都是由 ndis [ **\_交换机\_端口\_目标**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_port_destination)元素指定[ **\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)的。端口. 此数组包含在数据包的[**网络\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)的带外（OOB）转发上下文\_列表结构。 有关此上下文的详细信息，请参阅[Hyper-v 可扩展交换机转发上下文](hyper-v-extensible-switch-forwarding-context.md)。

可扩展交换机扩展调用[*GetNetBufferListDestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_get_net_buffer_list_destinations)函数，以获取指向[**NDIS\_交换机的指针\_转发\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)数据包的\_网络中\_数组结构[**缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构。 单个[**ndis\_交换机\_端口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_port_destination)在此结构内\_目标元素可[ **\_** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-switch-port-destination-at-array-index)通过以下方式进行访问：\_\_\_\_宏定义.

为了提高性能，转发扩展可以调用[*GrowNetBufferListDestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_grow_net_buffer_list_destinations)函数，而不是[*GetNetBufferListDestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_get_net_buffer_list_destinations) ，以获取指向[**NDIS\_交换机\_转发的指针\_目标\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)结构。 如果扩展确定它需要数据包的 OOB 数据中的目标端口的其他数组元素，则扩展将执行此项。 有关详细信息，请参阅[将可扩展交换机目标端口数据添加到数据包](adding-extensible-switch-destination-port-data-to-a-packet.md)。

**请注意**  仅从可扩展交换机传出数据路径获取的数据包将包含目标端口信息。 有关详细信息，请参阅[Hyper-v 可扩展交换机数据路径](hyper-v-extensible-switch-data-path.md)。

 

 

 






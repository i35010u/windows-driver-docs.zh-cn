---
title: 查询数据包的可扩展交换机目标端口数据
description: 查询数据包的可扩展交换机目标端口数据
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60588fa6650ee4e9e2e5402d1f1c9e51523bb39d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793405"
---
# <a name="querying-a-packets-extensible-switch-destination-port-data"></a>查询数据包的可扩展交换机目标端口数据


每个 Hyper-v 可扩展交换机目标端口都是在 [**ndis \_ 交换机 \_ 转发 \_ 目标 \_ 数组**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)结构内由 [**ndis \_ 交换机 \_ 端口 \_ 目标**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_port_destination)元素指定的。 此数组包含在数据包的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构的带外 (OOB) 转发上下文中。 有关此上下文的详细信息，请参阅 [Hyper-v 可扩展交换机转发上下文](hyper-v-extensible-switch-forwarding-context.md)。

可扩展交换机扩展调用 [*GetNetBufferListDestinations*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_get_net_buffer_list_destinations)函数，以获取一个指针，该指针指向包的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构内的 [**NDIS \_ 交换机 \_ 转发 \_ 目标 \_ 数组**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)结构。 可以通过使用 [**\_ \_ \_ \_ \_ 数组 \_ 索引宏中的 ndis 交换机端口目标**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndis_switch_port_destination_at_array_index)来访问此结构内的各个 [**NDIS \_ 交换机 \_ 端口 \_ 目标**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_port_destination)元素。

为了提高性能，转发扩展可以调用 [*GrowNetBufferListDestinations*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_grow_net_buffer_list_destinations) 函数而不是 [*GetNetBufferListDestinations*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_get_net_buffer_list_destinations) 来获取指向 [**NDIS \_ 交换机 \_ 转发 \_ 目标 \_ 数组**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_destination_array) 结构的指针。 如果扩展确定它需要数据包的 OOB 数据中的目标端口的其他数组元素，则扩展将执行此项。 有关详细信息，请参阅 [将可扩展交换机目标端口数据添加到数据包](adding-extensible-switch-destination-port-data-to-a-packet.md)。

**注意**  只有从可扩展交换机传出数据路径获取的数据包才会包含目标端口信息。 有关详细信息，请参阅 [Hyper-v 可扩展交换机数据路径](hyper-v-extensible-switch-data-path.md)。

 

 


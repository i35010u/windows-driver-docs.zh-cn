---
title: Hyper-V 可扩展交换机转发上下文数据类型
description: Hyper-V 可扩展交换机转发上下文数据类型
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 523484d4396fd7116e2f5db4b1b0ab171dd9b8b6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817129"
---
# <a name="hyper-v-extensible-switch-forwarding-context-data-types"></a>Hyper-V 可扩展交换机转发上下文数据类型


遍历 Hyper-v 可扩展交换机数据路径的每个数据包的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构包含带外 (OOB) 数据。 此数据指定从其发起数据包的源端口，以及用于数据包传递的一个或多个目标端口。 此 OOB 数据称为 *可扩展交换机转发上下文*。

以下数据类型已声明为访问数据包的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构内的可扩展交换机转发上下文：

<a href="" id="ndis-switch-forwarding-detail-net-buffer-list-info"></a>[**NDIS \_ 交换机 \_ 转发 \_ 详细信息 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_detail_net_buffer_list_info)  
这是一个包含数据包转发特性的64位联合。 此数据包括源端口的标识符，以及从中产生数据包的网络适配器连接的标识符。 此数据还包括目标端口数组中可用的未使用的元素的数目。

可扩展交换机扩展可以通过使用 [**网络 \_ 缓冲区 \_ 列表 \_ 开关 \_ 转发 \_ 详细信息**](/windows-hardware/drivers/ddi/ndis/nf-ndis-net_buffer_list_switch_forwarding_detail) 宏来访问这些数据。

<a href="" id="ndis-switch-forwarding-destination-array"></a>[**NDIS \_ 交换机 \_ 转发 \_ 目标 \_ 阵列**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_detail_net_buffer_list_info)  
此结构定义包的目标端口数组。 此数组中的每个元素都被格式化为 [**NDIS \_ 交换机 \_ 端口 \_ 目标**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_port_destination) 结构。

[**NDIS \_ 交换机 \_ 转发 \_ 目标 \_ 数组**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_detail_net_buffer_list_info)结构包含指定元素总数和数组中使用的元素数的当前数目的成员。

可扩展交换机扩展可以通过调用 [*GetNetBufferListDestinations*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_get_net_buffer_list_destinations) 函数获取此数组。 如果驱动程序为具有多个目标端口的数据包添加或修改数组中的元素，则必须调用 [*UpdateNetBufferListDestinations*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_update_net_buffer_list_destinations) 函数。 此函数将这些更改提交到数据包转发上下文中的目标端口数组。

**注意**  若要将所做的更改提交到只有一个目标端口的数据包，驱动程序可以更高效地调用 [*AddNetBufferListDestination*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_add_net_buffer_list_destination) 函数。

 

<a href="" id="ndis-switch-port-destination"></a>[**NDIS \_ 交换机 \_ 端口 \_ 目标**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_port_destination)  
此结构定义数据包的目标端口。 对于具有单个目标端口的数据包，目标端口数组中只有一个 [**NDIS \_ 交换机 \_ 端口 \_ 目标**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_port_destination) 元素。 对于包含多个目标端口的数据包，数组中有一个或多个此类元素。

在可扩展交换机扩展已调用 [*GetNetBufferListDestinations*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_get_net_buffer_list_destinations) 以获取数据包的目标端口数组后，它可以通过使用 [**\_ \_ \_ \_ \_ 数组 \_ 索引宏处的 NDIS 交换机端口目标**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndis_switch_port_destination_at_array_index) 来访问数组中的单个元素。

 


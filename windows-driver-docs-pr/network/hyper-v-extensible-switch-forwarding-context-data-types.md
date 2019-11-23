---
title: Hyper-V 可扩展交换机转发上下文数据类型
description: Hyper-V 可扩展交换机转发上下文数据类型
ms.assetid: B5377411-C6F0-47BE-BD45-534AC784ED76
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 374b18d95f001592b01b9a74f98aa686334a98bd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823910"
---
# <a name="hyper-v-extensible-switch-forwarding-context-data-types"></a>Hyper-V 可扩展交换机转发上下文数据类型


遍历 Hyper-v 可扩展交换机数据路径的每个数据包的[**NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构包含带外（OOB）数据。 此数据指定从其发起数据包的源端口，以及用于数据包传递的一个或多个目标端口。 此 OOB 数据称为*可扩展交换机转发上下文*。

以下数据类型已声明为访问数据包的[**网络\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)内的可扩展交换机转发上下文\_列表结构：

<a href="" id="ndis-switch-forwarding-detail-net-buffer-list-info"></a>[**NDIS\_交换机\_转发\_详细信息\_NET\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_detail_net_buffer_list_info)  
这是一个包含数据包转发特性的64位联合。 此数据包括源端口的标识符，以及从中产生数据包的网络适配器连接的标识符。 此数据还包括目标端口数组中可用的未使用的元素的数目。

可扩展交换机扩展可以使用[**NET\_BUFFER\_LIST\_开关\_转发\_详细信息**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-switch-forwarding-detail)宏来访问这些数据。

<a href="" id="ndis-switch-forwarding-destination-array"></a>[**NDIS\_交换机\_转发\_目标\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_detail_net_buffer_list_info)  
此结构定义包的目标端口数组。 此数组中的每个元素都被格式化为[**NDIS\_交换机\_端口\_目标**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_port_destination)结构。

[**NDIS\_交换机\_转发\_目标\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_detail_net_buffer_list_info)结构包含指定元素总数和数组中使用的元素的数目的成员。

可扩展交换机扩展可以通过调用[*GetNetBufferListDestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_get_net_buffer_list_destinations)函数获取此数组。 如果驱动程序为具有多个目标端口的数据包添加或修改数组中的元素，则必须调用[*UpdateNetBufferListDestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_update_net_buffer_list_destinations)函数。 此函数将这些更改提交到数据包转发上下文中的目标端口数组。

**请注意**  仅将更改提交到只有一个目标端口的数据包，驱动程序也更有效地调用[*AddNetBufferListDestination*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_add_net_buffer_list_destination)函数。

 

<a href="" id="ndis-switch-port-destination"></a>[**NDIS\_交换机\_端口\_目标**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_port_destination)  
此结构定义数据包的目标端口。 对于具有单个目标端口的数据包，目标端口数组中只有一个[**NDIS\_交换机\_端口\_目标**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_port_destination)元素。 对于包含多个目标端口的数据包，数组中有一个或多个此类元素。

在可扩展交换机扩展已调用[*GetNetBufferListDestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_get_net_buffer_list_destinations)以获取数据包的目标端口数组后，可以使用[**NDIS\_交换机\_端口\_目标\_\_array\_INDEX**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-switch-port-destination-at-array-index)宏来访问数组中的单个元素。

 

 






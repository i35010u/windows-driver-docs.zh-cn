---
title: Hyper-V 可扩展交换机发送和接收标志
description: Hyper-V 可扩展交换机发送和接收标志
ms.assetid: FBA506EC-4E9F-4964-9C9C-FF4910DDA908
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3dd16d47af8e8a2ae83c1408df9b780a9c3a0bf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823827"
---
# <a name="hyper-v-extensible-switch-send-and-receive-flags"></a>Hyper-V 可扩展交换机发送和接收标志


**请注意**  本页假设你熟悉[hyper-v 可扩展交换机](overview-of-the-hyper-v-extensible-switch.md)和[混合转发](hybrid-forwarding.md)概述中的信息和关系图。

 

通过 Hyper-v 可扩展交换机数据路径移动的数据包流量由扩展通过以下方式获取：

-   调用[*FilterSendNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_send_net_buffer_lists)函数时，扩展会从入口数据路径获取数据包。 该扩展通过调用[**NdisFSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlists)将数据包转发到入口数据路径上的基础扩展。 筛选和转发扩展还可以通过调用[**NdisFSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlistscomplete)从入口数据路径中删除数据包。

-   调用[*FilterReceiveNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_receive_net_buffer_lists)函数时，扩展会从出口数据路径获取数据包。 该扩展通过调用[**NdisFIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatereceivenetbufferlists)将数据包转发到传出数据路径上的过量扩展。 筛选和转发扩展还可以通过调用[**NdisFReturnNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreturnnetbufferlists)从出口数据路径中删除数据包。

可以在[*FilterSendNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_send_net_buffer_lists)或[**NdisFSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlists)的*SendFlags*参数中设置以下标志：

<a href="" id="ndis-send-flags-switch-single-source"></a>**NDIS\_将\_标志\_开关\_单个\_源**  
如果设置此标志， [**NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)的链接列表中的所有数据包\_列表结构源自相同的 hyper-v 可扩展交换机源端口。

当 NDIS 调用[*FilterSendNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_send_net_buffer_lists)时，如果可扩展交换机可扩展接口已将来自同一源端口的多个数据包分组，则会设置此标志。 为了获得最佳性能，扩展应保留这一分组，并在调用[**NdisFSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlists)时设置此标志。 如果扩展使用与列表中其他数据包相同的源端口，则扩展还可以将任何来源或克隆的数据包添加到[**网络\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)的链接列表中\_列表结构。

**请注意**，  如果[**网络\_\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)的链接列表中的每个数据包都使用相同的源端口，则扩展应将**NDIS\_发送\_\_\_\_标志**完成发送请求时， [**NdisFSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlistscomplete)的*SENDCOMPLETEFLAGS*参数中的单个\_源标志。

 

<a href="" id="ndis-send-flags-switch-destination-group"></a>**NDIS\_\_\_目标\_组发送\_标志**  
如果设置此标志，则会将[**网络\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构的链接列表中的所有数据包转发到相同的可扩展交换机目标端口。

在确定每个数据包的目标端口后，转发扩展可将此标志用于[**网络\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构的链接列表。 在将数据包转发到传出数据路径之前，将使用可扩展交换机的基础微型端口边缘来使用和删除此标志。

捕获和筛选扩展不能使用此标志。

**请注意**  转发扩展仅确定数据包的目标端口用于 NVGRE 数据包。 如果数据包为 NVGRE 数据包，Hyper-v 网络虚拟化（HNV）组件会确定数据包的目标端口并转发数据包。 有关详细信息，请参阅[混合转发](hybrid-forwarding.md)。

 

为了获得最佳性能，如果链接列表中的所有数据包都将转发到同一目标端口，则转发扩展应该设置此标志。 通过设置此标志，扩展将确认链接列表中的所有数据包在可扩展交换机转发上下文中具有相同的目标端口元素。

**请注意**  转发扩展不得为具有多个目标端口的数据包的链接列表设置此标志。

 

可以在[*FilterReceiveNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_receive_net_buffer_lists)或[**NdisFIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatereceivenetbufferlists)的*ReceiveFlags*参数中设置以下标志：

<a href="" id="ndis-receive-flags-switch-single-source"></a>**NDIS\_接收\_标志\_开关\_单个\_源**  
如果设置此标志， [**NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)的链接列表中的所有数据包\_列表结构源自相同的 hyper-v 可扩展交换机源端口。

当 NDIS 调用[*FilterReceiveNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_receive_net_buffer_lists)时，如果可扩展交换机已将来自同一源端口的多个数据包分组，则会设置此标志。 为了获得最佳性能，扩展应保留这一分组，并在调用[**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)时设置此标志。 如果数据包与列表中的其他数据包具有相同的源端口，还应将任何来源或克隆的数据包添加到[**网络\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)的链接列表中\_列表结构。

**请注意**，  如果[**网络\_\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)的链接列表中的每个数据包都使用相同的源端口，则扩展应将**NDIS\_返回\_\_\_\_标志**接收请求完成时， [*FilterReturnNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_return_net_buffer_lists)的*RETURNFLAGS*参数中的源标志。 如果扩展插件调用[**NdisFReturnNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreturnnetbufferlists)来返回它未发起或克隆的数据包，则必须在*ReturnFlags*参数中设置此标志。

 

<a href="" id="ndis-receive-flags-switch-destination-group"></a>**NDIS\_接收\_标志\_\_目标\_组**  
如果设置此标志，则会将[**网络\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构的链接列表中的所有数据包转发到相同的可扩展交换机目标端口。

当 NDIS 调用[*FilterReceiveNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_receive_net_buffer_lists)时，如果可扩展交换机已将具有相同目标端口的多个数据包分组，则会设置此标志。 为了获得最佳性能，扩展应保留这一分组，并在调用[**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)时设置此标志。 如果数据包与列表中的其他数据包具有相同的目标端口，还应将任何来源或克隆的数据包添加到[**网络\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)的链接列表中\_列表结构。

**请注意**  扩展调用[**NdisFIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatereceivenetbufferlists)时，它不能在*ReceiveFlags*参数中设置**NDIS\_接收\_标志\_资源**标志。 可扩展交换机接口忽略此标志，并将通过调用[*FilterReturnNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_return_net_buffer_lists)来完成接收指示。

 

 

 






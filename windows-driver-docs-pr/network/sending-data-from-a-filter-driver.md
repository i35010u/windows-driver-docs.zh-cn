---
title: 从筛选器驱动程序发送数据
description: 从筛选器驱动程序发送数据
ms.assetid: 09189010-d12c-43d6-ac9b-8fc7424edfd5
keywords:
- 发送数据 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b0ccd217f5c26cd82b4a31e5d9bc8980696b6af
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841981"
---
# <a name="sending-data-from-a-filter-driver"></a>从筛选器驱动程序发送数据





筛选器驱动程序可以启动过量驱动程序启动的发送请求或筛选发送请求。 当协议驱动程序调用[**NdisSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissendnetbufferlists)函数时，NDIS 会将指定的[**NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构提交给驱动程序堆栈中的最顶层筛选器模块。

### <a name="send-requests-initiated-by-a-filter-driver"></a>发送由筛选器驱动程序启动的请求

下图说明了由筛选器驱动程序启动的发送操作。

![说明筛选器驱动程序启动的发送操作的关系图](images/filtersend.png)

筛选器驱动程序调用[**NdisFSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlists)函数，以将网络\_缓冲区列表中定义的网络数据发送[ **\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构。

筛选器驱动程序必须将其创建的每个 NET\_缓冲区\_列表结构的**SourceHandle**成员设置为传递给**NdisFSendNetBufferLists**的*NdisFilterHandle*参数的值。 NDIS 驱动程序不应为驱动程序未起源\_列表结构的 NET\_缓冲区修改**SourceHandle**成员。

在调用**NdisFSendNetBufferLists**之前，筛选器驱动程序可以使用[**NET\_缓冲区\_列表\_信息**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-info)宏设置发送请求附带的信息。 底层驱动程序可以通过 NET\_缓冲区\_列表\_信息宏检索此信息。

一旦筛选器驱动程序调用**NdisFSendNetBufferLists**，它就让给了 NET\_缓冲区的所有权\_列表结构和所有关联的资源。 NDIS 可处理发送请求，或将请求传递到底层驱动程序。

NDIS 调用[*FilterSendNetBufferListsComplete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_send_net_buffer_lists_complete)函数将结构和数据返回到筛选器驱动程序。 在将列表传递到*FilterSendNetBufferListsComplete*之前，NDIS 可以将多个发送请求中的结构和数据收集到网络\_缓冲区的单个链接列表中\_列表结构。

在 NDIS 调用*FilterSendNetBufferListsComplete*之前，发送请求的当前状态是未知的。 在 NDIS 将结构返回到*FilterSendNetBufferListsComplete*之前，筛选器驱动程序*不*应尝试检查[**NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构或任何关联的数据。

*FilterSendNetBufferListsComplete*执行完成发送操作所需的任何后处理操作。

当 NDIS 调用*FilterSendNetBufferListsComplete*时，筛选器驱动程序会重新获得*NetBufferLists*参数指定的与 NET\_缓冲区关联的所有资源的所有权\_列表结构。 *FilterSendNetBufferListsComplete*可以释放这些资源（例如，通过调用[**NdisFreeNetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreenetbuffer)和[**NdisFreeNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreenetbufferlist)函数），或准备它们以便在后续调用**中重用NdisFSendNetBufferLists**。

NDIS 始终将筛选器提供的网络数据提交到由筛选器驱动程序确定的顺序，传递给**NdisFSendNetBufferLists**。 但是，在按指定顺序发送数据后，基础驱动程序可以按任意顺序返回缓冲区。

筛选器驱动程序可以为其源自的发送请求请求环回。 为请求环回，驱动程序将 NDIS\_发送\_标志\_\_检查在[**NdisFSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlists)的*SendFlags*参数中\_环回标志。 NDIS 指示收到的包含发送数据的数据包。

**请注意**  筛选器驱动程序应跟踪它所源自的发送请求，并确保在完成此类请求后，它不会调用[**NdisFSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlistscomplete)函数。

 

### <a name="filtering-send-requests"></a>筛选发送请求

下图说明了筛选过量驱动程序启动的发送请求。

![说明筛选由过量驱动程序启动的发送请求的关系图](images/sendfilter.png)

NDIS 调用筛选器驱动程序的[*FilterSendNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_send_net_buffer_lists)函数来筛选过量驱动程序的发送请求。

筛选器驱动程序不能修改 NET\_缓冲区中的**SourceHandle**成员，\_从其他驱动程序接收的列表结构。

筛选器驱动程序可以筛选数据，并将筛选后的数据发送到底层驱动程序。 对于每个提交到*FilterSendNetBufferLists*的网络\_缓冲区结构，筛选器驱动程序可以执行以下操作：

-   通过调用[**NdisFSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlists)函数将缓冲区传递到下一个基础驱动程序。 对于筛选器驱动程序，NDIS 保证上下文空间的可用性（请参阅[NET\_BUFFER\_列表\_上下文结构](net-buffer-list-context-structure.md)）。 筛选器驱动程序可以在调用**NdisFSendNetBufferLists**之前修改缓冲区内容。 筛选后的数据的处理过程与筛选器驱动程序启动的发送操作一样。

-   通过调用[**NdisFSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlistscomplete)函数删除该缓冲区。

-   在本地数据结构中对缓冲区排队，以便以后进行处理。 筛选器驱动程序的设计决定了导致驱动程序处理排队缓冲区的原因。 一些示例包括在收到特定缓冲区后超时或处理后的处理。

    **请注意**  如果驱动程序将发送请求以便以后处理，则它必须支持发送取消请求。 有关发送取消请求的详细信息，请参阅[在筛选器驱动程序中取消发送请求](canceling-a-send-request-in-a-filter-driver.md)。

     

-   复制缓冲区并使用副本发出发送请求。 发送操作类似于筛选器驱动程序启动的发送请求。 在这种情况下，驱动程序必须通过调用[**NdisFSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlistscomplete)函数将原始缓冲区返回到过量驱动程序。

完成发送请求后，将会继续驱动程序堆栈。 当微型端口驱动程序调用[**NdisMSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete)函数时，NDIS 将为底层筛选器模块调用[*FilterSendNetBufferListsComplete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_send_net_buffer_lists_complete)函数。

在发送操作完成后，筛选器驱动程序会反转筛选器驱动程序在*FilterSendNetBufferLists*中进行的对过量驱动程序缓冲区描述符的修改。 驱动程序调用[**NdisFSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlistscomplete)函数以将网络\_缓冲区\_列表结构的链接列表返回到过量驱动程序，并返回发送请求的最终状态。

当最顶层的筛选器模块调用**NdisFSendNetBufferListsComplete**时，NDIS 将调用发起方协议驱动程序的[**ProtocolSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_send_net_buffer_lists_complete)函数。

不提供*FilterSendNetBufferLists*函数的筛选器驱动程序仍可以启动发送请求。 如果此类驱动程序启动发送请求，则必须提供*FilterSendNetBufferListsComplete*函数，并且它不能在驱动程序堆栈上传递完整事件。

筛选器驱动程序可以通过或筛选过量驱动程序的环回请求。 若要在环回请求上传递，请在*FilterSendNetBufferLists*的*SendFlags*参数中，如果 NDIS set NDIS\_发送\_标志\_检查\_环回的\_\_标志\_在调用**NdisFSendNetBufferLists**时，在*SENDFLAGS*参数中检查\_环回的\_。 NDIS 指示收到的包含发送数据的数据包。

通常，如果筛选器驱动程序以不能提供标准服务的方式（如环回）修改任何行为，则筛选器驱动程序必须为 NDIS 提供该服务。 例如，修改硬件地址请求的筛选器驱动程序（请参阅[OID\_802\_3\_当前\_地址](https://docs.microsoft.com/windows-hardware/drivers/network/oid-802-3-current-address)）应处理定向到新硬件地址的缓冲区环回。 在这种情况下，NDIS 无法提供它通常提供的环回服务，因为筛选器已更改地址。 此外，如果筛选器驱动程序设置了混杂模式（请参阅[OID\_GEN\_当前\_数据包\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-current-packet-filter)），则不应将其收到的额外数据传递给过量驱动程序。

 

 






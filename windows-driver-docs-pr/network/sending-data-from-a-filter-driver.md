---
title: 从筛选器驱动程序发送数据
description: 从筛选器驱动程序发送数据
ms.assetid: 09189010-d12c-43d6-ac9b-8fc7424edfd5
keywords:
- 发送数据 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8dcff2888b0deafcfc64aeedaba860391db93502
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211591"
---
# <a name="sending-data-from-a-filter-driver"></a>从筛选器驱动程序发送数据





筛选器驱动程序可以启动过量驱动程序启动的发送请求或筛选发送请求。 当协议驱动程序调用 [**NdisSendNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissendnetbufferlists) 函数时，NDIS 会将指定的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构提交给驱动程序堆栈中的最顶层筛选器模块。

### <a name="send-requests-initiated-by-a-filter-driver"></a>发送由筛选器驱动程序启动的请求

下图说明了由筛选器驱动程序启动的发送操作。

![说明筛选器驱动程序启动的发送操作的关系图](images/filtersend.png)

筛选器驱动程序调用 [**NdisFSendNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlists) 函数来发送网络 [** \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构列表中定义的网络数据。

筛选器驱动程序必须将其创建的每个网络缓冲区列表结构的**SourceHandle**成员设置 \_ \_ 为传递给**NdisFSendNetBufferLists**的*NdisFilterHandle*参数的相同值。 NDIS 驱动程序不应为**SourceHandle** \_ 驱动程序未起源的网络缓冲区列表结构修改 SourceHandle 成员 \_ 。

在调用 **NdisFSendNetBufferLists**之前，筛选器驱动程序可以使用 [**NET \_ BUFFER \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/ndis/nf-ndis-net_buffer_list_info) 宏设置发送请求附带的信息。 底层驱动程序可以通过 NET \_ BUFFER \_ 列表信息宏检索此信息 \_ 。

一旦筛选器驱动程序调用 **NdisFSendNetBufferLists**，它就会让给网络 \_ 缓冲区 \_ 列表结构和所有关联资源的所有权。 NDIS 可处理发送请求，或将请求传递到底层驱动程序。

NDIS 调用 [*FilterSendNetBufferListsComplete*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_send_net_buffer_lists_complete) 函数将结构和数据返回到筛选器驱动程序。 在将 \_ \_ 列表传递到*FILTERSENDNETBUFFERLISTSCOMPLETE*之前，NDIS 可以将多个发送请求中的结构和数据收集到一个链接的网络缓冲区列表结构列表中

在 NDIS 调用 *FilterSendNetBufferListsComplete*之前，发送请求的当前状态是未知的。 在 NDIS 将结构返回到*FilterSendNetBufferListsComplete*之前，筛选器驱动程序*不*应尝试检查[**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构或任何关联的数据。

*FilterSendNetBufferListsComplete* 执行完成发送操作所需的任何后处理操作。

当 NDIS 调用 *FilterSendNetBufferListsComplete*时，筛选器驱动程序会重新获得与 \_ \_ *NetBufferLists* 参数指定的网络缓冲区列表结构关联的所有资源的所有权。 *FilterSendNetBufferListsComplete* 可以释放这些资源 (例如，通过调用 [**NdisFreeNetBuffer**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreenetbuffer) 和 [**NdisFreeNetBufferList**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreenetbufferlist) 函数) 或准备它们以便在对 **NdisFSendNetBufferLists**的后续调用中重复使用。

NDIS 始终将筛选器提供的网络数据提交到由筛选器驱动程序确定的顺序，传递给 **NdisFSendNetBufferLists**。 但是，在按指定顺序发送数据后，基础驱动程序可以按任意顺序返回缓冲区。

筛选器驱动程序可以为其源自的发送请求请求环回。 为请求环回，驱动程序会 \_ \_ \_ \_ \_ 在[**NdisFSendNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlists)的*SendFlags*参数中设置 "NDIS 发送标志检查" 标记。 NDIS 指示收到的包含发送数据的数据包。

**注意**   筛选器驱动程序应跟踪它所源自的发送请求，并确保在完成此类请求后，它不会调用[**NdisFSendNetBufferListsComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlistscomplete)函数。

 

### <a name="filtering-send-requests"></a>筛选发送请求

下图说明了筛选过量驱动程序启动的发送请求。

![说明筛选由过量驱动程序启动的发送请求的关系图](images/sendfilter.png)

NDIS 调用筛选器驱动程序的 [*FilterSendNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_send_net_buffer_lists) 函数来筛选过量驱动程序的发送请求。

筛选器驱动程序不能修改**SourceHandle** \_ \_ 其从其他驱动程序接收的网络缓冲区列表结构中的 SourceHandle 成员。

筛选器驱动程序可以筛选数据，并将筛选后的数据发送到底层驱动程序。 对于每个 \_ 提交到 *FILTERSENDNETBUFFERLISTS*的网络缓冲区结构，筛选器驱动程序可以执行以下操作：

-   通过调用 [**NdisFSendNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlists) 函数将缓冲区传递到下一个基础驱动程序。 NDIS 保证上下文空间的可用性 (参阅) 用于筛选器驱动程序的 [网络 \_ 缓冲区 \_ 列表 \_ 上下文结构](net-buffer-list-context-structure.md) 。 筛选器驱动程序可以在调用 **NdisFSendNetBufferLists**之前修改缓冲区内容。 筛选后的数据的处理过程与筛选器驱动程序启动的发送操作一样。

-   通过调用 [**NdisFSendNetBufferListsComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlistscomplete) 函数删除该缓冲区。

-   在本地数据结构中对缓冲区排队，以便以后进行处理。 筛选器驱动程序的设计决定了导致驱动程序处理排队缓冲区的原因。 一些示例包括在收到特定缓冲区后超时或处理后的处理。

    **注意**   如果驱动程序将发送请求以便以后处理，则它必须支持发送取消请求。 有关发送取消请求的详细信息，请参阅 [在筛选器驱动程序中取消发送请求](canceling-a-send-request-in-a-filter-driver.md)。

     

-   复制缓冲区并使用副本发出发送请求。 发送操作类似于筛选器驱动程序启动的发送请求。 在这种情况下，驱动程序必须通过调用 [**NdisFSendNetBufferListsComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlistscomplete) 函数将原始缓冲区返回到过量驱动程序。

完成发送请求后，将会继续驱动程序堆栈。 当微型端口驱动程序调用 [**NdisMSendNetBufferListsComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete) 函数时，NDIS 将为底层筛选器模块调用 [*FilterSendNetBufferListsComplete*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_send_net_buffer_lists_complete) 函数。

在发送操作完成后，筛选器驱动程序会反转筛选器驱动程序在 *FilterSendNetBufferLists*中进行的对过量驱动程序缓冲区描述符的修改。 驱动程序调用 [**NdisFSendNetBufferListsComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlistscomplete) 函数以将网络缓冲区列表结构的链接列表返回 \_ \_ 到过量驱动程序，并返回发送请求的最终状态。

当最顶层的筛选器模块调用 **NdisFSendNetBufferListsComplete**时，NDIS 将调用发起方协议驱动程序的 [**ProtocolSendNetBufferListsComplete**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_send_net_buffer_lists_complete) 函数。

不提供 *FilterSendNetBufferLists* 函数的筛选器驱动程序仍可以启动发送请求。 如果此类驱动程序启动发送请求，则必须提供 *FilterSendNetBufferListsComplete* 函数，并且它不能在驱动程序堆栈上传递完整事件。

筛选器驱动程序可以通过或筛选过量驱动程序的环回请求。 若要在环回请求上传递，在 \_ \_ \_ FilterSendNetBufferLists 的 SendFlags 参数中，如果 ndis 为回送设置了 ndis 发送标志检查 \_ \_ ，筛选器驱动程序会在*SendFlags* *FilterSendNetBufferLists* \_ \_ \_ \_ \_ 调用**NdisFSendNetBufferLists**时为*SendFlags*参数中的环回设置 ndis 发送标志检查。 NDIS 指示收到的包含发送数据的数据包。

通常，如果筛选器驱动程序以这种方式修改任何行为，而 NDIS 无法提供标准服务 (如环回) ，则筛选器驱动程序必须为 NDIS 提供该服务。 例如，修改硬件地址请求的筛选器驱动程序 (参阅 [OID \_ 802 \_ 3 \_ 当前 \_ 地址](./oid-802-3-current-address.md)) ，应处理定向到新硬件地址的缓冲区环回。 在这种情况下，NDIS 无法提供它通常提供的环回服务，因为筛选器已更改地址。 此外，如果筛选器驱动程序设置了混杂模式 (参阅 [OID \_ GEN \_ 当前 \_ 数据包 \_ 筛选器](./oid-gen-current-packet-filter.md)) ，则不应将其收到的额外数据传递给过量驱动程序。

 


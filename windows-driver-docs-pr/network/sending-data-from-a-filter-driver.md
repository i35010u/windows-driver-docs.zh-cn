---
title: 从筛选器驱动程序发送数据
description: 从筛选器驱动程序发送数据
ms.assetid: 09189010-d12c-43d6-ac9b-8fc7424edfd5
keywords:
- 发送数据 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53839037e8eaa23bfbef3e64d3368ba8770c6a46
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383646"
---
# <a name="sending-data-from-a-filter-driver"></a>从筛选器驱动程序发送数据





筛选器驱动程序可以启动的发送请求或筛选基础驱动程序启动的发送请求。 当协议驱动程序调用[ **NdisSendNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissendnetbufferlists)函数，NDIS 提交指定[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)驱动程序堆栈中的最顶层的筛选器模块的结构。

### <a name="send-requests-initiated-by-a-filter-driver"></a>发送请求由筛选器驱动程序启动

下图说明了由筛选器驱动程序启动的发送操作。

![说明由筛选器驱动程序启动的发送操作的关系图](images/filtersend.png)

筛选驱动程序调用[ **NdisFSendNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfsendnetbufferlists)函数来发送的列表中定义的网络数据[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构。

必须设置筛选器驱动程序**SourceHandle**的每个 NET 成员\_缓冲区\_为相同的值，它将传递给它创建的列表结构*NdisFilterHandle*参数**NdisFSendNetBufferLists**。 NDIS 驱动程序不应修改**SourceHandle** NET 成员\_缓冲区\_的驱动程序不是列表结构。

然后再调用**NdisFSendNetBufferLists**，筛选器驱动程序可以设置发送请求，附带的信息[ **NET\_缓冲区\_列表\_信息** ](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-info)宏。 基础驱动程序可以检索此信息与 NET\_缓冲区\_列表\_信息宏。

只要筛选器驱动程序调用**NdisFSendNetBufferLists**，它将放弃所有权的 NET\_缓冲区\_列表结构和所有关联的资源。 NDIS 可以处理发送请求，或将请求传递给基础驱动程序。

NDIS 调用[ *FilterSendNetBufferListsComplete* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_send_net_buffer_lists_complete)函数以返回到筛选器驱动程序的结构和数据。 NDIS 可以收集结构和数据从多个将请求发送到一个链接列表的 NET\_缓冲区\_列表结构传递到列表之前*FilterSendNetBufferListsComplete*

NDIS 调用直到*FilterSendNetBufferListsComplete*，发送请求的当前状态为未知。 筛选器驱动程序应*永远不会*尝试检查[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构或任何关联的数据之前 NDIS 返回为结构*FilterSendNetBufferListsComplete*。

*FilterSendNetBufferListsComplete*执行任何后续处理是完成发送操作所必需。

当调用 NDIS *FilterSendNetBufferListsComplete*，筛选器驱动程序重新获得与网络相关联的所有资源的所有权\_缓冲区\_所指定的列表结构*NetBufferLists*参数。 *FilterSendNetBufferListsComplete*可以是释放这些资源 (例如，通过调用[ **NdisFreeNetBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreenetbuffer)并[ **NdisFreeNetBufferList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreenetbufferlist)函数) 或让其可供在后续调用中重用**NdisFSendNetBufferLists**。

NDIS 始终提交中的筛选器驱动程序确定的顺序的底层驱动程序筛选器提供网络数据传递给**NdisFSendNetBufferLists**。 但是之后将数据发送指定的顺序，, 基础驱动程序可以返回缓冲区按任何顺序。

筛选器驱动程序可以请求将请求发送其环回发起。 若要请求环回，驱动程序设置 NDIS\_发送\_标志\_检查\_有关\_中的环回标志*SendFlags*参数[ **NdisFSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfsendnetbufferlists)。 NDIS 指示接收的数据包包含发送数据。

**请注意**  筛选器驱动程序应跟踪的源自的发送请求并确保它不会调用[ **NdisFSendNetBufferListsComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfsendnetbufferlistscomplete)函数时此类请求已完成。

 

### <a name="filtering-send-requests"></a>筛选发送请求

下图说明了筛选由基础驱动程序启动的发送请求。

![说明筛选由基础驱动程序启动的发送请求的关系图](images/sendfilter.png)

NDIS 筛选器驱动程序将调用[ *FilterSendNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_send_net_buffer_lists)函数来筛选基础驱动程序在发送请求。

筛选器驱动程序不能修改**SourceHandle**成员在 NET\_缓冲区\_它接收来自其他驱动程序的列表结构。

筛选器驱动程序可以对数据进行筛选，并将筛选后的数据发送到基础驱动程序。 于每个网络\_提交到的缓冲区结构*FilterSendNetBufferLists*，筛选器驱动程序可以执行以下操作：

-   通过调用传递到下一步基础驱动程序缓冲区[ **NdisFSendNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfsendnetbufferlists)函数。 NDIS 保证上下文空间的可用性 (请参阅[NET\_缓冲区\_列表\_上下文结构](net-buffer-list-context-structure.md)) 的筛选器驱动程序。 筛选器驱动程序可以修改缓冲区内容之前调用**NdisFSendNetBufferLists**。 已筛选数据的处理将继续与由筛选器驱动程序启动的发送操作一样。

-   通过调用删除缓冲区[ **NdisFSendNetBufferListsComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfsendnetbufferlistscomplete)函数。

-   排入队列供以后处理的本地数据结构中的缓冲区。 筛选器驱动程序的设计决定了哪些因素会导致驱动程序处理排队的缓冲区。 一些示例包括处理后超时或后接收到特定的缓冲区进行处理。

    **请注意**  如果驱动程序队列发送供以后处理的请求，则它必须支持发送取消请求。 有关发送取消请求的详细信息，请参阅[筛选器驱动程序中取消发送请求](canceling-a-send-request-in-a-filter-driver.md)。

     

-   将缓冲区复制并且源自与复制的发送请求。 发送操作与类似的筛选器驱动程序启动的发送请求。 在这种情况下，该驱动程序必须返回原始缓冲区到基础驱动程序通过调用[ **NdisFSendNetBufferListsComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfsendnetbufferlistscomplete)函数。

在驱动程序堆栈中向上继续发送请求的完成。 当微型端口驱动程序调用[ **NdisMSendNetBufferListsComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsendnetbufferlistscomplete)函数、 NDIS 调用[ *FilterSendNetBufferListsComplete* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_send_net_buffer_lists_complete)最低过量的筛选器模块的函数。

筛选器驱动程序发送操作完成后，将对基础驱动程序的缓冲区描述符的筛选器驱动程序中所做的修改反转*FilterSendNetBufferLists*。 驱动程序调用[ **NdisFSendNetBufferListsComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfsendnetbufferlistscomplete)函数以返回链接的列表的 NET\_缓冲区\_列表结构到基础驱动程序，并返回在发送请求的最终状态。

当最顶部的筛选器模块调用**NdisFSendNetBufferListsComplete**，NDIS 调用原始协议驱动程序[ **ProtocolSendNetBufferListsComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_send_net_buffer_lists_complete)函数。

不提供的筛选器驱动程序*FilterSendNetBufferLists*函数仍可启动的发送请求。 如果这样的驱动程序启动的发送请求，则它必须提供*FilterSendNetBufferListsComplete*函数和它必须通过在驱动程序堆栈中向上完成事件。

筛选器驱动程序可以传递或筛选基础驱动程序的环回请求。 将传递在回送请求中，如果 NDIS 设置 NDIS\_发送\_标志\_检查\_有关\_中的环回*SendFlags*参数*FilterSendNetBufferLists*，筛选器驱动程序设置 NDIS\_发送\_标志\_检查\_有关\_中的环回*SendFlags*当它调用的参数**NdisFSendNetBufferLists**。 NDIS 指示接收的数据包包含发送数据。

一般情况下，如果筛选器驱动程序修改的方式 NDIS 不能提供标准服务 （例如环回） 的任何行为，筛选器驱动程序必须提供该服务用于 NDIS。 例如，修改硬件地址的请求的筛选器驱动程序才能 (请参阅[OID\_802\_3\_当前\_地址](https://docs.microsoft.com/windows-hardware/drivers/network/oid-802-3-current-address))，应处理的缓冲区定向到新的环回硬件地址。 在这种情况下，NDIS 无法提供它通常提供，因为筛选器更改地址环回服务。 此外，如果筛选器驱动程序集混杂模式 (请参阅[OID\_代\_当前\_数据包\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-current-packet-filter))，它应不传递它接收的额外数据到过量驱动程序。

 

 






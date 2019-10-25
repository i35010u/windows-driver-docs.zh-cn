---
title: VMQ 传输路径
description: VMQ 传输路径
ms.assetid: a34f0708-e477-4acc-b854-f00f752be423
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9f14901e5e93603019447c4afe9a08435cc07d5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842940"
---
# <a name="vmq-transmit-path"></a>VMQ 传输路径





对于传输请求，过量驱动程序使用[**NET\_缓冲区\_列表\_接收\_队列\_ID**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-receive-queue-id)宏，以将传出数据**中传出队列的队列标识符设置为NetBufferListFilteringInfo** OOB 信息。 **NetBufferListFilteringInfo**信息在[**NDIS\_NET\_缓冲器\_列表中指定\_筛选\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_net_buffer_list_filtering_info)结构。

NDIS 驱动程序可以使用[**net\_buffer\_list\_接收\_队列\_ID**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-receive-queue-id)宏来设置或获取[**NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构的队列标识符。 如果一个队列组包含多个 VM 队列，则可以将传输数据包的队列标识符设置为该组中任何 VM 队列的队列标识符。

协议驱动程序在[**NdisSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissendnetbufferlists)函数的*SendFlags*参数上将 NDIS\_发送\_标志\_单一\_队列位，以指示所有传输网络\_缓冲区\_列表调用中的结构用于同一传输队列。

微型端口驱动程序设置 NDIS\_在[**NdisMSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete)函数的*SendCompleteFlags*参数上\_SINGLE\_QUEUE 位发送\_完整\_标志，以指示所有网络\_调用中的缓冲区\_列表在同一传输队列中发送。

有关筛选器测试的详细信息，请参阅[VMQ 筛选器操作](vmq-filter-operations.md)。

**请注意**  在删除 VMQ 时（例如，在 VM 实时迁移期间），微型端口驱动程序可以接收包含无效**QUEUEID**值的 NBL。 如果发生这种情况，微型端口应忽略无效的队列 ID 并改用0（默认队列）。 **QueueId**是在 NBL 的 OOB 数据的**NetBufferListFilteringInfo**部分中找到的，使用[**NET\_BUFFER\_列表\_接收\_队列\_ID**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-receive-queue-id)宏来检索。

 

 

 






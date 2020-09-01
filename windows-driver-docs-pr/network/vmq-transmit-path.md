---
title: VMQ 传输路径
description: VMQ 传输路径
ms.assetid: a34f0708-e477-4acc-b854-f00f752be423
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a7364c928bcbba84743332c5496ccaf5fdf0b748
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216900"
---
# <a name="vmq-transmit-path"></a>VMQ 传输路径





对于传输请求，过量驱动程序使用 [**网络 \_ 缓冲区 \_ 列表 \_ 接收 \_ 队列 \_ ID**](/windows-hardware/drivers/ddi/ndis/nf-ndis-net_buffer_list_receive_queue_id) 宏，用 **NetBufferListFilteringInfo** OOB 信息设置传出数据中传出队列的队列标识符。 **NetBufferListFilteringInfo**信息是在[**NDIS \_ 网络 \_ 缓冲区 \_ 列表 \_ 筛选 \_ 信息**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_net_buffer_list_filtering_info)结构中指定的。

NDIS 驱动程序可以使用 [**网络 \_ 缓冲区 \_ 列表 \_ 接收 \_ 队列 \_ ID**](/windows-hardware/drivers/ddi/ndis/nf-ndis-net_buffer_list_receive_queue_id) 宏来设置或获取 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构的队列标识符。 如果一个队列组包含多个 VM 队列，则可以将传输数据包的队列标识符设置为该组中任何 VM 队列的队列标识符。

协议驱动程序在 \_ \_ \_ \_ [**NdisSendNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissendnetbufferlists)函数的*SendFlags*参数上设置 NDIS 发送标志单一队列位，以指示调用中的所有传输网络 \_ 缓冲区 \_ 列表结构都适用于同一传输队列。

微型端口驱动程序在 \_ \_ \_ \_ \_ [**NdisMSendNetBufferListsComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete)函数的*SendCompleteFlags*参数上将 NDIS 发送完成标志单一队列位设置为，以指示调用中的所有网络 \_ 缓冲区 \_ 列表都已在同一传输队列中发送。

有关筛选器测试的详细信息，请参阅 [VMQ 筛选器操作](vmq-filter-operations.md)。

**注意**   删除 VMQ 后 (例如，在 VM 实时迁移期间) ，微型端口驱动程序可以接收包含无效**QueueId**值的 NBL。 如果发生这种情况，微型端口应忽略无效的队列 ID 并使用 0 (默认队列) 。 **QueueId**在 NBL 的 OOB 数据的**NetBufferListFilteringInfo**部分中找到，并使用[**NET \_ BUFFER \_ LIST \_ RECEIVE \_ QUEUE \_ ID**](/windows-hardware/drivers/ddi/ndis/nf-ndis-net_buffer_list_receive_queue_id)宏检索。

 

 


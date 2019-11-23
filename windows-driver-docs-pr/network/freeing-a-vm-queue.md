---
title: 释放 VM 队列
description: 释放 VM 队列
ms.assetid: 32679638-eeef-4e11-bf56-c96f047e4de7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51584d5dcfc3cbd0dae85fd49f25ff83c4971e8f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842121"
---
# <a name="freeing-a-vm-queue"></a>释放 VM 队列





为了释放接收队列，过量驱动程序[会发出 OID\_接收\_FILTER\_可用\_队列](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-free-queue)集 OID 请求。 [**Ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**ndis\_接收\_队列的指针\_免费\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_free_parameters)结构，其队列标识符类型为**NDIS\_接收\_queue\_ID**。

[OID\_接收\_筛选器\_可用的\_队列](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-free-queue)释放接收队列，该队列由使用 OID 分配的过量驱动程序\_[接收\_筛选器\_分配\_队列](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-allocate-queue)OID。 有关分配接收队列的详细信息，请参阅[分配 VM 队列](allocating-a-vm-queue.md)。

**请注意**  默认队列（具有 NDIS 的队列标识符 **\_默认\_接收\_队列\_ID**）始终被分配且无法释放。

 

过量驱动程序必须释放它在队列上设置的所有筛选器，然后才能释放队列。 此外，在调用[**NdisCloseAdapterEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscloseadapterex)函数以关闭到网络适配器的绑定之前，过量驱动程序必须释放在网络适配器上分配的所有接收队列。 NDIS 在调用微型端口驱动程序的[*MiniportHaltEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)函数之前，释放在网络适配器上分配的所有队列。

当微型端口驱动程序收到释放队列的请求时，它将执行以下操作：

-   必须立即停止与队列关联的共享内存资源的 DMA。

-   生成指示 DMA 已停止的状态指示。

-   等待要返回的所有未完成的[**NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构与队列关联。

-   释放关联的共享内存和硬件资源。

当微型端口驱动程序收到[OID\_接收\_FILTER\_可用的\_队列](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-free-queue)集请求时，该队列必须进入 "停止 dma" 状态，它将停止队列上的 dma，而微型端口驱动程序必须通过使用[**NDIS\_状态\_"接收\_队列\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-receive-queue-state)状态指示" 来指示状态更改。 有关队列状态的详细信息，请参阅[队列状态和操作](queue-states-and-operations.md)。

小型端口驱动程序发出后， [**NDIS\_状态\_接收\_队列\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-receive-queue-state)状态指示，则它必须等待所有挂起的接收指示完成，然后才能释放关联的共享内存。 有关释放共享内存的详细信息，请参阅[共享内存资源分配](shared-memory-resource-allocation.md)。

 

 






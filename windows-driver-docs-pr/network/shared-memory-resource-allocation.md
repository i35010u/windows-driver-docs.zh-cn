---
title: 共享内存资源分配
description: 共享内存资源分配
ms.assetid: cf030a0f-1202-4d10-b9a1-58d031345678
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d3a77bbd9bfa88a1abaf9aba165bd6e1ac9725b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841923"
---
# <a name="shared-memory-resource-allocation"></a>共享内存资源分配





若要为 VM 队列分配共享内存资源，微型端口驱动程序将调用[**NdisAllocateSharedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatesharedmemory)函数。 例如，微型端口驱动程序在收到[OID\_接收\_筛选器时分配共享内存，\_队列\_分配\_完整](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-queue-allocation-complete)OID。 此外，小型端口驱动程序可以在网络适配器初始化期间为默认队列分配共享内存。 有关分配队列的详细信息，请参阅[分配 VM 队列](allocating-a-vm-queue.md)。

在释放队列之前，微型端口驱动程序可以为队列分配更多内存。 有关释放队列的详细信息，请参阅[释放 VM 队列](freeing-a-vm-queue.md)。

[**NDIS\_shared\_MEMORY\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_shared_memory_parameters)结构指定共享内存分配请求的共享内存参数。 微型端口驱动程序将此结构传递给[**NdisAllocateSharedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatesharedmemory)函数。 NDIS 将此结构传递给[**NetAllocateSharedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-allocate_shared_memory_handler)函数（即，分配\_共享\_内存\_处理程序入口点）。

当微型端口驱动程序分配共享内存时，它会指定以下内容：

-   队列标识符。

-   共享内存长度。

-   共享内存的使用方式。 例如，如果共享内存将用于接收缓冲区，则微型端口驱动程序将指定**NdisSharedMemoryUsageReceive** 。

如果在**Flags**成员中未设置 NDIS\_共享\_MEM\_参数\_CONTIGOUS 标志，则可以在非连续内存中包含的分散收集列表中指定共享内存。

[**NDIS\_共享\_内存\_使用情况**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ne-ndis-_ndis_shared_memory_usage)枚举指定共享内存的使用方式。 NDIS\_共享\_内存\_使用情况枚举是在[**ndis\_shared\_内存\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_shared_memory_parameters)和[**NDIS\_散点\_收集\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_scatter_gather_list_parameters)构造. 有关 VMQ 中的共享内存参数接收数据缓冲区的信息，请参阅[接收缓冲区中的共享内存](shared-memory-in-receive-buffers.md)。

[**NdisAllocateSharedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatesharedmemory)函数向调用方提供以下内容：

-   已分配内存的虚拟地址。

-   散播-聚集列表。

-   共享内存句柄-用于接收指示。

-   分配句柄-用于在以后标识内存。

微型端口驱动程序调用[**NdisFreeSharedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreesharedmemory)函数来释放队列的共享内存。 如果微型端口驱动程序为非默认队列分配了共享内存，则它将释放 OID 上下文中的共享内存[\_接收\_筛选器\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-free-queue)在释放队列时使用\_队列 OID。 微型端口驱动程序在[*MiniportHaltEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)函数的上下文中为默认队列分配的共享内存可用。

 

 






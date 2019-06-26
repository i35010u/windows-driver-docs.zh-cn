---
title: 共享内存资源分配
description: 共享内存资源分配
ms.assetid: cf030a0f-1202-4d10-b9a1-58d031345678
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aabcc37f41f2249de7dafd72471e3551ee543802
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379176"
---
# <a name="shared-memory-resource-allocation"></a>共享内存资源分配





若要为虚拟机队列分配共享的内存资源，微型端口驱动程序调用[ **NdisAllocateSharedMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocatesharedmemory)函数。 例如，微型端口驱动程序分配共享的内存，当它收到[OID\_接收\_筛选器\_队列\_分配\_完成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-queue-allocation-complete)OID。 此外，微型端口驱动程序可以共享的内存为分配默认的队列在网络适配器初始化过程。 有关分配队列的详细信息，请参阅[分配 VM 队列](allocating-a-vm-queue.md)。

微型端口驱动程序可以为队列分配更多的内存，直到释放队列。 释放队列的详细信息，请参阅[释放 VM 队列](freeing-a-vm-queue.md)。

[ **NDIS\_共享\_内存\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_shared_memory_parameters)结构指定的共享的内存分配请求的共享的内存参数。 微型端口驱动程序将向此结构传递[ **NdisAllocateSharedMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocatesharedmemory)函数。 NDIS 将传递到此结构[ **NetAllocateSharedMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-allocate_shared_memory_handler)函数 (即，分配\_共享\_内存\_处理程序入口点)。

微型端口驱动程序分配共享的内存，它指定以下：

-   队列标识符。

-   共享的内存长度。

-   如何使用共享的内存。 例如，微型端口驱动程序指定**NdisSharedMemoryUsageReceive**如果共享的内存是要用于接收缓冲区。

如果 NDIS\_共享\_内存优化\_参数\_未设置 CONTIGOUS 标志**标志**共享的成员可以包含在散播-聚集列表中指定的内存非连续内存。

[ **NDIS\_共享\_内存\_使用情况**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ne-ndis-_ndis_shared_memory_usage)枚举指定如何共享的内存使用。 NDIS\_共享\_内存\_中使用使用情况枚举[ **NDIS\_共享\_内存\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_shared_memory_parameters)并[ **NDIS\_散点图\_收集\_列表\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_scatter_gather_list_parameters)结构。 有关共享内存的信息中 VMQ 参数接收数据缓冲区，请参阅[接收缓冲区中的共享内存](shared-memory-in-receive-buffers.md)。

[ **NdisAllocateSharedMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocatesharedmemory)函数为调用方提供了以下：

-   已分配内存的虚拟地址。

-   散播-聚集列表。

-   共享的内存句柄的接收的指示。

-   分配句柄的用于标识内存更高版本。

微型端口驱动程序调用[ **NdisFreeSharedMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreesharedmemory)函数来释放队列的共享的内存。 如果微型端口驱动程序分配的非默认队列的共享的内存，则将释放的上下文中的共享的内存[OID\_接收\_筛选器\_免费\_队列](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-free-queue)时它的 OID正在释放队列。 微型端口驱动程序免费共享默认的队列的上下文中为它们分配的内存[ *MiniportHaltEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)函数。

 

 






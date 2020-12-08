---
title: 共享内存资源分配
description: 共享内存资源分配
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfb284d893d10f49aff6b8dd86e7ff62c32b9d75
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829163"
---
# <a name="shared-memory-resource-allocation"></a>共享内存资源分配





若要为 VM 队列分配共享内存资源，微型端口驱动程序将调用 [**NdisAllocateSharedMemory**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatesharedmemory) 函数。 例如，微型端口驱动程序在收到 [oid \_ 接收 \_ 筛选器 \_ 队列 \_ 分配 \_ 完成](./oid-receive-filter-queue-allocation-complete.md) oid 时，分配共享内存。 此外，小型端口驱动程序可以在网络适配器初始化期间为默认队列分配共享内存。 有关分配队列的详细信息，请参阅 [分配 VM 队列](allocating-a-vm-queue.md)。

在释放队列之前，微型端口驱动程序可以为队列分配更多内存。 有关释放队列的详细信息，请参阅 [释放 VM 队列](freeing-a-vm-queue.md)。

[**NDIS \_ shared \_ memory \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_shared_memory_parameters)结构指定共享内存分配请求的共享内存参数。 微型端口驱动程序将此结构传递给 [**NdisAllocateSharedMemory**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatesharedmemory) 函数。 NDIS 将此结构传递给 [**NetAllocateSharedMemory**](/windows-hardware/drivers/ddi/ndis/nc-ndis-allocate_shared_memory_handler) 函数 (即，分配 \_ 共享 \_ 内存 \_ 处理程序入口点) 。

当微型端口驱动程序分配共享内存时，它会指定以下内容：

-   队列标识符。

-   共享内存长度。

-   共享内存的使用方式。 例如，如果共享内存将用于接收缓冲区，则微型端口驱动程序将指定 **NdisSharedMemoryUsageReceive** 。

如果在 \_ \_ \_ Flags 成员中未设置 NDIS SHARED MEM PARAMETERS \_ CONTIGOUS 标志 **Flags** ，则可以在非连续内存中包含的分散收集列表中指定共享内存。

[**NDIS \_ shared \_ memory \_ 用量**](/windows-hardware/drivers/ddi/ndis/ne-ndis-_ndis_shared_memory_usage)枚举指定如何使用共享内存。 Ndis shared \_ memory \_ \_ 用量枚举用于 [**ndis \_ shared \_ memory \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_shared_memory_parameters) 和 [**ndis \_ 散播 \_ 聚集 \_ 列表 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_scatter_gather_list_parameters) 结构。 有关 VMQ 中的共享内存参数接收数据缓冲区的信息，请参阅 [接收缓冲区中的共享内存](shared-memory-in-receive-buffers.md)。

[**NdisAllocateSharedMemory**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatesharedmemory)函数向调用方提供以下内容：

-   已分配内存的虚拟地址。

-   散播-聚集列表。

-   共享内存句柄-用于接收指示。

-   分配句柄-用于在以后标识内存。

微型端口驱动程序调用 [**NdisFreeSharedMemory**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreesharedmemory) 函数来释放队列的共享内存。 如果微型端口驱动程序为非默认队列分配了共享内存，则它将在释放队列时在 [oid \_ 接收 \_ 筛选器 \_ \_ ](./oid-receive-filter-free-queue.md) 的上下文中释放共享内存。 微型端口驱动程序在 [*MiniportHaltEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt) 函数的上下文中为默认队列分配的共享内存可用。

 


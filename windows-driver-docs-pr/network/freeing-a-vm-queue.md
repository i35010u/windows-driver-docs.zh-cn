---
title: 释放 VM 队列
description: 释放 VM 队列
ms.assetid: 32679638-eeef-4e11-bf56-c96f047e4de7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab520cd4e41e66641738ab0033a7cf8fa4d24c05
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212475"
---
# <a name="freeing-a-vm-queue"></a>释放 VM 队列





为了释放接收队列，过量驱动程序 [会发出 oid \_ 接收 \_ 筛选器 \_ 释放 \_ 队列](./oid-receive-filter-free-queue.md) 集 OID 请求。 [**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**ndis \_ 接收 \_ 队列 \_ 可用 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_free_parameters)结构的指针，该结构具有类型为**ndis \_ 接收 \_ 队列 \_ ID**的队列标识符。

[OID \_接收 \_ 筛选器 \_ 空闲 \_ 队列](./oid-receive-filter-free-queue.md) 释放通过使用 [OID \_ 接收 \_ 筛选器 \_ 分配 \_ 队列](./oid-receive-filter-allocate-queue.md) OID 分配的过量驱动程序的接收队列。 有关分配接收队列的详细信息，请参阅 [分配 VM 队列](allocating-a-vm-queue.md)。

**注意**   始终分配默认队列，该队列具有**NDIS \_ 默认 \_ 接收 \_ 队列 \_ ID**的队列标识符，不能被释放。

 

过量驱动程序必须释放它在队列上设置的所有筛选器，然后才能释放队列。 此外，在调用 [**NdisCloseAdapterEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscloseadapterex) 函数以关闭到网络适配器的绑定之前，过量驱动程序必须释放在网络适配器上分配的所有接收队列。 NDIS 在调用微型端口驱动程序的 [*MiniportHaltEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt) 函数之前，释放在网络适配器上分配的所有队列。

当微型端口驱动程序收到释放队列的请求时，它将执行以下操作：

-   必须立即停止与队列关联的共享内存资源的 DMA。

-   生成指示 DMA 已停止的状态指示。

-   等待返回与队列关联的所有未完成的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构。

-   释放关联的共享内存和硬件资源。

当微型端口驱动程序收到 [OID \_ 接收 \_ 筛选器 \_ 释放 \_ 队列](./oid-receive-filter-free-queue.md) 集请求时，队列必须输入停止 dma 状态，停止队列上的 dma，微型端口驱动程序必须通过使用 [**NDIS \_ 状态 \_ 接收 \_ 队列 \_ 状态**](./ndis-status-receive-queue-state.md) 状态指示来指示状态更改。 有关队列状态的详细信息，请参阅 [队列状态和操作](queue-states-and-operations.md)。

当微型端口驱动程序发出 [**NDIS \_ 状态 \_ 接收 \_ 队列 \_ 状态**](./ndis-status-receive-queue-state.md) 状态指示后，它必须等待所有挂起的接收指示完成，然后才能释放关联的共享内存。 有关释放共享内存的详细信息，请参阅 [共享内存资源分配](shared-memory-resource-allocation.md)。

 


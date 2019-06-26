---
title: 释放 VM 队列
description: 释放 VM 队列
ms.assetid: 32679638-eeef-4e11-bf56-c96f047e4de7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c17deb842749d18affe722ba3c7a11fda793128d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382768"
---
# <a name="freeing-a-vm-queue"></a>释放 VM 队列





要释放接收队列，基础驱动程序将发出[OID\_接收\_筛选器\_免费\_队列](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-free-queue)集 OID 请求。 **InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含一个指向[ **NDIS\_接收\_队列\_免费\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_queue_free_parameters)结构类型的队列标识符**NDIS\_接收\_队列\_ID**。

[OID\_接收\_筛选器\_免费\_队列](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-free-queue)释放基础驱动程序通过使用分配的接收队列[OID\_接收\_筛选器\_分配\_队列](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-allocate-queue)OID。 有关分配接收队列的详细信息，请参阅[分配 VM 队列](allocating-a-vm-queue.md)。

**请注意**  默认队列，都有一个队列标识符的**NDIS\_默认\_接收\_队列\_ID**始终分配，且不能为释放。

 

基础驱动程序必须释放它在释放队列前在队列设置的所有筛选器。 此外，基础驱动程序必须释放它分配网络适配器调用之前的所有接收队列[ **NdisCloseAdapterEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscloseadapterex)函数以关闭到的网络适配器的绑定。 NDIS 释放之前它将调用微型端口驱动程序的网络适配器分配的所有队列[ *MiniportHaltEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)函数。

当微型端口驱动程序收到请求以释放队列时，执行以下操作：

-   与队列相关联的共享的内存资源，必须立即停止 DMA。

-   生成状态指示，以指示 DMA 已停止。

-   等待所有未完成[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构，与队列，若要返回相关联。

-   释放关联的共享的内存和硬件资源。

当微型端口驱动程序收到[OID\_接收\_筛选器\_免费\_队列](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-free-queue)集请求队列必须输入停止 DMA 状态，它将停止 DMA 上队列及其包含的微型端口驱动程序必须通过使用指示的状态更改[ **NDIS\_状态\_接收\_队列\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-receive-queue-state)状态指示。 队列状态的详细信息，请参阅[队列状态和操作](queue-states-and-operations.md)。

微型端口驱动程序问题后[ **NDIS\_状态\_接收\_队列\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-receive-queue-state)状态指示，它必须等待所有挂起接收指示完成之前它可以释放相关联的共享的内存。 有关释放共享的内存的详细信息，请参阅[共享的内存资源分配](shared-memory-resource-allocation.md)。

 

 






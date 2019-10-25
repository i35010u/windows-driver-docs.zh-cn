---
title: NDIS VMQ 实时迁移支持
description: NDIS VMQ 实时迁移支持
ms.assetid: 6872594a-35f8-4fbf-b764-22b286fb940c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 08547368d2678998a75cd6060c44d6dfd0c9a021
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834644"
---
# <a name="ndis-vmq-live-migration-support"></a>NDIS VMQ 实时迁移支持





若要支持实时迁移，可在任何指令或挂起的 i/o 边界处暂停虚拟机（VM）。 也就是说，VM 可能无法完成挂起的接收请求。 因此，网络虚拟服务提供程序（VSP）会将接收到的所有数据包返回给未返回给 VM 的基础网络适配器。

**请注意**，hyper-v 中的  ，子分区也称为 VM。

 

在另一台主机上重启 VM 时，新主机上的网络 VSP 会处理恢复的 VM 返回的接收数据包，并且不会将其向下传递到微型端口驱动程序中的新基础。 迁移完成后，与 VM 关联的接收队列会被释放，并可重复用于另一个 VM。

**请注意**  新的网络适配器可能不支持 VMQ。

 

当 NDIS 请求微型端口驱动程序释放 VMQ 接收队列时，将执行以下步骤：

1.  网络适配器停止数据的 DMA 传输以接收与接收队列关联的缓冲区，在此之后，队列必须进入 DMA 停止状态。 网络适配器在收到[oid\_接收\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-clear-filter)时可能停止 DMA 活动，\_清除\_筛选 OID 请求以清除接收队列中的最后一个 set 筛选器。

2.  微型端口驱动程序生成[**ndis\_状态\_接收\_队列\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-receive-queue-state)状态指示与[**NDIS\_接收\_队列\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_receive_queue_state)结构集的**QueueState**成员**NdisReceiveQueueOperationalStateDmaStopped**以通知 NDIS 已停止 DMA 传输。

3.  微型端口驱动程序等待该队列的所有指示接收数据包返回到微型端口驱动程序。

4.  通过调用[**NdisFreeSharedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreesharedmemory)，微型端口驱动程序可释放它为网络适配器的接收缓冲区分配的、与队列关联的所有共享内存。

5.  微型端口驱动程序完成[OID\_接收\_FILTER\_可用的\_队列](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-free-queue)OID 请求，以释放接收队列。

有关队列状态的详细信息，请参阅[NDIS VM 队列状态](ndis-virtual-machine-queue-states.md)。

 

 






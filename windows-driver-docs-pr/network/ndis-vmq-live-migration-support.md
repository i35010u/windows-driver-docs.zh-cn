---
title: NDIS VMQ 实时迁移支持
description: NDIS VMQ 实时迁移支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c718eafd680dfbdd4aef8cea5f8a0bfe5bcaa17
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839881"
---
# <a name="ndis-vmq-live-migration-support"></a>NDIS VMQ 实时迁移支持





若要支持实时迁移，可在任何指令或挂起的 i/o 边界处暂停虚拟机 (VM) 。 也就是说，VM 可能无法完成挂起的接收请求。 因此，网络虚拟服务提供商 (VSP) 会将接收到的所有数据包返回给 VM 未返回的基础网络适配器。

**注意**  在 Hyper-v 中，子分区也称为 VM。

 

在另一台主机上重启 VM 时，新主机上的网络 VSP 会处理恢复的 VM 返回的接收数据包，并且不会将其向下传递到微型端口驱动程序中的新基础。 迁移完成后，与 VM 关联的接收队列会被释放，并可重复用于另一个 VM。

**注意**  新网络适配器可能不支持 VMQ。

 

当 NDIS 请求微型端口驱动程序释放 VMQ 接收队列时，将执行以下步骤：

1.  网络适配器停止数据的 DMA 传输以接收与接收队列关联的缓冲区，在此之后，队列必须进入 DMA 停止状态。 网络适配器在收到 [oid \_ 接收筛选器 " \_ \_ 清除 \_ 筛选器](./oid-receive-filter-clear-filter.md) oid 请求" 时可能会停止 DMA 活动，以清除接收队列中的最后一个 set 筛选器。

2.  微型端口驱动程序使用 [**ndis \_ 接收 \_ 队列 \_ 状态**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_receive_queue_state)结构设置为 " **NdisReceiveQueueOperationalStateDmaStopped** " 的 **QueueState** 成员生成 [**NDIS \_ 状态 \_ 接收 \_ 队列 \_ 状态**](./ndis-status-receive-queue-state.md)状态指示，以通知 NDIS 已停止 DMA 传输。

3.  微型端口驱动程序等待该队列的所有指示接收数据包返回到微型端口驱动程序。

4.  通过调用 [**NdisFreeSharedMemory**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreesharedmemory)，微型端口驱动程序可释放它为网络适配器的接收缓冲区分配的、与队列关联的所有共享内存。

5.  微型端口驱动程序完成 [OID \_ 接收 \_ 筛选器 \_ 免费 \_ 队列](./oid-receive-filter-free-queue.md) OID 请求，以释放接收队列。

有关队列状态的详细信息，请参阅 [NDIS VM 队列状态](ndis-virtual-machine-queue-states.md)。

 


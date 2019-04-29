---
title: NDIS VMQ 实时迁移支持
description: NDIS VMQ 实时迁移支持
ms.assetid: 6872594a-35f8-4fbf-b764-22b286fb940c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 48e61e6bfa1e72abd3cc25effeee6841e96f1820
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368992"
---
# <a name="ndis-vmq-live-migration-support"></a>NDIS VMQ 实时迁移支持





若要支持实时迁移，可以在任何指令或挂起的 I/O 边界暂停虚拟机 (VM)。 也就是说，VM 可能无法完成挂起的接收请求。 因此，网络虚拟服务提供商 (VSP) 返回所有已接收数据包到该 VM 未返回的基础网络适配器。

**请注意**  HYPER-V 中，子分区也称为是 VM。

 

在另一台主机上重新启动 VM 时，网络 VSP 新主机上的能够处理已恢复的 VM 返回并不将它们传递到新的基础微型端口驱动程序中的接收数据包。 在迁移完毕后，与 VM 相关联的接收队列将被释放，另一个 vm 可以重用它。

**请注意**  新的网络适配器可能不支持 VMQ。

 

NDIS 请求微型端口驱动程序以释放 VMQ 时接收队列，则会遵循以下步骤：

1.  网络适配器停止 DMA 将数据传输到接收队列，队列必须在其后输入 DMA 停止状态与相关联的接收缓冲区。 网络适配器可能停止 DMA 活动，当它收到[OID\_接收\_筛选器\_清除\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569785)OID 请求清除上接收的最后一组筛选器队列。

2.  微型端口驱动程序将生成[ **NDIS\_状态\_接收\_队列\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff567417)与状态指示**QueueState**的成员[ **NDIS\_接收\_队列\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff567214)结构设置为**NdisReceiveQueueOperationalStateDmaStopped**通知 NDIS DMA 传输已停止。

3.  微型端口驱动程序等待所有所指示接收该队列要返回给微型端口驱动程序的数据包。

4.  微型端口驱动程序释放它分配为网络适配器的接收缓冲区通过调用与队列关联的所有共享的内存[ **NdisFreeSharedMemory**](https://msdn.microsoft.com/library/windows/hardware/ff562601)。

5.  微型端口驱动程序完成[OID\_接收\_筛选器\_免费\_队列](https://msdn.microsoft.com/library/windows/hardware/ff569789)OID 请求免费接收队列。

队列状态的详细信息，请参阅[NDIS VM 队列状态](ndis-virtual-machine-queue-states.md)。

 

 






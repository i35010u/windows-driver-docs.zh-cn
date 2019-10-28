---
title: 使用硬件队列的 RSS
description: 使用硬件队列的 RSS
ms.assetid: f37caef9-6d22-4d17-8628-0c3f93de470e
keywords:
- 接收方缩放 WDK 网络，硬件队列
- RSS WDK 网络，硬件队列
- 硬件排队 WDK RSS
- 接收队列 WDK RSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03b7fed29d69f0d321b1df05d9fed1a79443becc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841999"
---
# <a name="rss-with-hardware-queuing"></a>使用硬件队列的 RSS





使用单个硬件接收队列解决方案，具有硬件队列的 RSS 可改善相对于 RSS 的系统性能。 支持硬件队列的 Nic 将接收的数据分配给多个接收队列。 接收队列与 CPU 关联。 NIC 基于哈希值和一个间接寻址表将接收的数据分配给 Cpu。

下图说明了包含 NIC 接收队列的 RSS。

![阐释包含 nic 接收队列的 rss 的示意图](images/rssqstack.png)

在图中，虚线箭头表示接收处理的备用路径。 RSS 无法控制接收初始 ISR 调用的 CPU。 驱动程序不必将数据排队，因此它可以立即计划正确 Cpu 上的初始 Dpc。

对于每个中断，将重复以下过程：

1.  NIC：
    1.  使用 DMA 来填充已接收数据的缓冲区。

        小型端口驱动程序在初始化期间将接收缓冲区分配到共享内存中。

    2.  计算哈希值。
    3.  在缓冲区中排队等待 CPU，并向微型端口驱动程序提供队列分配。

        例如，NIC 可能会循环步骤1-3，并在收到一定数量的数据包后 DMA 一个 CPU 分配列表。 特定机制留给 NIC 设计。

    4.  中断系统。

        系统在一个中断中处理的接收缓冲区在 Cpu 之间分布。

2.  NDIS 在系统确定的 CPU 上调用微型端口驱动程序的[*MiniportInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_isr)函数（ISR）。

3.  微型端口驱动程序请求 NDIS 对每个具有非空队列的 Cpu 的延迟过程调用（Dpc）进行排队。

    请注意，必须先完成所有 Dpc，驱动程序才会启用中断。 另请注意，ISR 可能在没有要处理的缓冲区的 CPU 上运行。

4.  NDIS 为每个排队的 DPC 调用[*MiniportInterruptDPC*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_interrupt_dpc)函数。 给定 CPU 上的 DPC：
    1.  为其队列中所有接收的缓冲区生成接收描述符，并指示驱动程序堆栈上的数据。

        有关详细信息，请参阅[指示 RSS 接收数据](indicating-rss-receive-data.md)。

    2.  如果是要完成的最后一个 DPC，则启用中断。 此中断已完成，进程将再次启动。 驱动程序必须使用原子操作来确定要完成的最后一个 DPC。 例如，驱动程序可以使用[**NdisInterlockedDecrement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisinterlockeddecrement)函数来实现原子计数器。

 

 






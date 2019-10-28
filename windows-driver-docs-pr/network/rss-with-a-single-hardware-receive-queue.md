---
title: 使用单个硬件接收队列的 RSS
description: 使用单个硬件接收队列的 RSS
ms.assetid: 835f5646-4514-4973-978a-9bab0777a66c
keywords:
- 接收方缩放 WDK 网络，硬件队列
- RSS WDK 网络，硬件队列
- 硬件排队 WDK RSS
- 接收队列 WDK RSS
- 单个接收队列 WDK RSS
- 多个接收队列 WDK RSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f144837af3abe9e5f40b7607d37361008367cc3e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842002"
---
# <a name="rss-with-a-single-hardware-receive-queue"></a>使用单个硬件接收队列的 RSS





微型端口驱动程序可以支持支持 RSS 哈希计算和单个接收描述符队列的 Nic 的 RSS。

下图说明了使用单个接收描述符队列进行 RSS 处理。

![阐释使用单个接收描述符队列进行 rss 处理的关系图](images/rssswstack.png)

在图中，虚线箭头表示接收处理的备用路径。 RSS 无法控制接收初始 ISR 调用的 CPU。

与非 RSS 接收处理不同，基于 RSS 的接收处理分布在多个 Cpu 上。 另外，对给定连接的处理可以绑定到给定的 CPU。

对于每个中断，将重复以下过程：

1.  NIC 使用 DMA 来填充已接收数据的缓冲区，并使系统中断。

    小型端口驱动程序在初始化期间将接收缓冲区分配到共享内存中。

2.  NIC 可随时填充其他接收缓冲区，但不会再次中断，直到微型端口驱动程序启用中断。

    系统在一个中断中处理的接收的缓冲区可以与多个不同的网络连接关联。

3.  NDIS 在系统确定的 CPU 上调用微型端口驱动程序的[*MiniportInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_isr)函数（ISR）。

4.  ISR 禁用中断，并请求 NDIS 对延迟的过程调用（DPC）进行排队以处理接收的数据。

5.  NDIS 在当前 CPU 上调用[*MiniportInterruptDPC*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_interrupt_dpc)函数（DPC）。 在 DPC 中：

    1.  微型端口驱动程序使用 NIC 为每个接收的缓冲区计算的哈希值，并将每个接收的缓冲区重新分配到与 CPU 关联的接收队列。
    2.  当前 DPC 请求 NDIS 为与非空接收队列关联的每个其他 Cpu 将 DPC 排队。
    3.  如果当前 DPC 在与非空队列关联的 CPU 上运行，则当前 DPC 会处理关联的接收缓冲区，并指示在驱动程序堆栈上收到的数据。

    分配队列和排队其他 Dpc 需要额外的处理开销。 若要提高系统性能，则必须使用更好的可用 Cpu 利用率来抵消此开销。

6.  给定 CPU 上的 DPC：
    1.  处理与接收队列关联的接收缓冲区，并指示驱动程序堆栈上的数据。 有关详细信息，请参阅[指示 RSS 接收数据](indicating-rss-receive-data.md)。
    2.  如果是要完成的最后一个 DPC，则启用中断。 此中断已完成，进程将再次启动。 驱动程序必须使用原子操作来确定要完成的最后一个 DPC。 例如，驱动程序可以使用[**NdisInterlockedDecrement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisinterlockeddecrement)函数来实现原子计数器。

 

 






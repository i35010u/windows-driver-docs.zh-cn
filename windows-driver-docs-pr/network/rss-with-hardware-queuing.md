---
title: 使用硬件队列的 RSS
description: 使用硬件队列的 RSS
ms.assetid: f37caef9-6d22-4d17-8628-0c3f93de470e
keywords:
- 接收方缩放 WDK 网络硬件队列
- RSS WDK 网络、 硬件队列
- 硬件队列 WDK RSS
- 接收队列 WDK RSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a8d51be9abba531e9702cd058371ed32dc19039
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382136"
---
# <a name="rss-with-hardware-queuing"></a>使用硬件队列的 RSS





与硬件队列的 RSS 可以提高系统性能相对于 RSS 与单个硬件接收队列解决方案。 接收队列支持的硬件队列分配收到数据，到多个 Nic。 接收队列相关联的 CPU。 NIC 将接收到的数据分配给基于哈希值和间接表上的 Cpu。

下图说明了与网络接口卡的 RSS 接收队列。

![与网络接口卡的关系图演示 rss 接收队列](images/rssqstack.png)

在图中，虚线的箭头表示接收处理的备用路径。 RSS 无法控制接收初始 ISR 调用的 CPU。 该驱动程序不需要该数据加入队列，因此它可以立即计划初始 Dpc 在正确的 Cpu 上。

对于每个中断重复以下过程：

1.  NIC:
    1.  使用 DMA 与接收的数据填充缓冲区。

        微型端口驱动程序在初始化期间分配共享内存中的接收缓冲区。

    2.  计算哈希值。
    3.  为 CPU 队列缓冲区，并提供给微型端口驱动程序的队列分配。

        例如，NIC 可以循环步骤 1-3 和 DMA CPU 分配分配后接收一定数量的数据包。 特定的机制为从左到 NIC 设计。

    4.  系统会中断。

        在 Cpu 之间分发时系统中一个中断处理的接收的缓冲区。

2.  NDIS 调用微型端口驱动程序[ *MiniportInterrupt* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_isr)系统确定 CPU 上的函数 (ISR)。

3.  微型端口驱动程序请求 NDIS 延缓的过程调用 (Dpc) 对队列的每个 Cpu 具有非空队列。

    请注意，该驱动程序之前必须完成所有 Dpc 启用中断。 另请注意，可能会不有任何缓冲区来处理的 CPU 上运行 ISR。

4.  NDIS 调用[ *MiniportInterruptDPC* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_interrupt_dpc)函数每个排队 DPC。 在给定 CPU DPC:
    1.  生成其队列中接收所有的接收缓冲区描述符，并指示驱动程序堆栈上的数据。

        有关详细信息，请参阅[接收数据，该值指示 RSS](indicating-rss-receive-data.md)。

    2.  启用中断，如果它是最后一个的 DPC 才能完成。 此中断已完成，此过程再次启动。 该驱动程序必须使用原子操作来标识要完成最后一个 DPC。 例如，可以使用该驱动程序[ **NdisInterlockedDecrement** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisinterlockeddecrement)函数，实现原子计数器。

 

 






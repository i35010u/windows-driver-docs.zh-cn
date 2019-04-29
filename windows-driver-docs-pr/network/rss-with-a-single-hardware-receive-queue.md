---
title: 使用单个硬件接收队列的 RSS
description: 使用单个硬件接收队列的 RSS
ms.assetid: 835f5646-4514-4973-978a-9bab0777a66c
keywords:
- 接收方缩放 WDK 网络硬件队列
- RSS WDK 网络、 硬件队列
- 硬件队列 WDK RSS
- 接收队列 WDK RSS
- 单个接收队列 WDK RSS
- 多个接收队列 WDK RSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f6ac453e65e8a3b992b6ef3d8521368308d929eb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359783"
---
# <a name="rss-with-a-single-hardware-receive-queue"></a>使用单个硬件接收队列的 RSS





微型端口驱动程序可以支持 RSS 支持 RSS 哈希计算的 Nic 和一个接收描述符队列。

下图说明了 RSS 处理使用单个接收描述符队列。

![关系图演示 rss 处理使用单个接收描述符队列](images/rssswstack.png)

在图中，虚线的箭头表示接收处理的备用路径。 RSS 无法控制接收初始 ISR 调用的 CPU。

与非 RSS 不同接收处理，基于 RSS 的接收处理分布在多个 Cpu。 此外，给定连接的处理可以绑定到给定的 CPU。

对于每个中断重复以下过程：

1.  NIC 使用 DMA 与接收的数据填充缓冲区并中断系统。

    微型端口驱动程序在初始化期间分配共享内存中的接收缓冲区。

2.  NIC 可以填充附加在任何时间接收缓冲区，但不会中断再次直到微型端口驱动程序启用中断。

    系统中一个中断处理的接收的缓冲区可以与多个不同的网络连接相关联。

3.  NDIS 调用微型端口驱动程序[ *MiniportInterrupt* ](https://msdn.microsoft.com/library/windows/hardware/ff559395)系统确定 CPU 上的函数 (ISR)。

4.  ISR 禁用中断和请求 NDIS 排队延迟的过程调用 (DPC) 来处理接收到的数据。

5.  NDIS 调用[ *MiniportInterruptDPC* ](https://msdn.microsoft.com/library/windows/hardware/ff559398)函数 (DPC) 上当前的 CPU。 在 DPC:

    1.  微型端口驱动程序使用每个接收缓冲区 NIC 计算的哈希值，并将重新分配到接收队列关联的 CPU 的每个接收的缓冲区。
    2.  当前 DPC 请求 NDIS DPC 队列的每个其他与非空接收队列关联的 Cpu。
    3.  如果当前 DPC 与非空队列关联的 CPU 上运行，当前 DPC 处理关联的接收缓冲区，并指示驱动程序堆栈中向上接收到的数据。

    将队列，分配和其他的 Dpc 队列需要额外的处理开销。 若要实现改进了的系统性能，必须通过更好地利用可用的 Cpu 偏移此开销。

6.  在给定 CPU DPC:
    1.  处理其接收队列与相关联的接收缓冲区，并指示驱动程序堆栈上的数据。 有关详细信息，请参阅[接收数据，该值指示 RSS](indicating-rss-receive-data.md)。
    2.  启用中断，如果它是最后一个的 DPC 才能完成。 此中断已完成，此过程再次启动。 该驱动程序必须使用原子操作来标识要完成最后一个 DPC。 例如，可以使用该驱动程序[ **NdisInterlockedDecrement** ](https://msdn.microsoft.com/library/windows/hardware/ff562751)函数，实现原子计数器。

 

 






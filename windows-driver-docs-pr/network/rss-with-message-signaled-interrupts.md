---
title: 使用消息信号中断的 RSS
description: 使用消息信号中断的 RSS
keywords:
- 接收方缩放 WDK 网络，消息信号中断
- RSS WDK 网络，消息信号中断
- 消息-已发出信号中断 WDK 网络，RSS
- Msi WDK 网络，RSS
- MSI-X WDK 网络，RSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92280ae592742a3eac2ce5edb30b06c61f22bdf3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840293"
---
# <a name="rss-with-message-signaled-interrupts"></a>使用消息信号中断的 RSS





微型端口驱动程序可以 (Msi) 支持消息信号中断，以提高 RSS 性能。 Msi 使 NIC 能够请求 CPU 上将处理收到的数据的中断。 有关 NDIS 对 MSI 的支持的详细信息，请参阅 [NDIS MSI-X](ndis-msi-x.md)。

下图说明了包含 MSI X 的 RSS。

![阐释具有 msi 的 rss 的示意图-x](images/rssmsistack.png)

在图中，虚线箭头表示针对不同连接的处理。 使用具有 MSI 的 RSS-X 允许 NIC 中断正确的连接 CPU。

对于每个中断，将重复以下过程：

1.  NIC：
    1.  使用 DMA 来填充已接收数据的缓冲区。

        小型端口驱动程序在初始化期间将接收缓冲区分配到共享内存中。

    2.  计算哈希值。
    3.  将缓冲区排队到 CPU，并向微型端口驱动程序提供队列分配。 例如，NIC 可能会循环步骤1-3，并在收到一定数量的数据包后 DMA 一个 CPU 分配列表。 特定机制留给 NIC 设计。
    4.  使用 MSI X 会中断与非空队列关联的 CPU。

2.  NIC 可以在任何时候填写额外的接收缓冲区并将其添加到队列中，但在微型端口驱动程序启用该 CPU 的中断之前，不会再次中断该 CPU。

3.  NDIS 在当前 CPU 上调用微型端口驱动程序的 ISR ( [*MiniportInterrupt*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_isr)) 。

4.  ISR 禁用当前 CPU 上的中断，并对当前 CPU 上的 DPC 进行排队。

    当 DPC 正在当前 CPU 上运行时，其他 Cpu 上的中断仍可能发生。

5.  NDIS 为每个排队的 DPC 调用 [*MiniportInterruptDPC*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_interrupt_dpc) 函数。 每个 DPC：
    1.  为其队列中所有接收的缓冲区生成接收描述符，并指示驱动程序堆栈上的数据。 有关详细信息，请参阅 [指示 RSS 接收数据](indicating-rss-receive-data.md)。
    2.  为当前 CPU 启用中断。 此中断已完成，进程将再次启动。 请注意，无需执行任何原子操作即可跟踪其他 Dpc 的进度。

 


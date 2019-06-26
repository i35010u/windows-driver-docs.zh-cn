---
title: 使用消息信号中断的 RSS
description: 使用消息信号中断的 RSS
ms.assetid: 3c1776cf-f870-4910-88b2-9b5a9544cdf8
keywords:
- 接收方缩放 WDK 网络，消息信号中断
- RSS WDK 网络、 消息信号中断
- 消息信号中断 WDK 网络 RSS
- Msi WDK 网络 RSS
- MSI X WDK 网络 RSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16470ce0747917f85ae9b63f491966e334d22dd8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382128"
---
# <a name="rss-with-message-signaled-interrupts"></a>使用消息信号中断的 RSS





微型端口驱动程序可以支持消息信号中断 (Msi) 以提高 RSS 性能。 Msi 启用 NIC 以请求将处理接收到的数据在 CPU 上中断。 有关 MSI 的 NDIS 支持的详细信息，请参阅[NDIS MSI-X](ndis-msi-x.md)。

下图说明了与 MSI X 的 RSS。

![说明与 msi x rss 的关系图](images/rssmsistack.png)

在图中，虚线的箭头表示不同的连接上的处理。 使用 MSI X RSS 允许要中断的连接正确的 CPU 的 NIC。

对于每个中断重复以下过程：

1.  NIC:
    1.  使用 DMA 与接收的数据填充缓冲区。

        微型端口驱动程序在初始化期间分配共享内存中的接收缓冲区。

    2.  计算哈希值。
    3.  队列为一个 CPU 的缓冲区，并提供给微型端口驱动程序的队列分配。 例如，NIC 可以循环步骤 1-3 和 DMA CPU 分配分配后接收一定数量的数据包。 特定的机制为从左到 NIC 设计。
    4.  使用 MSI X，中断与非空队列关联的 CPU。

2.  NIC 可以填充其他接收缓冲区并在任何时间将它们添加到队列，但不会中断该 CPU 再次直到微型端口驱动程序启用该 cpu 中断。

3.  NDIS 调用微型端口驱动程序的 ISR ( [ *MiniportInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_isr)) 上当前的 CPU。

4.  ISR 禁用当前的 CPU 上的中断和队列上当前 CPU DPC。

    DPC 运行在当前的 CPU 上时，其他 Cpu 上仍会发生中断。

5.  NDIS 调用[ *MiniportInterruptDPC* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_interrupt_dpc)函数每个排队 DPC。 每个 DPC:
    1.  生成其队列中接收所有的接收缓冲区描述符，并指示驱动程序堆栈上的数据。 有关详细信息，请参阅[接收数据，该值指示 RSS](indicating-rss-receive-data.md)。
    2.  当前 cpu 启用中断。 此中断已完成，此过程再次启动。 请注意，没有以原子操作需要跟踪其他 Dpc 的进度。

 

 






---
title: NDIS 虚拟机队列 (VMQ) 简介
description: NDIS 虚拟机队列 (VMQ) 简介
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4fe829f2a1b69f3122825d77f5373c20f5653265
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808623"
---
# <a name="introduction-to-ndis-virtual-machine-queue-vmq"></a>NDIS 虚拟机队列 (VMQ) 简介





许多网络适配器可以为网络服务器 (MAC) 地址支持多个单播媒体访问控制。 因此，网络适配器可以接收目标 MAC 地址与在不处于混合模式下的网络适配器硬件上设置的任何单播 MAC 地址相匹配的网络数据帧。 此类硬件可以为每个 MAC 地址分配接收队列，并将具有匹配 MAC 地址的传入帧路由到队列。 此功能结合了从分配给每个虚拟机的内存地址空间为每个队列分配接收缓冲区的功能，这是 VMQ 支持所需的主要功能。

具备 VMQ 功能的网络适配器可以使用 DMA 将所有传入帧（应路由到接收队列）传输到为该队列分配的接收缓冲区。 微型端口驱动程序可以通过一个接收指示调用来指示接收队列中的所有帧。

VMQ 提供以下功能：

-   通过为多个虚拟机 (Vm) 多个处理器之间分配网络流量的处理，提高网络吞吐量。

    **注意**  在 Hyper-v 中，子分区也称为 VM。

     

-   将接收数据包筛选卸载到网络适配器硬件，从而降低 CPU 利用率。

-   使用 DMA 阻止网络数据复制将数据直接传输到 VM 内存。

-   拆分网络数据以提供安全的环境。 有关安全问题的详细信息，请参阅 [ (VM) 共享内存的 NDIS 虚拟机的安全问题](security-issues-with-ndis-virtual-machine--vm--shared-memory.md)。

    **注意**  从 NDIS 6.30 和 Windows Server 2012 开始，不再支持将网络数据拆分为单独的预测先行缓冲区。

     

-   支持实时迁移。 有关实时迁移的详细信息，请参阅 [NDIS VMQ 实时迁移支持](ndis-vmq-live-migration-support.md)。

为了引入高级 VMQ 概念，本部分包括以下其他主题：

[VMQ 组件](vmq-components.md)

[VMQ 接收队列](vmq-receive-queues.md)

[VMQ 接收筛选器](vmq-receive-filters.md)

 

 






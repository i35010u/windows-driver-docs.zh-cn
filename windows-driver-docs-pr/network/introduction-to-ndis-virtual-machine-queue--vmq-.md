---
title: NDIS 虚拟机队列 (VMQ) 简介
description: NDIS 虚拟机队列 (VMQ) 简介
ms.assetid: 03c6bbd1-bd4f-415f-b4ed-c6e812c50f8d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5aad0b79cf7eb6ca1d3d468b6908270a4b1d6b3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329882"
---
# <a name="introduction-to-ndis-virtual-machine-queue-vmq"></a>NDIS 虚拟机队列 (VMQ) 简介





许多网络适配器可以支持网络服务器的多个单播媒体访问控制 (MAC) 地址。 因此，网络适配器可以接收网络与目标 MAC 地址相匹配的任何单播 MAC 地址不是在混合模式中设置的网络适配器硬件的数据帧。 此类硬件可以为每个 MAC 地址分配接收队列并将具有匹配的 MAC 地址的传入帧发送到队列。 此功能，结合能够分配接收从分配给每个虚拟机，是所需的 VMQ 的支持的主要功能的内存地址空间为每个队列的缓冲区。

支持 VMQ 的网络适配器可以使用 DMA 将传输到接收队列分配给该队列的接收缓冲区应路由的所有传入的帧。 微型端口驱动程序可以指示所有一次接收指示调用接收队列中的帧。

VMQ 提供以下功能：

-   通过将分布在多个处理器之间的多个虚拟机 (Vm) 的网络通信量的处理可以提高网络吞吐量。

    **请注意**  HYPER-V 中，子分区也称为是 VM。

     

-   减少 CPU 使用率通过卸载接收的数据包筛选网络适配器硬件。

-   通过使用 DMA 将数据传输直接到虚拟机内存来防止网络数据复制。

-   将拆分网络数据，以提供安全的环境。 有关安全问题的详细信息，请参阅[NDIS 虚拟机 (VM) 共享内存的安全问题](security-issues-with-ndis-virtual-machine--vm--shared-memory.md)。

    **请注意**  从 NDIS 6.30 和 Windows Server 2012 开始，将网络数据拆分为单独的预测先行缓冲区不再受支持。

     

-   支持实时迁移。 有关实时迁移的详细信息，请参阅[NDIS VMQ 实时迁移支持](ndis-vmq-live-migration-support.md)。

若要引入高级 VMQ 概念，本部分包括以下其他主题：

[VMQ 组件](vmq-components.md)

[VMQ 接收队列](vmq-receive-queues.md)

[VMQ 接收筛选器](vmq-receive-filters.md)

 

 






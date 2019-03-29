---
title: 接收端缩放简介
description: 接收端缩放简介
ms.assetid: 492628a7-ca2e-40cd-bf81-53a925130422
keywords:
- 接收方缩放 WDK 网络，有关接收方缩放
- RSS WDK 网络、 有关接收方缩放
- CPU 确定 WDK RSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4b3106fd9a3a588341d4025db11f76cad97172c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575930"
---
# <a name="introduction-to-receive-side-scaling"></a>接收端缩放简介





接收的方缩放 (RSS) 是一种网络驱动程序技术实现高效的网络分布在多处理器系统中接收处理跨多个 Cpu。

**请注意**  因为相同的核心处理器共享相同的执行引擎上的超线程 Cpu，效果不是为具有多个核处理器相同。 出于此原因，RSS 不使用超线程处理器。

 

若要有效地处理接收的数据，微型端口驱动程序收到中断服务函数计划延迟的过程调用 (DPC)。 不使用 RSS，典型 DPC 指示 DPC 调用中接收的所有数据。 因此，所有与中断相关联的接收处理运行在 CPU 上接收中断的发生位置。 有关非 RSS 概述接收处理，请参阅[处理非 RSS 接收](non-rss-receive-processing.md)。

使用 RSS，NIC 和微型端口驱动程序提供的功能来计划在其他处理器上接收 dpc 进行标记。 此外，RSS 设计可确保与给定连接关联的处理会保留在已分配的 CPU 上。 NIC 实现一个哈希函数，并生成的哈希值提供的方法来选择一个 CPU。

下图说明了用于确定 CPU 的 RSS 机制。

![说明用于确定 cpu 的 rss 机制的关系图](images/rss.png)

NIC 使用的哈希函数来计算哈希值通过定义区域 （哈希类型） 中接收的网络数据。 定义的区域可以是不连续。

数的哈希值的最低有效位 (LSBs) 用于编制索引的间接寻址表。 间接寻址表中的值用于将接收到的数据分配给一个 CPU。 有关详细的间接寻址表有关的信息，请参阅[RSS 配置](rss-configuration.md)。

消息信号中断 (MSI) 支持，NIC 可以还中断关联的 CPU。 有关 Msi 的 NDIS 支持的详细信息，请参阅[NDIS MSI-X](ndis-msi-x.md)。

通过减少，RSS 可以提高网络系统性能：

-   通过分发的处理延迟接收处理 NIC 中跨多个 Cpu。

    这有助于确保没有 CPU 负载很重时另一个 CPU 处于空闲状态。

-   旋转锁开销通过增加共享数据的软件算法在 CPU 执行相同的概率。

    数值调节钮锁定开销时发生，例如上卸下 cpu 0, 函数执行都拥有 CPU1 上运行的函数必须访问的数据的自旋锁。 CPU1 旋转 （等待），直到卸下 cpu 0 释放锁。

-   通过增加共享数据的软件算法在 CPU 执行相同的概率，重新加载缓存和其他资源。

    此类重新加载，例如，当执行并访问上卸下 cpu 0，共享的数据的函数执行时发生上 CPU1 中后续中断。

若要实现这些性能改进的安全环境中，RSS 提供了以下机制：

-   分布式的处理

    RSS 将的处理进程分布到多个 Cpu Dpc 在给定 NIC 中接收的指示。

-   按序处理

    RSS 可保留已接收的数据包的传递的顺序。 对于每个网络连接，RSS 进程收到指示关联的 CPU 上。 有关 RSS 的详细信息接收处理，请参阅[接收数据，该值指示 RSS](indicating-rss-receive-data.md)。

-   动态负载平衡

    RSS 提供了一种方法来重新平衡 Cpu 之间的网络处理负载，因为主机系统负载各不相同。 若要重新平衡负荷，过量驱动程序可以更改间接表。 有关指定间接表的详细信息，哈希处理类型和哈希函数，请参阅[RSS 配置](rss-configuration.md)。

-   发送方缩放

    RSS 可让进程发送和接收端数据在同一 CPU 上的给定连接的驱动程序堆栈。 通常情况下，基础驱动程序 (例如，TCP) 发送数据块的一部分，并发送数据的平衡性之前等待确认。 然后，此确认触发器后续发送请求。 RSS 间接表标识接收数据处理的特定 CPU。 默认情况下，发送处理在上运行相同的 CPU 如果它由接收确认触发。 驱动程序还可以指定 CPU （例如，如果使用计时器）。

-   安全哈希

    RSS 包括一个签名，它提供了更高的安全性。 此签名保护系统免受恶意远程主机要强行使系统进入不平衡状态可能会尝试。

-   MSI X 支持

    RSS，与支持 MSI X 运行中断服务例程 (ISR) 更高版本执行 DPC 在同一 CPU 上。 这将减少系统开销并重新加载缓存的自旋锁。

下图说明了 RSS 的硬件支持的级别。

![说明的 rss 硬件支持的级别的关系图](images/rss-hw.png)

有三个可能的 RSS 硬件支持级别：

<a href="" id="hash-calculation-with-a-single-queue"></a>使用单个队列的哈希计算  
NIC 计算的哈希值并微型端口驱动程序将接收到的数据包分配给与 Cpu 相关联的队列。 有关详细信息，请参阅[与单个硬件接收队列的 RSS](rss-with-a-single-hardware-receive-queue.md)。

<a href="" id="hash-calculation-with-multiple-receive-queues"></a>具有多个哈希计算接收队列  
NIC 将分配给与 Cpu 相关联的队列的接收的数据缓冲区。 有关详细信息，请参阅[与硬件队列的 RSS](rss-with-hardware-queuing.md)。

<a href="" id="message-signaled-interrupts--msis-"></a>发出信号的消息可以中断 (Msi)  
NIC 会中断应处理接收到的数据包的 CPU。 有关详细信息，请参阅[与消息信号中断 RSS](rss-with-message-signaled-interrupts.md)。

始终在 32 位哈希值将传递 NIC。

 

 






---
title: 接收端缩放简介
description: 接收端缩放简介
keywords:
- 接收方缩放 WDK 网络，关于接收方缩放
- RSS WDK 网络，关于接收方缩放
- CPU 确定 WDK RSS
ms.date: 09/04/2020
ms.localizationpriority: medium
ms.custom: contperfq1
ms.openlocfilehash: 1d499ddc8090d4f3640032114e6840ce5524254d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803689"
---
# <a name="introduction-to-receive-side-scaling"></a>接收端缩放简介

接收方缩放 (RSS) 是一种网络驱动程序技术，可用于在多处理器系统中跨多个 Cpu 高效地分发网络接收处理。

> [!NOTE]
> 由于同一核心处理器上的超线程 Cpu 共享同一执行引擎，因此效果不同于拥有多个核心处理器。 出于此原因，RSS 不使用超线程处理器。

为了有效处理接收的数据，微型端口驱动程序的接收中断服务函数将 (DPC) 计划延迟的过程调用。 如果没有 RSS，则典型 DPC 会指示 DPC 调用中接收的所有数据。 因此，与中断关联的所有接收处理都在发生接收中断的 CPU 上运行。 有关非 RSS 接收处理的概述，请参阅 [非 Rss 接收处理](non-rss-receive-processing.md)。

利用 RSS，NIC 和微型端口驱动程序提供了在其他处理器上安排接收 Dpc 的能力。 此外，RSS 设计可确保与给定连接关联的处理保持在已分配的 CPU 上。 NIC 实现哈希函数，结果哈希值提供了选择 CPU 的方法。

下图说明了用于确定 CPU 的 RSS 机制。

![说明用于确定 cpu 的 rss 机制的关系图](images/rss.png)

NIC 使用哈希函数来计算所接收的网络数据中 (哈希类型) 定义的区域的哈希值。 定义的区域可能是不连续的。

 (LSBs) 哈希值的最小有效位用于为间接寻址表编制索引。 间接表中的值用于将接收的数据分配给 CPU。

有关指定间接表、哈希类型和哈希函数的更多详细信息，请参阅 [RSS 配置](rss-configuration.md)。

使用消息信号中断 (MSI) 支持，NIC 还可以中断关联的 CPU。 有关 NDIS 对 Msi 的支持的详细信息，请参阅 [NDIS MSI-X](ndis-msi-x.md)。

## <a name="hardware-support-for-rss"></a>RSS 的硬件支持

下图说明了 RSS 的硬件支持级别。

![说明 rss 硬件支持级别的示意图](images/rss-hw.png)

对于 RSS，有三种可能的硬件支持级别：

<a href="" id="hash-calculation-with-a-single-queue"></a>使用单个队列进行哈希计算  
NIC 计算哈希值，微型端口驱动程序将接收的数据包分配给与 Cpu 关联的队列。 有关详细信息，请参阅 [使用单个硬件接收队列的 RSS](rss-with-a-single-hardware-receive-queue.md)。

<a href="" id="hash-calculation-with-multiple-receive-queues"></a>具有多个接收队列的哈希计算  
NIC 将接收的数据缓冲区分配给与 Cpu 关联的队列。 有关详细信息，请参阅 [包含硬件队列的 RSS](rss-with-hardware-queuing.md)。

<a href="" id="message-signaled-interrupts--msis-"></a>消息已发出信号中断 (Msi)   
NIC 将中断应处理所接收数据包的 CPU。 有关详细信息，请参阅 [具有消息信号中断的 RSS](rss-with-message-signaled-interrupts.md)。

NIC 始终传递32位哈希值。

## <a name="how-rss-improves-system-performance"></a>RSS 如何提高系统性能

RSS 可通过减少以下内容提高网络系统性能：

-   通过跨多个 Cpu 跨 NIC 分发接收处理来处理延迟。

    这有助于确保在另一个 CPU 处于空闲状态时，CPU 负载不大。

-   通过提高在同一 CPU 上执行共享数据的软件算法的概率来旋转锁开销。

    例如，在 CPU0 上执行的函数拥有对 CPU1 上运行的函数必须访问的数据的自旋锁时，会发生自旋锁开销。 CPU1 旋转 (等待) ，直到 CPU0 释放该锁。

-   通过提高共享数据的软件算法在同一 CPU 上执行的概率，重新加载缓存和其他资源。

    例如，在执行和访问 CPU0 上的共享数据的函数时，将在后续中断中的 CPU1 上执行。

若要在安全的环境中实现这些性能改进，RSS 提供了以下机制：

-   分布式处理

    RSS 将来自 Dpc 中给定 NIC 的接收指示处理分散到多个 Cpu。

-   按序处理

    RSS 保留接收的数据包的传递顺序。 对于每个网络连接，RSS 会处理关联 CPU 上的指示。 有关 RSS 接收处理的详细信息，请参阅 [指示 Rss 接收数据](indicating-rss-receive-data.md)。

-   动态负载均衡

    RSS 提供一种方法，用于在主机系统负载变化时重新平衡 Cpu 之间的网络处理负载。 为了重新平衡负载，过量驱动程序可以更改间接寻址表。 有关指定间接表、哈希类型和哈希函数的详细信息，请参阅 [RSS 配置](rss-configuration.md)。

-   发送方缩放

    使用 RSS，驱动程序堆栈可以处理同一 CPU 上给定连接的发送和接收端数据。 通常情况下，过量的驱动程序 (例如，TCP) 发送部分数据块，并在发送数据的平衡之前等待确认。 然后，确认触发后续发送请求。 RSS 间接寻址表标识用于接收数据处理的特定 CPU。 默认情况下，如果发送处理触发接收确认，则发送处理在同一 CPU 上运行。 例如，如果) 使用计时器，驱动程序还可以指定 CPU (。

-   安全哈希

    RSS 包含提供额外安全性的签名。 此签名可防止系统受到恶意远程主机的攻击，这些主机可能会尝试强制系统进入不平衡状态。

-   支持 MSI X

    RSS （支持 MSI X）在稍后执行 DPC 的同一 CPU 上 (ISR) 运行中断服务例程。 这样可以减少缓存的旋转锁定开销和重新加载。
 

 






---
title: 数据包合并概述
description: 数据包合并概述
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b535c5552e0a3a448976317c209a02310821faef
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801331"
---
# <a name="overview-of-packet-coalescing"></a>数据包合并概述


某些 IP 版本 4 (IPv4) 和 IP 版本 6 (IPv6) 网络协议涉及将数据包传输到广播或多播地址。 这些数据包由 IPv4/IPv6 子网中的多个主机接收。 在大多数情况下，接收这些数据包的主机不会对这些数据包执行任何操作。 因此，接收到这些不需要的多播或广播数据包会导致不必要的处理和电源消耗发生在接收主机内。

例如，主机 A 向 IPv6 子网上的 LLMNR) 请求发送多播链路本地多播名称解析 (，以解析主机 B 的名称。 除了主机 A 之外，子网中的所有主机都将接收此 LLMNR 请求。 除了主机 B 以外，在其他主机上运行的 TCP/IP 协议堆栈会检查数据包，并确定数据包并非适用于该数据包。 因此，协议堆栈拒绝数据包，并调用 [**NdisReturnNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreturnnetbufferlists) 将数据包返回给微型端口驱动程序。

从 NDIS 6.30 开始，网络适配器可支持 NDIS 数据包合并。 通过对随机广播或多播数据包的合并减少接收中断数，系统上的处理开销和功率消耗明显降低。

数据包合并包括以下步骤：

1.  过量驱动程序，如 TCP/IP 协议堆栈，定义用于屏幕广播和多播数据包的 NDIS 接收筛选器。 过量驱动程序将这些筛选器下载到支持数据包合并的底层微型端口驱动程序。 下载后，微型端口驱动程序将网络适配器配置为具有数据包合并接收筛选器。

    有关这些筛选器的详细信息，请参阅 [数据包合并接收筛选器](packet-coalescing-receive-filters.md)。

2.  在网络适配器上缓存或 *合并* 与接收筛选器匹配的接收数据包。 适配器不会为合并的数据包生成接收中断。 而是在另一个硬件事件发生时，适配器将中断主机。

    生成此中断后，适配器必须指示带有中断的接收事件。 这允许网络适配器处理网络适配器接收的合并的数据包。

    例如，支持数据包合并的网络适配器可以在发生以下事件之一时生成接收中断：

    -   过期时间设置为匹配接收筛选器的最大合并延迟值的硬件计时器的过期时间。

    -   硬件合并缓冲区中的可用空间达到适配器指定的低水位线。

    -   接收的数据包与合并筛选器不匹配。

    -   发生了另一个中断事件，如发送完成事件。

    有关此过程的详细信息，请参阅 [处理包合并接收筛选器](handling-packet-coalescing-receive-filters.md)。

以下几点适用于由 NDIS 支持数据包合并：

-   NDIS 支持 (端口 0) 分配给物理网络适配器的默认 NDIS 端口接收数据包合并。 NDIS 不支持分配给虚拟网络适配器的 NDIS 端口上的数据包合并。 有关详细信息，请参阅 [NDIS 端口](overview-of-ndis-ports.md)。

-   对于在网络适配器默认接收队列中接收的数据包，NDIS 支持数据包合并。 此接收队列具有 NDIS \_ 默认 \_ 接收 \_ 队列 ID 的标识符 \_ 。

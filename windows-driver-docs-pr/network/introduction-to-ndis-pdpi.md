---
title: NDIS PacketDirect 提供程序接口简介
description: '本部分介绍了 NDIS PacketDirect 提供程序接口 (PDPI) '
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c8e98f55af38ba00eeaa203c18a271a55de62182
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820099"
---
# <a name="introduction-to-the-ndis-packetdirect-provider-interface"></a>NDIS PacketDirect 提供程序接口简介


PacketDirect 提供程序接口 (PDPI) 使用加速的 i/o 模型（适用于物理环境和虚拟环境）扩展 NDIS，这会增加每秒处理的数据包数的数量级，并大大降低抖动（与传统 NDIS i/o 路径相比）。

## <a name="background"></a>背景


Windows 中的传统 i/o 模式实现为多用途，一般 i/o 平台旨在使用多种不同的媒体类型，其中的网络只是整个系统的一个方面。 如今，由于网络虚拟化在数据中心成为一种普遍的技术，Windows Server 操作系统中的传统 NDIS i/o 模型不仅足以满足网络密集型工作负荷，而这些工作负载预计会变得越来越常见，但也不能将资源专门用于网络 i/o 处理。 在数据中心环境中，实施专用于网络的单一用途计算机通常是为硬件设备预留的功能，这种情况并不常见。 这些网络设备的示例包括软件负载平衡器、DDoS 设备和转发网关。 更糟的是，在其他操作系统上可以通过一些机制来加速 i/o，使这些替代 OS 成为构建网络密集型应用程序（例如虚拟设备）的首选平台。

PacketDirect (PD) 使用每秒针对数据包进行了优化的加速网络 i/o 路径扩展了当前 NDIS 模型， (pps) 计算比传统 NDIS i/o 模型更高的量的顺序。 完成此操作的步骤如下：

-   减少延迟
-   缩短循环/数据包
-   线性加速，使用其他系统资源

PacketDirect 与传统模型并存。 当应用程序优先使用新的 PD 路径并且有足够的硬件资源来容纳该路径时，可以使用该路径。 PD 不打算替换传统的 i/o 模型，假设向 PD 接口写入的客户端将对基于系统拓扑的基础资源具有严格的分区要求。 PD 旨在作为新的高速数据路径，该路径将帮助 Windows 系统替换在传统上在硬件中完成的高 pps 工作负载，从而使数据中心所有者数百万于基础结构成本。

## <a name="packetdirect-concepts"></a>PacketDirect 概念


PD 通过允许 PD 客户端使用 (NIC) 从网络适配器显式管理网络流量。 PD 通过 PackageDirect 客户端接口 (PDCI) 为 PD 客户端提供 NIC 的高性能发送和接收功能。 在内部，PDCI 发送/接收函数会直接映射到 PDPI。 PD 发送/接收函数对由 pd 支持的 Nic 上的 pd 客户端创建的 PD 队列进行操作。 PD 为 PD 客户端提供根据 PD 客户端的需求为非常特定的通信类型或非常通用的流量设置自定义筛选器的功能。 这允许 PD 客户端将某些传入数据包定向到其 PD 队列。 PD 模型中的数据包处理始终发生在由 PD 客户端拥有 (或受控/协调) 的执行上下文中。 支持 PD 的 NIC 驱动程序完全是被动的，这意味着它不会在驱动程序拥有的执行上下文（如 DPC 或工作线程）中主动将传入数据包或完成指示发送到 PD 客户端。

如果 PD 客户端不了解如何处理数据包或接收其某个队列（如 ARP、LLDP 或其他协议数据包）中的控制数据包，则 PD 客户端可以将数据包重新路由回当前 i/o 路径进行处理。 这允许 PD 继续处理其具有上下文的数据包，而不会浪费控制流量的循环。

**重要提示**  每个网络适配器可以有一个 PD 提供程序和一个 PD 客户端。 因此，一个系统中可以有多个 PD 客户端和 PD 提供程序。

 

PD 客户端可以控制在系统中分配给 PD 的资源。 在网络流量较高的情况下，PD 客户端负责将其工作负荷降到最低，以便操作系统能够响应其他工作负荷。

Windows 实现的 PacketDirect 平台将客户端接口映射到提供程序接口。 平台控制缓冲区管理并能够将通过 PD 接收的数据包重新注入到当前的 NDIS 接收路径。 它还处理与 PD 客户端的交互，以满足 NDIS 控制路径要求，如 NIC 禁用、进入低能耗、系统关闭和意外删除，而不会妨碍 PD 数据路径性能。

**PacketDirect 提供程序接口 (PDPI)**

PDPI 允许 NIC 驱动程序向 Windows OS 公开其高性能发送和接收功能。 实现的函数是完整微型端口功能的子集，并且对于实现 PD 的所有 Nic 都是通用的。 有关 PDPI 的参考文档，请参阅 [PacketDirect Provider Interface (PDPI) reference](/windows-hardware/drivers/ddi/_netvista/)。

**PacketDirect Client Interface (PDCI)**

PDCI 允许第一方 Windows 服务/应用程序 (例如，负载平衡器、NAT、VM 交换机等 ) 通过使用 PD 客户端通过使用 PacketDirect i/o 模型来加速其数据路径。 此接口是第2层接口，与当前 NDIS 发送/接收接口相同。 主要功能 PDCI 除了提供 PDPI) access 外，还提供 (，它还提供了 PD 数据包缓冲区分配/管理、用于将数据包注入到常规 NDIS 接收路径的后通道，以及对 NDIS 电源/PnP 事件的处理。

## <a name="related-topics"></a>相关主题


[PacketDirect Provider Interface (PDPI) Reference](/windows-hardware/drivers/ddi/_netvista/)

 


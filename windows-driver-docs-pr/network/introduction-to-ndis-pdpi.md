---
title: NDIS PacketDirect 提供程序界面简介
description: 本部分介绍到 NDIS PacketDirect 提供程序接口 (PDPI)
ms.assetid: E85ED51E-BDE5-43BE-93BA-19F214670B8F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca37eb13e3ef06867136802fbe44d5a7c1d74270
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343653"
---
# <a name="introduction-to-the-ndis-packetdirect-provider-interface"></a>NDIS PacketDirect 提供程序界面简介


PacketDirect 提供程序接口 (PDPI) 使用的物理和虚拟环境，可以增加每秒处理一个数量级的数据包数，并显著减少抖动一个加速的 I/O 模型扩展 NDIS 时与传统的 NDIS I/O 路径进行比较。

## <a name="background"></a>后台


在 Windows 中传统的 I/O 模型实施到原来是为了使用具有许多不同的特征的多个媒体类型的多用途、 常规 I/O 平台和在网络是整个系统的仅一个方面。 现在，如网络虚拟化已经成为一种流行技术在数据中心，Windows Server 操作系统中的传统 NDIS I/O 模型不是仅不不足，无法跟上我们预计会变得越来越常见的网络密集型工作负荷，但还若要将资源专用于网络 I/O 处理不适合模型。 在数据中心环境中，不常见实现专用于网络执行了通常预留给硬件设备的函数的单一用途机。 这些网络设备的示例包括软件负载均衡器、 DDoS 设备和转发网关。 更糟糕的是，有其他操作系统上的加速 I/O，使这些其他操作系统的生成如虚拟设备的网络密集型应用程序的首选的平台的方式。

PacketDirect (PD) 扩展了当前 NDIS 模型适用于每个比什么更高版本将量值顺序中出现了传统的 NDIS I/O 模型的第二个 (pps) 计数的数据包的加速的网络 I/O 路径。 这是通过实现的：

-   减少的延迟
-   减少的周期数据包
-   线性加速与其他系统资源的使用

PacketDirect 存在的传统模型并行。 当应用程序时首选它并且有足够的硬件资源，以容纳它时，可以使用新的 PD 路径。 PD 并不旨在取代传统的 I/O 模型，并假定写入 PD 接口的客户端将具有针对基于系统拓扑的基础资源的严格分区要求。 PD 要作为新的高速数据路径有助于 Windows 系统将为高 pps 工作负荷的传统上完成硬件、 节省数据中心所有者数以百万计的基础结构成本。

## <a name="packetdirect-concepts"></a>PacketDirect 概念


PD 工作原理是使 PD 客户端来显式管理网络流量从网络适配器 (NIC)。 PD 提供高性能发送 PD 客户端控件，并接收 PackageDirect 客户端接口 (PDCI) 通过 NIC 功能。 在内部，PDCI 发送/接收函数直接向 PDPI 映射。 PD 发送/接收函数对 PD PD 客户端支持 PD 的 Nic 上创建的队列。 PD 向 PD 客户端提供设置为非常具体类型的流量或非常通用的流量，根据需求 PD 客户端的自定义筛选器的功能。 这允许将某些传入数据包发送到其 PD 队列 PD 客户端。 始终处理 PD 模型中的数据包会执行 PD 客户端拥有的执行上下文中的位置 （或控制/协调）。 PD 支持的 NIC 驱动程序是完全被动，这意味着它不主动转发传入数据包或完成指示已发送的数据包到如 DPC 或工作线程的驱动程序负责执行上下文中的 PD 客户端。

如果 PD 客户端不知道如何处理数据包或如 ARP、 LLDP 或其他协议的数据包，其队列之一接收控制数据包 PD 客户端可以重新路由到当前的 I/O 路径进行处理的数据包。 这允许 PD 可以继续处理具有上下文的数据包，并不会控制流量上浪费周期。

**重要**  可以有一个 PD 提供程序和每个网络适配器的一个 PD 客户端。 因此，可以有多个 PD 客户端和 PD 在单个系统上的提供程序。

 

PD 客户端可以控制分配给 PD 系统中的资源。 在的网络流量很高的情况下，PD 客户端负责将其工作负荷降至最低，以便操作系统可以对其他工作负荷的响应能力。

由 Windows 实现的 PacketDirect 平台将客户端接口映射到提供程序接口。 平台控件缓冲区管理和能够重新插入到当前的 NDIS PD 通过接收的数据包接收路径。 它还处理交互与 PD 满足 NDIS 的客户端控制进入低功耗，系统关闭，例如 NIC 禁用，路径要求和感到惊讶不妨碍 PD 数据路径性能的方式删除。

**PacketDirect 提供程序接口 (PDPI)**

PDPI 允许 NIC 驱动程序来公开其高性能发送和接收的 Windows 操作系统的功能。 实现的函数是完整的微型端口功能的子集，并且是通用的实现 PD 的所有 Nic。 PDPI 的参考文档，请参阅[PacketDirect 提供程序接口 (PDPI) 引用](https://msdn.microsoft.com/library/windows/hardware/dn931858)。

**PacketDirect 客户端接口 (PDCI)**

PDCI 允许第一方 Windows 服务/应用程序 （例如，负载均衡器、 NAT、 VM 交换机等） 来通过利用 PacketDirect I/O 模型通过 PD 客户端使用其数据路径提高速度。 此接口是一样的当前 NDIS 发送/接收接口的第 2 层接口。 PDCI （除了 PDPI 访问） 提供的主要功能是 PD 数据包缓冲区分配/管理，用于插入数据包返回到正常的后通道 NDIS 接收路径、 NDIS power/PnP 事件的处理。

## <a name="related-topics"></a>相关主题


[PacketDirect 提供程序接口 (PDPI) 参考](https://msdn.microsoft.com/library/windows/hardware/dn931858)

 

 







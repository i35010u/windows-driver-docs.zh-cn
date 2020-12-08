---
title: 在网络驱动程序设计指南中导航
description: 在网络驱动程序设计指南中导航
keywords:
- 网络驱动程序 WDK，文档
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 65fef66bd89cf47fc828352e32d6d49015c7fbd3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837649"
---
# <a name="navigating-the-network-driver-design-guide"></a>在网络驱动程序设计指南中导航





基于 Microsoft Windows 的操作系统支持多种类型的内核模式网络驱动程序。 Windows 驱动程序工具包 (WDK) 文档的网络部分介绍了如何编写这些网络驱动程序。 本主题简要介绍了支持的网络驱动程序类型，并说明了在写入每种类型的网络驱动程序之前应阅读的网络部分。

此网络驱动程序设计指南记录以下网络驱动程序接口规范 (NDIS) 接口：

-   在 Windows 8.1、Windows Server 2012 R2 和更高版本的 Windows 上支持的 NDIS 6.40。 NDIS 6.30 支持 (NDKPI) 1.12 的网络直接内核提供程序接口。

    有关 NDIS 6.30 的详细信息，请参阅 [ndis 6.40 简介](introduction-to-ndis-6-40.md)。

-   NDIS 6.30，在 Windows 8、Windows Server 2012 和更高版本的 Windows 上受支持。 NDIS 6.30 包括对单个根/i/o 虚拟化的支持 (SR-IOV) 、Hyper-v 可扩展交换机、网络直接内核提供程序接口 (NDKPI) 1.1 和其他服务。

    有关 NDIS 6.30 的详细信息，请参阅 [ndis 6.30 简介](introduction-to-ndis-6-30.md)。

-   NDIS 6.20，在 windows 7、Windows Server 2008 R2 和更高版本的 Windows 上受支持。 NDIS 6.20 包括对虚拟机队列 (VMQ) 、接收端限制和其他服务的支持。

    有关 NDIS 6.20 的详细信息，请参阅 [ndis 6.20 简介](introduction-to-ndis-6-20.md)。

-   在 Windows Vista Service Pack 1 (SP1) 、Windows Server 2008 和更高版本的 Windows 上支持 NDIS 6.1。 NDIS 6.1 包括对标头数据拆分、直接 OID 请求和其他服务的支持。

    有关 NDIS 6.1 的详细信息，请参阅 [ndis 6.1 简介](introduction-to-ndis-6-1.md)。

-   NDIS 6.0，在 Windows Vista 和更高版本的 Windows 上受支持。 NDIS 6.0 包括对筛选器驱动程序的支持，以及以前的 NDIS 版本未提供的许多其他服务。 NDIS 6.0 包括对驱动程序初始化和网络数据管理的重要更新，其中包括在运行时对驱动程序重新配置所需的支持和用于处理网络数据包数据的 [**NET \_ BUFFER**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer) 体系结构。 有关支持运行时重新配置的详细信息，请参阅 [驱动程序堆栈管理](driver-stack-management.md)。 有关如何在 NDIS 6.0 中处理网络数据包数据的详细信息，请参阅 [NET \_ BUFFER 体系结构](net-buffer-architecture.md)。

    有关 NDIS 6.0 的详细信息，请参阅 [ndis 6.0 简介](introduction-to-ndis-6-0.md)。

Windows Vista 和更高版本的操作系统版本支持以下类型的基于 NDIS 的内核模式的网络驱动程序：

<a href="" id="miniport-drivers"></a>[微型端口驱动程序](learning-about-miniport-drivers.md)  
*微型端口驱动程序* 管理微型端口适配器，并为高级驱动程序的适配器提供接口。 *小型端口适配器* 是一种概念实体，可以表示物理设备或虚拟设备。 例如，微型端口适配器可以表示网络接口卡 (NIC) 或与中间驱动程序相关联的虚拟设备。

微型端口驱动程序有很多变化，如 *面向连接的微型端口调用管理器 (MCM) 、* *Windows 驱动模型 (WDM) 微型端口驱动程序* 和中间驱动程序的上边缘。

<a href="" id="protocol-drivers"></a>[协议驱动程序](learning-about-protocol-drivers.md)  
*协议驱动程序* 在驱动程序堆栈中提供高级服务。 协议驱动程序绑定到基础微型端口适配器。 *上层协议驱动程序* 在其上部边缘实现一个接口，可能是特定于应用程序的接口，为网络用户提供服务。 在其下边缘，协议驱动程序提供了一个协议接口，用于将网络数据传递到下一个较低版本的驱动程序并从中接收传入的数据。

协议驱动程序有很多变化，如 *面向连接的呼叫管理器 (MCM) 、面向连接的客户端* 以及中间驱动程序的下边缘。

<a href="" id="filter-drivers"></a>[筛选器驱动程序](learning-about-filter-drivers.md)  
*筛选器驱动* 程序对协议驱动程序和微型端口驱动程序之间的接口的信息进行筛选。 *筛选器模块* 附加在协议驱动程序和微型端口适配器之间的绑定中，对于其他驱动程序通常是透明的。 筛选器驱动程序可以实现 *修改或监视筛选器*。 例如，筛选器驱动程序可以增强基础微型端口适配器提供的服务或仅仅收集统计信息。

<a href="" id="intermediate-drivers"></a>[中间驱动程序](learning-about-intermediate-drivers.md)  
上层协议驱动程序和微型端口驱动程序之间的 *中间驱动程序* 接口。 中间驱动程序在其上部边缘提供微型端口驱动程序接口，以绑定到过量协议驱动程序。 中间驱动程序在其下边缘提供一个协议驱动程序接口，用于绑定到底层微型端口适配器。 中间驱动程序通常用于实现 *n* 到 *m* 个多路复用器服务。 例如，中间驱动程序可以实现负载平衡和故障转移解决方案。

中间驱动程序还可以在将硬件配置为 *微型端口中间驱动程序* 时对其进行管理。

有关 Windows 网络体系结构和编程注意事项的详细信息，请参阅 [用于 Kernel-Mode 驱动程序的网络体系结构](windows-network-architecture-and-the-osi-model.md) 和 [网络驱动程序编程注意事项](network-driver-programming-considerations.md)。

有关用于安装网络组件的网络 INF 文件的详细信息，请参阅 [安装网络组件](installing-network-components.md)。 如果网络驱动程序需要通知对象（例如，为了控制绑定），请参阅 [通知对象获取网络组件](notify-objects-for-network-components.md)。

可以使用以下附加的驱动程序模型来使用特定的硬件技术和体系结构。

<table>  
<colgroup> <col width="50%" /> <col width="50%" /> </colgroup>  
<thead>  
<tr class="header">  
<th align="left">技术</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/_netvista/" data-raw-source="[Scalable Networking](/windows-hardware/drivers/ddi/_netvista/)">可缩放网络</a></p></td>
<td align="left"><p>支持将任务卸载到网络适配器的网络技术，如下所示：</p>
<ul>
<li><p><a href="header-data-split.md" data-raw-source="[Header-Data Split](header-data-split.md)">标头-数据拆分</a>，一种服务，它将接收的以太网帧中的标头和数据拆分为单独的缓冲区。</p></li>
<li><p><a href="/windows-hardware/drivers/network/receive-side-scaling-version-2-rssv2-" data-raw-source="[Receive Side Scaling](./receive-side-scaling-version-2-rssv2-.md)">接收方缩放</a>，一种网络驱动程序技术，可提高多处理器系统的网络性能。</p></li>
<li><p><a href="/previous-versions/windows/hardware/network/ndis-tcp-chimney-offload" data-raw-source="[TCP Chimney Offload](/previous-versions/windows/hardware/network/ndis-tcp-chimney-offload)">Tcp 烟囱卸载</a>，将 tcp 协议处理的数据传输部分卸载到具有适当功能的网络适配器。</p></li>
<li><p><a href="tcp-ip-offload.md" data-raw-source="[TCP/IP Offload](tcp-ip-offload.md)">Tcp/ip 卸载</a>、任务或与具有适当功能的网络适配器的连接。</p></li>
<li><p><a href="overview-of-network-direct-kernel-provider-interface--ndkpi-.md" data-raw-source="[Network Direct Kernel Provider Interface (NDKPI)](overview-of-network-direct-kernel-provider-interface--ndkpi-.md)">网络直接内核提供程序接口 (NDKPI) </a>，这使得内核模式 Windows 组件（如 SMB 服务器和客户端）可以使用远程直接内存访问 (RDMA) 功能，这些功能由独立硬件供应商 (ihv) 提供。</p></li>
<li><p><a href="network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload.md" data-raw-source="[Network Virtualization using Generic Routing Encapsulation (NVGRE) Task Offload](network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload.md)">使用通用路由封装的网络虚拟化 (NVGRE) 任务卸载</a>，这使得可以使用通用路由封装 (GRE) 封装的数据包：</p>
<ul>
<li>大量发送卸载 (LSO)</li>
<li>虚拟机队列 (VMQ)</li>
<li>传输 (Tx) 校验和卸载</li>
<li>接收 (Rx) 校验和卸载</li>
</ul></li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p><a href="virtualized-networking.md" data-raw-source="[Virtualized Networking](virtualized-networking.md)">虚拟化网络</a></p></td>
<td align="left"><p>支持 Hyper-v 虚拟化环境的网络技术，如下所示：</p>
<ul>
<li><p><a href="single-root-i-o-virtualization--sr-iov-.md" data-raw-source="[Single Root I/O Virtualization (SR-IOV)](single-root-i-o-virtualization--sr-iov-.md)">单根 I/O 虚拟化 (SR-IOV)</a></p></li>
<li><p><a href="virtual-machine-queue--vmq--in-ndis-6-20.md" data-raw-source="[Virtual Machine Queue (VMQ)](virtual-machine-queue--vmq--in-ndis-6-20.md)">虚拟机队列 (VMQ)</a></p></li>
<li><p><a href="hyper-v-extensible-switch.md" data-raw-source="[Hyper-V Extensible Switch](hyper-v-extensible-switch.md)">Hyper-V 可扩展交换机</a></p></li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/_netvista/" data-raw-source="[Wireless Networking](/windows-hardware/drivers/ddi/_netvista/)">无线联网</a></p></td>
<td align="left"><p>包含本机802.11 无线 LAN 的网络功能。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/_netvista/" data-raw-source="[Network Module Registrar](/windows-hardware/drivers/ddi/_netvista/)">网络模块注册机构</a></p></td>
<td align="left"><p>允许驱动程序将网络模块相互连接的系统设备。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/_netvista/" data-raw-source="[Winsock Kernel](/windows-hardware/drivers/ddi/_netvista/)">Winsock 内核</a></p></td>
<td align="left"><p> (NPI) 的内核模式网络编程接口。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ip-helper.md" data-raw-source="[IP Helper](ip-helper.md)">IP 帮助程序</a></p></td>
<td align="left"><p>一组实用函数，使驱动程序可以检索和修改有关本地计算机的网络配置的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="windows-filtering-platform-callout-drivers2.md" data-raw-source="[Windows Filtering Platform Callout Drivers](windows-filtering-platform-callout-drivers2.md)">Windows 筛选平台标注驱动程序</a></p></td>
<td align="left"><p>一种提供深层检查、数据包修改、流修改和网络数据记录的内核模式接口。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="system-area-networks.md" data-raw-source="[System Area Networks](system-area-networks.md)">系统区域网络</a></p></td>
<td align="left"><p>一种网络连接，该连接使用 Windows Socket Direct 来支持高性能、面向连接的网络。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/previous-versions/ff570659(v=vs.85)" data-raw-source="[Remote NDIS (RNDIS)](/previous-versions/ff570659(v=vs.85))">远程 NDIS (RNDIS)</a></p></td>
<td align="left"><p>一种类规范，用于定义与系统提供的、与总线无关的、通过 USB 总线设置的消息集。</p></td>
</tr>
</tbody>
</table>

 


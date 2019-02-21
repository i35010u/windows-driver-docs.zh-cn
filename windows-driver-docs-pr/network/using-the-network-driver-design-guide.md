---
title: 使用网络驱动程序设计指南
description: 使用网络驱动程序设计指南
ms.assetid: 8d9cbf3c-5eec-4409-ab4c-595bb921832d
keywords:
- 网络驱动程序 WDK，文档
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2b2bf7c48a9efaee8b1dd3117ab1d791cfdeb83f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520781"
---
# <a name="using-the-network-driver-design-guide"></a>使用网络驱动程序设计指南





Microsoft 基于 Windows 的操作系统支持多种类型的内核模式网络驱动程序。 Windows Driver Kit (WDK) 文档的网络部分介绍如何编写这些网络驱动程序。 本主题简要描述了受支持的类型的网络驱动程序，并介绍了在编写每种类型的网络驱动程序之前应阅读的网络部分的哪些部分。

此网络驱动程序设计指南介绍以下网络驱动程序接口规范 (NDIS) 接口：

-   NDIS 6.40 支持 Windows 8.1、 Windows Server 2012 R2 和更高版本的 Windows。 NDIS 6.30 包括支持的网络直接内核提供程序接口 (NDKPI) 1.12。

    有关 NDIS 6.30 详细信息，请参阅[简介 NDIS 6.40](introduction-to-ndis-6-40.md)。

-   NDIS 6.30，Windows 8、 Windows Server 2012 和更高版本的 Windows 受支持。 NDIS 6.30 包括支持单根 / / O 虚拟化 (SR-IOV)、 HYPER-V 可扩展交换机、 网络直接内核提供程序接口 (NDKPI) 1.1 版中和其他服务。

    有关 NDIS 6.30 详细信息，请参阅[简介 NDIS 6.30](introduction-to-ndis-6-30.md)。

-   NDIS 6.20，在 Windows 7、 Windows Server 2008 R2 和更高版本的 Windows 受支持。 NDIS 6.20 包括支持的虚拟机队列 (VMQ)、 接收端限制和其他服务。

    有关 NDIS 6.20 的详细信息，请参阅[简介 NDIS 6.20](introduction-to-ndis-6-20.md)。

-   NDIS 6.1，Windows Vista Service Pack 1 (SP1)、 Windows Server 2008 和更高版本的 Windows 受支持。 NDIS 6.1 包括对标头数据拆分、 直接的 OID 请求和其他服务的支持。

    有关 NDIS 6.1 的详细信息，请参阅[简介 NDIS 6.1](introduction-to-ndis-6-1.md)。

-   NDIS 6.0 中，这在 Windows Vista 和更高版本的 Windows 上受支持。 NDIS 6.0 包括对筛选器驱动程序和支持早期 NDIS 版本未提供的许多其他服务。 NDIS 6.0 提供了对驱动程序初始化和网络数据管理，包括所需的驱动程序重新配置在运行时支持的重大更新和[ **NET\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff568376)用于处理网络数据包数据体系结构。 支持运行时重新配置的详细信息，请参阅[驱动程序堆栈管理](driver-stack-management.md)。 有关如何处理在 NDIS 6.0 中的网络数据包数据的详细信息请参阅[NET\_缓冲体系结构](net-buffer-architecture.md)。

    NDIS 6.0 的详细信息，请参阅[简介 NDIS 6.0](introduction-to-ndis-6-0.md)。

Windows Vista 和更高版本的操作系统版本支持以下类型的内核模式下基于 NDIS 网络驱动程序：

<a href="" id="miniport-drivers"></a>[微型端口驱动程序](learning-about-miniport-drivers.md)  
一个*微型端口驱动程序*管理微型端口适配器并提供给适配器用于更高级别的驱动程序的接口。 一个*微型端口适配器*为概念实体可以表示物理设备或虚拟设备。 例如，微型端口适配器可以表示网络接口卡 (NIC) 或与中间的驱动程序相关联的虚拟设备。

有许多变体微型端口驱动程序，如*面向连接的微型端口呼叫管理器 (MCM)、* *Windows 驱动程序模型 (WDM) 微型端口驱动程序，* 和中间驱动程序的上边缘。

<a href="" id="protocol-drivers"></a>[协议驱动程序](learning-about-protocol-drivers.md)  
一个*协议驱动程序*提供驱动程序堆栈中的高级别服务。 协议驱动程序将绑定到基础微型端口适配器。 *较高级别协议驱动程序*实现接口时，可能是特定于应用程序的接口，在其上边缘为网络中的用户提供服务。 在其下边缘，协议驱动程序提供了一个协议接口用于传递到的网络数据和接收来自较低的下一步驱动程序传入数据。

有许多变体协议驱动程序，如*面向连接的呼叫管理器 (MCM)、 面向连接的客户端，* 和中间驱动程序的下边缘。

<a href="" id="filter-drivers"></a>[筛选器驱动程序](learning-about-filter-drivers.md)  
一个*筛选器驱动程序*筛选协议驱动程序和微型端口驱动程序之间的接口的信息。 *筛选器模块*协议驱动程序和微型端口适配器之间的绑定中附加和通常对是透明的其他驱动程序。 筛选器驱动程序可以实现*修改或监视筛选器*。 例如，筛选器驱动程序可以增强基础的微型端口适配器提供的服务或只需收集统计信息。

<a href="" id="intermediate-drivers"></a>[中间驱动程序](learning-about-intermediate-drivers.md)  
*中间驱动程序*较高级别协议驱动程序和微型端口驱动程序之间的接口。 中间驱动程序提供在其上边缘要绑定到过量协议驱动程序微型端口驱动程序接口。 中间驱动程序提供在其下边缘要绑定到基础微型端口适配器协议驱动程序接口。 中间驱动程序通常用于实现*n*到*m*多路复用器服务。 例如，中间驱动程序可以实现负载平衡和故障转移解决方案。

它们被配置为时，中间驱动程序还可以管理硬件*中间微型端口驱动程序*。

详细了解 Windows 网络体系结构和编程注意事项，请参见[内核模式驱动程序的网络体系结构](network-architecture-for-kernel-mode-drivers.md)并[网络驱动程序编程注意事项](network-driver-programming-considerations.md)。

详细了解网络 INF 文件，这用于安装网络组件，请参阅[安装网络组件](installing-network-components.md)。 如果您的网络驱动程序需要通知对象-例如，若要控制绑定-还请参阅[通知网络组件的对象](notify-objects-for-network-components.md)。

以下的其他驱动程序模型都可以使用特定的硬件技术和体系结构。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">技术</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570735" data-raw-source="[Scalable Networking](https://msdn.microsoft.com/library/windows/hardware/ff570735)">可伸缩网络</a></p></td>
<td align="left"><p>支持的网络适配器，如下所示的任务卸载的网络技术：</p>
<ul>
<li><p><a href="header-data-split.md" data-raw-source="[Header-Data Split](header-data-split.md)">标头数据拆分</a>，将拆分标头和中的数据的服务接收到单独的缓冲区的以太网帧。</p></li>
<li><p><a href="ndis-receive-side-scaling2.md" data-raw-source="[Receive Side Scaling](ndis-receive-side-scaling2.md)">接收方缩放</a>，可以提高网络性能多处理器系统上的网络驱动程序技术。</p></li>
<li><p><a href="ndis-tcp-chimney-offload.md" data-raw-source="[TCP Chimney Offload](https://docs.microsoft.com/previous-versions/windows/hardware/network/ndis-tcp-chimney-offload)">TCP 烟囱卸载</a>，卸载到具有相应功能的网络适配器处理的 TCP 协议的数据传输部分。</p></li>
<li><p><a href="tcp-ip-offload.md" data-raw-source="[TCP/IP Offload](tcp-ip-offload.md)">卸载 TCP/IP</a>，任务或连接到具有相应功能的网络适配器的卸载。</p></li>
<li><p><a href="overview-of-network-direct-kernel-provider-interface--ndkpi-.md" data-raw-source="[Network Direct Kernel Provider Interface (NDKPI)](overview-of-network-direct-kernel-provider-interface--ndkpi-.md)">网络直接内核提供程序接口 (NDKPI)</a>，使内核模式 Windows 组件，例如 SMB 服务器和客户端，若要使用独立硬件供应商 (Ihv) 提供的远程直接内存访问 (RDMA) 功能。</p></li>
<li><p><a href="network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload.md" data-raw-source="[Network Virtualization using Generic Routing Encapsulation (NVGRE) Task Offload](network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload.md)">网络虚拟化使用通用路由封装 (NVGRE) 任务卸载</a>，从而有可能使用通用路由封装 GRE 封装的数据包，其中：</p>
<ul>
<li>大量发送卸载 (LSO)</li>
<li>虚拟机队列 (VMQ)</li>
<li>传输 （德克萨斯州） 校验和卸载</li>
<li>接收 (Rx) 校验和卸载</li>
</ul></li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p><a href="virtualized-networking.md" data-raw-source="[Virtualized Networking](virtualized-networking.md)">虚拟化的网络</a></p></td>
<td align="left"><p>支持的 HYPER-V 虚拟化环境，如下所示的网络技术：</p>
<ul>
<li><p><a href="single-root-i-o-virtualization--sr-iov-.md" data-raw-source="[Single Root I/O Virtualization (SR-IOV)](single-root-i-o-virtualization--sr-iov-.md)">单根 I/O 虚拟化 (SR-IOV)</a></p></li>
<li><p><a href="virtual-machine-queue--vmq--in-ndis-6-20.md" data-raw-source="[Virtual Machine Queue (VMQ)](virtual-machine-queue--vmq--in-ndis-6-20.md)">虚拟机队列 (VMQ)</a></p></li>
<li><p><a href="hyper-v-extensible-switch.md" data-raw-source="[Hyper-V Extensible Switch](hyper-v-extensible-switch.md)">Hyper-V 可扩展交换机 </a></p></li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff571095" data-raw-source="[Wireless Networking](https://msdn.microsoft.com/library/windows/hardware/ff571095)">无线网络</a></p></td>
<td align="left"><p>包含本机 802.11 无线 LAN 的网络功能。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568366" data-raw-source="[Network Module Registrar](https://msdn.microsoft.com/library/windows/hardware/ff568366)">网络模块注册机构</a></p></td>
<td align="left"><p>系统工具，使得将附加到另一个网络模块的驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff571083" data-raw-source="[Winsock Kernel](https://msdn.microsoft.com/library/windows/hardware/ff571083)">Winsock 内核</a></p></td>
<td align="left"><p>内核模式网络编程接口 (NPI)。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ip-helper.md" data-raw-source="[IP Helper](ip-helper.md)">IP 帮助程序</a></p></td>
<td align="left"><p>一组启用驱动程序来检索和修改本地计算机的网络配置信息的实用工具函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="windows-filtering-platform-callout-drivers2.md" data-raw-source="[Windows Filtering Platform Callout Drivers](windows-filtering-platform-callout-drivers2.md)">Windows 筛选平台标注驱动程序</a></p></td>
<td align="left"><p>一个内核模式界面，使深度检测、 数据包修改、 流修改和网络数据的日志记录。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="system-area-networks.md" data-raw-source="[System Area Networks](system-area-networks.md)">系统区域网络</a></p></td>
<td align="left"><p>使用 Windows 套接字直接支持高性能、 面向连接的网络的网络连接的类型。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570659" data-raw-source="[Remote NDIS (RNDIS)](https://msdn.microsoft.com/library/windows/hardware/ff570659)">远程 NDIS (RNDIS)</a></p></td>
<td align="left"><p>定义系统提供的、 独立于总线的消息设置通过 USB 总线类规范。</p></td>
</tr>
</tbody>
</table>

 

 

 






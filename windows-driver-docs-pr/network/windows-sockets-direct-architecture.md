---
title: Windows Sockets Direct 体系结构
description: Windows Sockets Direct 体系结构
ms.assetid: 2f6ac4a7-76fe-45b4-8b5b-3a5f1d5c0553
keywords:
- Windows 套接字直接 WDK，体系结构
- TCP/IP WDK San
- NIC 组件 WDK San
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 586d869b50d8ba5e583cb7d2e6d0d24d02e9dec4
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215391"
---
# <a name="windows-sockets-direct-architecture"></a>Windows Sockets Direct 体系结构





Windows 套接字直接通过将 SAN 传输接口直接映射到应用程序进程，在同一系统区域网络上的两个网络节点之间提供高速、高性能的连接 (SAN) 。 此 SAN 连接使用户模式进程可以 (i/o) 执行直接输入和输出，而无需在用户内核边界之间进行复制。

[系统区域简介](introduction-to-system-area-networks.md)中的 SAN 体系结构图显示了 Windows socket Direct 如何提供 SAN 连接。 图中的阴影区域表示一个 SAN NIC 供应商必须提供的组件，以支持使用 SAN。

以下各段介绍了图中显示的组件。

### <a name="supplied-components-for-san-network-interface-controllers"></a>提供的 SAN 网络接口控制器组件

每个 SAN 网络接口控制器 (NIC) 使用以下软件组件为 NDIS 和 Windows Socket Direct 提供支持。

-   用于 SAN NIC 的 NDIS 微型端口驱动程序支持 NDIS，使其能够使用标准 TCP/IP 协议驱动程序与 Windows 套接字应用程序进行通信。 此 NDIS 微型端口驱动程序支持标准媒体类型（例如以太网或 ATM）。

-   SAN 服务提供程序 DLL 及其关联的代理驱动程序为 Windows Socket Direct 提供支持。 这些 Windows 套接字直通组件将 SAN 的互连的本机传输语义导出到 Windows 套接字应用程序。 例如，这些语义可以包括地址系列和消息方向。

SAN NIC 供应商提供 NDIS 微型端口驱动程序和 Windows 套接字直接组件。 如果 NIC 中未完全实现传输服务，则 SAN NIC 供应商也可能提供 SAN 传输驱动程序。 San 服务提供程序 DLL 和 SAN 传输驱动程序的代理驱动程序包含在 NDIS 微型端口驱动程序中，或者包含在单独的驱动程序中，由 SAN NIC 供应商决定。

### <a name="windows-sockets-switch-components"></a>Windows 套接字交换机组件

Windows 套接字交换机是 Windows 套接 Direct 的操作系统提供的组件。 开关是在 TCP/IP 和 SAN 服务提供商之上分层的 Windows 套接字服务提供程序。 Windows 操作系统在 Windows 套接 interface 和其他服务提供商之间插入交换机。 为清楚起见，此开关作为单独的实体显示在图中。 但是，开关和基本 TCP/IP 服务提供程序实际上是在同一个 DLL 中实现的。 开关执行以下操作：

-   使安装的 SAN 服务提供商和标准 TCP/IP 提供程序的集合看起来像是 Windows 套接字应用程序的单个提供程序。

-   根据每个连接选择是否使用本机 SAN 服务提供程序或标准 TCP/IP 提供程序为应用程序套接字提供服务。

-   使用本机 SAN 服务提供程序时模拟 TCP/IP 语义。

开关的顶部和底部接口符合 Windows 套接字服务提供程序接口 (SPI) 。 交换机的底部界面使用 Windows 套接 SPI 的扩展来利用 SAN 的功能。 这些扩展在适用于 [san 的 Windows 套接字 SPI 扩展](windows-sockets-spi-extensions-for-sans.md) 中进行了介绍，并在 [Windows socket 直接参考](/previous-versions/windows/hardware/network/ff565857(v=vs.85))中提供了完整记录。

交换机管理对所有网络的应用程序访问。 一台计算机可以包含多个供应商提供的多个 SAN Nic，以及一个或多个 LAN 和 WAN Nic，如支持以太网网络的 LAN NIC。 交换机可以透明地管理应用程序对与这些 Nic 关联的所有网络的访问。

### <a name="tcpip-functions"></a>TCP/IP 函数

与通过 NDIS 公开的任何 NIC 一样，TCP/IP 协议驱动程序将一个或多个 IP 地址分配给每个 SAN NIC。 Windows 套接字交换机和 SAN 服务提供商确定这些分配，如 [接收和转换 NIC 地址](receiving-and-translating-nic-addresses.md)中所述。 交换机使用此 IP 地址信息来确定要用于给定套接字连接的 SAN 服务提供程序。 SAN 服务提供程序使用此 IP 地址信息将 IP 地址转换为本机 SAN 地址。

交换机与标准的基本 TCP/IP 服务提供程序密切合作，以获得 SAN 服务提供商不支持的功能。 TCP/IP 服务提供程序支持侦听多个提供程序上的连接，并支持跨多个提供程序进行同步。

TCP/IP 服务提供程序还处理通过标准 LAN 和 WAN 互连、原始 IP 套接字、所有 UDP 套接字和子网之间的连接进行的所有通信。

 


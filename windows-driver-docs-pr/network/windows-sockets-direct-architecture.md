---
title: Windows Sockets Direct 体系结构
description: Windows Sockets Direct 体系结构
ms.assetid: 2f6ac4a7-76fe-45b4-8b5b-3a5f1d5c0553
keywords:
- Windows 套接字直接 WDK，体系结构
- San 的 TCP/IP WDK
- NIC 组件 WDK San
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f1f396dcb7eb444f076930fcad082b2f7bdc3af1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364926"
---
# <a name="windows-sockets-direct-architecture"></a>Windows Sockets Direct 体系结构





Windows 套接字直接提供通过 SAN 传输接口映射直接到应用程序进程在同一系统区域网络 (SAN) 上的两个网络节点之间的高速、 高性能连接。 此 SAN 连接，可以用户模式进程，而不复制在用户内核边界之间执行直接输入和输出 (I/O)。

图的 SAN 体系结构[简介系统区域网络](introduction-to-system-area-networks.md)显示如何 Windows 套接字直接提供的 SAN 连接。 在图中的阴影的区域表示 SAN NIC 供应商必须提供可用来启用的 SAN 的组件。

以下各段介绍图中显示的组件。

### <a name="supplied-components-for-san-network-interface-controllers"></a>提供 SAN 网络接口控制器组件

每个 SAN 网络接口控制器 (NIC) 使用以下软件组件提供对 NDIS 和 Windows 套接字直接支持。

-   SAN NIC 的 NDIS 微型端口驱动程序提供支持 NDIS，以便它可以与使用标准的 TCP/IP 协议驱动程序的 Windows 套接字应用程序进行通信。 此 NDIS 微型端口驱动程序支持标准的媒体类型，例如以太网或 ATM。

-   SAN 服务提供程序 DLL 和其关联的代理驱动程序提供对 Windows 套接字直接的支持。 这些 Windows 套接字直接组件导出的 Windows 套接字应用程序到 SAN 的相互连接的本机传输语义。 例如，这些语义可包括地址系列和消息方向。

SAN NIC 供应商提供的 NDIS 微型端口驱动程序和 Windows 套接字直接组件。 如果传输服务未在 NIC 中完全实现，SAN NIC 供应商还可能提供 SAN 传输驱动程序 在 NDIS 微型端口驱动程序中或在单独的驱动程序，SAN NIC 供应商决定包含 SAN 服务提供程序 DLL 的代理驱动程序，可能是 SAN 传输驱动程序。

### <a name="windows-sockets-switch-components"></a>Windows 套接字交换机组件

Windows 套接字开关是 Windows 套接字直接的操作系统提供的组件。 开关是之上 TCP/IP 和 SAN 服务提供商的 Windows 套接字服务提供商。 Windows 操作系统将插入 Windows 套接字接口和其他服务提供商之间切换。 为清楚起见，该交换机显示在图中作为单独的实体。 但是，交换机和基本的 TCP/IP 服务提供程序会实际在 DLL 中实现相同。 此开关执行以下操作：

-   使已安装的 SAN 服务提供商和标准 TCP/IP 提供程序看起来像单个提供程序对 Windows 套接字应用程序的集合。

-   选择时，基于每个连接是否使用本机 SAN 服务提供商或标准 TCP/IP 提供程序服务应用程序套接字。

-   使用本机 SAN 服务提供程序时，来模拟 TCP/IP 语义。

此开关的顶部和底部接口符合对 Windows 套接字服务提供程序接口 (SPI)。 开关的底部接口使用 Windows 套接字 SPI 的扩展来充分利用 SAN 的功能。 这些扩展插件中所述[Windows 套接字的 SPI 扩展 San](windows-sockets-spi-extensions-for-sans.md) ，并完全记录中记录[Windows 套接字直接引用](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565857(v=vs.85))。

交换机管理应用程序对所有网络访问。 计算机可能包含多个来自多个供应商的 SAN Nic，以及一个或多个 LAN 和 WAN Nic，如 LAN NIC 支持以太网网络。 交换机管理应用程序以透明方式与两个 Nic 相关联的所有网络访问。

### <a name="tcpip-functions"></a>TCP/IP 函数

使用 NDIS 通过公开的任何 NIC，如 TCP/IP 协议驱动程序将一个或多个 IP 地址分配给每个 SAN nic。 Windows 套接字切换和 SAN 服务提供商确定这些分配，如中所述[接收和转换 NIC 地址](receiving-and-translating-nic-addresses.md)。 此开关使用此 IP 地址信息来确定哪些 SAN 服务提供程序要用于给定的套接字连接。 SAN 服务提供商使用此 IP 地址信息转换为本机 SAN 地址的 IP 地址。

与标准基本 TCP/IP 服务提供商来获取 SAN 服务提供商不支持的功能，该交换机紧密合作。 TCP/IP 服务提供程序支持跨多个提供程序侦听的多个提供程序和同步的连接。

TCP/IP 的服务提供程序还处理所有通信通过标准的 LAN 和 WAN 都互连，原始 IP 套接字，所有 UDP 套接字和子网之间的连接。

 

 






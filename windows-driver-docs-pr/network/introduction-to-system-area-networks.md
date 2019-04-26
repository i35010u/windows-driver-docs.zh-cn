---
title: 系统区域网络简介
description: 系统区域网络简介
ms.assetid: 28d92bb5-8c3c-4f46-b908-63e3a3efff37
keywords:
- 系统区域网络 WDK，有关系统区域网络
- SAN WDK，有关系统区域网络
- 中心 WDK San
- 节点 WDK San
- San 的 SAN NIC WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31d4ae95050407d48ea488edbc1b447b80d76131
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329853"
---
# <a name="introduction-to-system-area-networks"></a>系统区域网络简介





一个*系统区域网络 (SAN)* 是可以将链接的计算机的群集的高性能、 面向连接的网络。 SAN 提供高带宽 (1 Gbps 或更高版本) 较低的延迟。 SAN 通常切换支持八个或多个节点的中心。 节点上从几个计量到几公里为单位的 SAN 范围之间数据线的长度。

与现有的网络技术，如以太网和 ATM，不同 SAN 提供可靠传输服务;也就是说，SAN 保证它已发送的相同顺序中未被破坏的数据传送。 在 SAN 中的连接终结点不需要使用 TCP/IP 协议堆栈来传输数据，除非必须子网之间路由流量。 可以使用 SAN 本地通信绕过 TCP/IP 协议堆栈的本机 SAN 传输。

SAN 网络接口控制器 (NIC)，SAN NIC 的传输驱动程序或这两者的组合公开专用传输接口。 但是，由于大多数网络应用程序编写为使用 TCP/IP 通过 Windows 套接字，它们不能直接使用 SAN。 [Windows 套接字直接](windows-sockets-direct.md)组件在下图中所示，这些应用程序，而无需修改以透明方式使用 SAN 而受益。 Windows 套接字直接是的一部分：

-   Microsoft Windows 2000 Datacenter Server

-   Microsoft Windows 2000 Advanced Server SP2

-   Microsoft Windows 2000 Server 设备工具包 SP2

-   Microsoft Windows Server 2003

下图显示了支持 SAN 所需的体系结构。 阴影的区域表示组件以便使用 SAN 的 SAN NIC 供应商提供。

![说明支持系统区域网络 (san) 所需的体系结构的关系图](images/wsdpsan.png)

下面是在此图中所示的组件的说明。

<a href="" id="windows-sockets-application-------"></a>**Windows 套接字应用程序**   
使用 Windows 套接字接口的网络服务的应用程序。

<a href="" id="windows-sockets-------"></a>**Windows 套接字**   
Windows 套接字接口 (Ws2\_32.dll)。

<a href="" id="windows-sockets-spi-------"></a>**Windows 套接字 SPI**   
Windows 套接字服务提供程序接口 (SPI)。

<a href="" id="windows-sockets-switch"></a>**Windows 套接字切换**  
Windows 套接字使用的标准 TCP/IP 服务提供程序和特定 SAN 服务提供商之间切换。

<a href="" id="tcp-ip-service-provider"></a>**TCP/IP 服务提供程序**  
用户模式 DLL 和关联的内核模式代理驱动程序组成的标准基本 Windows 套接字服务提供程序 TCP/IP。 代理驱动程序公开 TDI 接口。

<a href="" id="tcp-ip"></a>**TCP/IP**  
标准的 TCP/IP 协议驱动程序。

<a href="" id="san-service-provider"></a>**SAN 服务提供程序**  
SAN 服务提供程序的用户模式 DLL 部分。

<a href="" id="proxy-driver-for-a-san-service-provider"></a>**SAN 服务提供程序的代理驱动程序**  
SAN 服务提供程序的内核模式下的代理驱动程序。

<a href="" id="ndis-miniport-driver"></a>**NDIS 微型端口驱动程序**  
支持使用标准的 TCP/IP 协议驱动程序的 SAN nic 通信 NDIS 微型端口驱动程序。

<a href="" id="san-transport"></a>**SAN 传输**  
一个可靠传输服务，它可以完全实现中的 NIC，完全在软件中，实现也实现中的硬件和软件组合。

<a href="" id="san-nic"></a>**SAN NIC**  
物理 SAN 的网络接口控制器 (NIC)。

[]()  
用于特定 SAN 的内核模式提供程序。 （保留供将来使用。）

 

 






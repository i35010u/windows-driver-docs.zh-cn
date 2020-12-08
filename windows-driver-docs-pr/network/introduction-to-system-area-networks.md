---
title: 系统区域网络简介
description: 系统区域网络简介
keywords:
- 系统区域网络 WDK，关于系统区域网络
- SAN WDK，关于系统区域网络
- 集线器 WDK San
- 节点 WDK San
- SAN NIC WDK San
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0762103a3626156543e657987016a2f65df4f410
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815953"
---
# <a name="introduction-to-system-area-networks"></a>系统区域网络简介





*(SAN) 的系统区域网络* 是一种高性能、面向连接的网络，可以链接计算机的群集。 SAN 提供高带宽 (1 Gbps 或更高的) ，延迟较低。 SAN 通常通过支持八个或更多节点的集线器进行切换。 SAN 上节点之间的电缆长度介于数米到几千米之间。

与现有的网络技术（如以太网和 ATM）不同，SAN 提供可靠的传输服务;也就是说，SAN 保证交付未损坏的数据，其顺序与发送时的顺序相同。 SAN 中的连接终结点不需要使用 TCP/IP 协议堆栈传输数据，除非必须在子网之间路由流量。 SAN 本地通信可以使用本机 SAN 传输，绕过 TCP/IP 协议堆栈。

SAN 网络接口控制器 (NIC) ，用于 SAN NIC 的传输驱动程序，或者两者的组合都公开专用传输接口。 但是，由于大多数网络应用程序都是通过 Windows 套接字使用 TCP/IP 来编写的，因此它们不能直接使用 SAN。 下图中显示的 [Windows 套接字直接](windows-sockets-direct.md) 组件可让这些应用程序从无需修改的情况下透明地使用 SAN。 Windows 套接 Direct 属于以下内容：

-   Microsoft Windows 2000 Datacenter 服务器

-   Microsoft Windows 2000 Advanced Server SP2

-   Microsoft Windows 2000 服务器设备工具包 SP2

-   Microsoft Windows Server 2003

下图显示支持 SAN 所需的体系结构。 灰色区域表示 SAN NIC 供应商提供的用于使用 SAN 的组件。

![说明支持 (san 的系统区域网络所需的体系结构的关系图) ](images/wsdpsan.png)

下面是此图中所示组件的说明。

<a href="" id="windows-sockets-application-------"></a>**Windows 套接字应用程序**   
用于网络服务的 Windows 套接字接口的应用程序。

<a href="" id="windows-sockets-------"></a>**Windows 套接字**   
Windows 套接字接口 (Ws2 \_32.dll) 。

<a href="" id="windows-sockets-spi-------"></a>**Windows 套接字 SPI**   
Windows 套接字服务提供程序接口 (SPI) 。

<a href="" id="windows-sockets-switch"></a>**Windows 套接字交换机**  
Windows 套接字在使用标准 TCP/IP 服务提供程序和特定的 SAN 服务提供程序之间切换。

<a href="" id="tcp-ip-service-provider"></a>**TCP/IP 服务提供程序**  
用户模式 DLL 和关联的内核模式代理驱动程序，其中包含适用于 TCP/IP 的标准基本 Windows 套接字服务提供程序。 代理驱动程序公开 TDI 接口。

<a href="" id="tcp-ip"></a>**TCP/IP**  
标准 TCP/IP 协议驱动程序。

<a href="" id="san-service-provider"></a>**SAN 服务提供程序**  
SAN 服务提供程序的用户模式 DLL 部分。

<a href="" id="proxy-driver-for-a-san-service-provider"></a>**SAN 服务提供程序的代理驱动程序**  
SAN 服务提供程序的内核模式代理驱动程序。

<a href="" id="ndis-miniport-driver"></a>**NDIS 微型端口驱动程序**  
支持使用标准 TCP/IP 协议驱动程序与 SAN NIC 通信的 NDIS 微型端口驱动程序。

<a href="" id="san-transport"></a>**SAN 传输**  
可靠的传输服务，可在 NIC 中完全实现，在软件中完全实现，或者在硬件和软件的组合中实现。

<a href="" id="san-nic"></a>**SAN NIC**  
物理 SAN 网络接口控制器 (NIC) 。

特定 SAN 的内核模式提供程序。  (保留以供将来使用。 ) 

 

 






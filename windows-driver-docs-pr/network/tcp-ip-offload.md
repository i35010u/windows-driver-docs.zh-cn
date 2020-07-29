---
title: TCP/IP 卸载概述
description: TCP/IP 卸载概述
ms.assetid: 1f074ce5-2614-47a5-9ee0-a5e43f05273d
keywords:
- 网络驱动程序 WDK，TCP/IP 卸载
- TCP/IP 卸载 WDK 网络
- 卸载 WDK TCP/IP 传输
- Tcp/ip 卸载 WDK 网络，关于 TCP/IP 卸载
- 卸载 WDK TCP/IP 传输，关于 TCP/IP 卸载
- 任务卸载 WDK TCP/IP 传输
- 连接卸载 WDK TCP/IP 传输
- 包 WDK 网络，TCP/IP 卸载
ms.date: 06/21/2019
ms.localizationpriority: medium
ms.openlocfilehash: 68803e54f329221257f4cb0205918f5e186f718d
ms.sourcegitcommit: 9102e34c3322d8697dbb6f9a1d78879147a73373
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/28/2020
ms.locfileid: "87264454"
---
# <a name="tcpip-offload-overview"></a>TCP/IP 卸载概述

为了提高性能，Microsoft TCP/IP 传输可以卸载具有相应 TCP/IP 卸载功能的 NIC 的任务或连接。

从 Windows Vista 开始，Windows 操作系统支持以下 TCP/IP 卸载服务：

-   校验和任务

-   应用程序 Internet 协议安全性（IPsec）卸载版本1

-   IPsec 卸载版本2
    - \[IPsec 任务卸载功能已弃用，不应使用。\]

-   大型发送卸载版本1

-   大型发送卸载版本2

-   连接卸载

从 Windows 10 版本1912开始，Windows 还支持 UDP 分段卸载（USO）。

从 Windows Vista 开始提供的 TCP/IP 传输支持用于 IPv4 和 IPv6 数据包的 TCP/IP 卸载服务。

NDIS 6.0 和更高版本的微型端口驱动程序支持多协议驱动程序环境中的 TCP/IP 卸载服务。 绑定到 TCP/IP 卸载的多端口适配器的多个 NDIS 6.0 和更高版本的协议驱动程序可以配置 TCP/IP 卸载服务。

本节包括：

-   [访问 TCP/IP 卸载网络 \_ 缓冲区 \_ 列表信息](accessing-tcp-ip-offload-net-buffer-list-information.md)
-   [使用 TCP/IP 卸载管理员界面](using-the-tcp-ip-offload-administrator-interface.md)
-   [支持卸载的微型端口驱动程序安全指导原则](security-guidelines-for-offload-capable-miniport-drivers.md)
-   [TCP/IP 任务卸载](task-offload.md)
-   [连接卸载](connection-offload.md)

 

 






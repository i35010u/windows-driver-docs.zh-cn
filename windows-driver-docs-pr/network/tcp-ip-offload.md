---
title: TCP/IP 卸载
description: TCP/IP 卸载
ms.assetid: 1f074ce5-2614-47a5-9ee0-a5e43f05273d
keywords:
- 网络驱动程序 WDK，TCP/IP 卸载
- 卸载 WDK 的 TCP/IP 网络
- 卸载 WDK TCP/IP 传输
- TCP/IP 卸载 WDK 网络，有关 TCP/IP 卸载
- 卸载 WDK TCP/IP 传输，有关 TCP/IP 卸载
- 任务卸载，WDK TCP/IP 传输
- 连接将卸载 WDK TCP/IP 传输
- 数据包 WDK 网络，TCP/IP 卸载
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5924e6c230c51f5a84a4028b3eb610748941266f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350832"
---
# <a name="tcpip-offload"></a>TCP/IP 卸载





若要提高其性能，可以将任务或连接到具有相应的 TCP/IP-卸载功能的 NIC 会卸载 Microsoft TCP/IP 传输。

从 Windows Vista 开始，Windows 操作系统支持以下 TCP/IP 卸载服务：

-   校验和任务

-   应用程序的 Internet 协议安全性 (IPsec) 将卸载版本 1

-   IPsec 卸载版本 2
    - \[IPsec 任务卸载功能已弃用，不应使用。\]

-   大量发送卸载版本 1

-   大量发送卸载版本 2

-   连接卸载

使用 Windows Vista 提供从 TCP/IP 传输支持为 IPv4 和 IPv6 数据包的 TCP/IP 卸载服务。

NDIS 6.0 和更高版本的微型端口驱动程序在多个协议驱动程序的环境中支持 TCP/IP 卸载服务。 多个 NDIS 6.0 和更高版本的协议驱动程序绑定到 TCP/IP 支持卸载的微型端口适配器可以配置 TCP/IP 卸载服务。

本部分包括：

-   [访问 TCP/IP 卸载 NET\_缓冲区\_列出信息](accessing-tcp-ip-offload-net-buffer-list-information.md)
-   [使用 TCP/IP 卸载管理员界面](using-the-tcp-ip-offload-administrator-interface.md)
-   [支持卸载的微型端口驱动程序的安全指导原则](security-guidelines-for-offload-capable-miniport-drivers.md)
-   [TCP/IP 任务卸载](task-offload.md)
-   [连接卸载](connection-offload.md)

 

 






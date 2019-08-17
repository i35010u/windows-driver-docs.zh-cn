---
title: Windows 套接字直接概述
description: Windows 套接字直接概述
ms.assetid: 9e153a77-c4d4-4425-8f36-5ab9d6a80386
keywords:
- 系统区域网络 WDK, Windows 套接字直通
- SAN WDK, Windows 套接字直通
- Windows 套接直 WDK
- Windows 套接字直接 WDK, 关于 Windows 套接 Direct
- Windows 套接字直接切换 WDK
- 切换 WDK Windows 套接字直通
- 套接字 WDK Windows 套接直
- SAN NIC WDK San
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1fdc47682455939532267c771cbd4c05f340c54c
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565614"
---
# <a name="windows-sockets-direct-overview"></a>Windows 套接字直接概述





Microsoft Windows Socket Direct 是一种技术, 在可能的情况下, 在可能的情况下, 通过系统区域网络 (SAN) 而不是 TCP/IP 传输和 NDIS 微型端口驱动程序以高速路由数据和从 Windows 套接字应用程序进行高性能路由。

Windows 套接字直接包含在中:

-   Microsoft Windows 2000 Datacenter 服务器

-   Microsoft Windows 2000 Advanced Server SP2

-   Microsoft Windows 2000 服务器设备工具包 SP2

-   Microsoft Windows Server 2003

以下主题介绍了 Windows 套接字直接功能和操作、启用 Windows Socket Direct 的软件组件以及写入 SAN 服务提供程序及其关联代理驱动程序的要求:

[Windows 套接字直接体系结构](windows-sockets-direct-architecture.md)

[Windows 套接字直接组件操作](windows-sockets-direct-component-operation.md)

[为 SAN 创建服务提供程序](creating-a-service-provider-for-a-san.md)

[为 SAN 服务提供程序创建代理驱动程序](creating-a-proxy-driver-for-a-san-service-provider.md)

 

 






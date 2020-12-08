---
title: 连接卸载概述
description: 连接卸载概述
keywords:
- 连接卸载 WDK TCP/IP 传输
- TCP/IP 卸载 WDK 网络，连接卸载
- 卸载 WDK TCP/IP 传输，连接卸载
- 连接卸载 WDK TCP/IP 传输，关于连接卸载
- 功能 WDK TCP/IP 卸载
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c33ebcca6fa98793d16d0e707bf98e5ad0fd62a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808067"
---
# <a name="connection-offload-overview"></a>连接卸载概述





为了提高性能，Microsoft TCP/IP 传输可将连接卸载到具有适当 TCP/IP 连接卸载功能的 NIC。

NDIS 连接卸载接口提供挂钩来启用连接卸载服务（如 TCP 烟囱卸载）的配置。 有关 NDIS 中的连接卸载服务的详细信息，请参阅 [卸载 Tcp/ip 连接](offloading-tcp-ip-connections.md)。

在 NDIS 6.0 和更高版本中支持 TCP 烟囱卸载服务。

本节包括：

-   [确定连接卸载功能](determining-connection-offload-capabilities.md)
-   [报告 NIC 的连接卸载功能](reporting-a-nic-s-connection-offload-capabilities.md)
-   [启用和禁用连接卸载服务](enabling-and-disabling-connection-offload-services.md)
-   [确定当前的连接卸载设置](determining-the-current-connection-offload-settings.md)
-   [使用注册表值启用和禁用连接卸载](using-registry-values-to-enable-and-disable-connection-offloading.md)
-   [卸载 TCP/IP 连接](offloading-tcp-ip-connections.md)

 

 






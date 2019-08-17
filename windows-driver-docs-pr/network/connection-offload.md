---
title: 连接卸载概述
description: 连接卸载概述
ms.assetid: 4c1b1a98-6ad3-4817-9e3d-d6112c887352
keywords:
- 连接卸载 WDK TCP/IP 传输
- TCP/IP 卸载 WDK 网络, 连接卸载
- 卸载 WDK TCP/IP 传输, 连接卸载
- 连接卸载 WDK TCP/IP 传输, 关于连接卸载
- 功能 WDK TCP/IP 卸载
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b5f850b8785ec0ccc4537026bd58c95d4c269c96
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565761"
---
# <a name="connection-offload-overview"></a>连接卸载概述





为了提高性能, Microsoft TCP/IP 传输可将连接卸载到具有适当 TCP/IP 连接卸载功能的 NIC。

NDIS 连接卸载接口提供挂钩来启用连接卸载服务 (如 TCP 烟囱卸载) 的配置。 有关 NDIS 中的连接卸载服务的详细信息, 请参阅[卸载 Tcp/ip 连接](offloading-tcp-ip-connections.md)。

在 NDIS 6.0 和更高版本中支持 TCP 烟囱卸载服务。

本部分包括：

-   [确定连接卸载功能](determining-connection-offload-capabilities.md)
-   [报告 NIC 的连接卸载功能](reporting-a-nic-s-connection-offload-capabilities.md)
-   [启用和禁用连接卸载服务](enabling-and-disabling-connection-offload-services.md)
-   [确定当前的连接卸载设置](determining-the-current-connection-offload-settings.md)
-   [使用注册表值启用和禁用连接卸载](using-registry-values-to-enable-and-disable-connection-offloading.md)
-   [卸载 TCP/IP 连接](offloading-tcp-ip-connections.md)

 

 






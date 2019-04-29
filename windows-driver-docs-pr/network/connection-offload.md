---
title: 连接卸载
description: 连接卸载
ms.assetid: 4c1b1a98-6ad3-4817-9e3d-d6112c887352
keywords:
- 连接将卸载 WDK TCP/IP 传输
- TCP/IP 卸载 WDK 网络连接卸载
- 卸载 WDK TCP/IP 传输，连接卸载
- 连接卸载 WDK TCP/IP 传输，有关连接卸载
- 卸载功能 WDK TCP/IP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf445931229909edb60544d2ac2a785a5e3ce914
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357444"
---
# <a name="connection-offload"></a>连接卸载





为了提高其性能，Microsoft TCP/IP 传输可以卸载到 NIC 具有相应 TCP/IP-连接卸载功能的连接。

NDIS 连接卸载接口提供挂钩，以启用连接的配置将卸载服务，例如 TCP 烟囱卸载。 在 NDIS 连接卸载服务的详细信息，请参阅[卸载 TCP/IP 连接](offloading-tcp-ip-connections.md)。

NDIS 6.0 及更高版本支持 TCP 烟囱卸载服务。

本部分包括：

-   [确定连接卸载功能](determining-connection-offload-capabilities.md)
-   [报告一个 NIC 连接卸载功能](reporting-a-nic-s-connection-offload-capabilities.md)
-   [启用和禁用连接卸载服务](enabling-and-disabling-connection-offload-services.md)
-   [确定当前的连接卸载设置](determining-the-current-connection-offload-settings.md)
-   [使用注册表值来启用和禁用连接卸载](using-registry-values-to-enable-and-disable-connection-offloading.md)
-   [卸载 TCP/IP 连接](offloading-tcp-ip-connections.md)

 

 






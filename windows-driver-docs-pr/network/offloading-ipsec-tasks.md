---
title: 卸载 IPsec 任务
description: 卸载 IPsec 任务
ms.assetid: e2006459-cc74-43d1-9ce0-4869e2ef5d7d
keywords:
- 任务卸载 WDK TCP/IP 传输，IPsec 任务
- IPsec 卸载 WDK TCP/IP 传输，关于卸载 IPsec 任务
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f6f9e7a6b44e0d219193c05299aed859cdeee01e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834606"
---
# <a name="offloading-ipsec-tasks"></a>卸载 IPsec 任务

\[IPsec 任务卸载功能已弃用，不应使用。\]




本部分介绍了如何卸载 Internet 协议安全（IPsec）任务。

**请注意**  IPsec 卸载带外（OOB）数据将存储在[**网络\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)信息数组中。 有关 OOB 数据的详细信息，请参阅[访问 Tcp/ip 卸载 NET\_BUFFER\_列表信息](accessing-tcp-ip-offload-net-buffer-list-information.md)。

 

在 NDIS 6.1 和更高版本中支持[IPsec 卸载版本 2](ipsec-offload-version-2.md) 。

在 NDIS 6.0 和更高版本中支持[IPsec 卸载版本 1](ipsec-offload-version-1.md) 。

本部分包括以下主题：

-   [IPsec 卸载版本1](ipsec-offload-version-1.md)
-   [IPsec 卸载版本2](ipsec-offload-version-2.md)

 

 






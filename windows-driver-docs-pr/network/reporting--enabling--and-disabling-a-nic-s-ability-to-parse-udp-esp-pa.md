---
title: 报告、 启用和禁用分析 UDP ESP 数据包的 NIC 的能力
description: 报告、 启用和禁用分析 UDP ESP 数据包的 NIC 的能力
ms.assetid: 3a75c5b2-2d94-428e-9b2a-d760e14df552
keywords:
- UDP 封装的 ESP 数据包 WDK IPsec 卸载、 分析功能
- 分析的功能 WDK IPsec 卸载
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a46badf0be2c795728d9311e257cea5097e4994
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373285"
---
# <a name="reporting-enabling-and-disabling-a-nics-ability-to-parse-udp-esp-packets"></a>报告、 启用和禁用分析 UDP ESP 数据包的 NIC 的能力

\[IPsec 任务卸载功能已弃用，不应使用。\]




微型端口驱动程序指定 NIC 的 Internet 协议安全 (IPsec) 中的功能[ **NDIS\_IPSEC\_卸载\_V1** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_ipsec_offload_v1)结构。 有关详细信息，请参阅[报告 NIC 的 IPsec 功能](reporting-a-nic-s-ipsec-capabilities.md)。

微型端口报告来分析传入的 UDP 封装 ESP 数据包设置一个或多个标志的 NIC 的能力**支持**。 **保留**成员的 NDIS\_IPSEC\_卸载\_V1 结构。 微型端口驱动程序可以指定 any 或 all 中进行了描述的四个 UDP ESP 封装子[UDP ESP 封装类型](udp-esp-encapsulation-types.md)。

有关启用和 disableing UDP ESP 分析功能的信息，请参阅[启用和禁用 TCP/IP 卸载服务](enabling-and-disabling-task-offload-services.md)。

 

 






---
title: NDIS 6.20 中的电源管理增强功能
description: 介绍 NDIS 6.20 电源管理增强功能，以减少计算机能耗
ms.assetid: 99900def-66f8-4ba1-a7c1-3a5e9f456ca1
keywords:
- NDIS 6.20 WDK，电源管理增强功能
- 电源管理 WDK 网络，NDIS 6.20 增强功能
- 电源管理增强功能 WDK NDIS 6.20
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 422bb22f53aa3c4dad962e0c926d02dbd3d3da1b
ms.sourcegitcommit: db9d058a9e592d4c47c67fc14f04f0ddc3aa92af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/13/2020
ms.locfileid: "91989831"
---
# <a name="power-management-enhancements-in-ndis-620"></a>NDIS 6.20 中的电源管理增强





NDIS 6.20 引入了电源管理增强功能，以降低计算机的功耗。 对于 NDIS 6.20 和更高版本的驱动程序，NDIS 6.20 电源管理支持是必需的。

NDIS 6.20 电源管理接口向后兼容不支持最新电源管理功能的 Nic 和微型端口驱动程序。

NDIS 6.20 和更高版本中的电源管理界面支持：

-   LAN 唤醒 (基于数据包类型的 WOL) 模式，以及支持偏移和模式匹配的 NDIS 6.1 及更低版本的方法。 因此，NDIS 6.20 和更高版本的 WOL 模式可能更具体，以避免不必要的唤醒事件。 例如，NIC 可以确定 TCP 同步) 数据包 (。

-   用于某些最常见协议的 Nic 的协议卸载。 由于协议已卸载到 NIC，因此它可以代表计算机进行响应，以避免不需要的唤醒事件。 例如，NIC 可以处理 IPv4 地址解析协议 (ARP) 和 IPv6 邻居请求 (NS) 协议数据包，而无需唤醒计算机。

NDIS 6.20 和更高版本中的电源管理接口还支持：

-   WOL WLAN 增强功能。 必要时，NIC 可以处理 IEEE 802.11 组时态密钥， (GTK) rekey 请求处于低功耗状态。

-   当媒体连接时，NDIS 6.20 和更高版本可以唤醒计算机。 当媒体断开连接时，操作系统会将 NIC 置于低功耗状态。

某些 NDIS 设备驱动程序接口元素对于 NDIS 6.20 和更高版本的驱动程序已过时。 有关过时接口的详细信息，请参阅 [NDIS 6.20 中的过时接口](obsolete-interfaces-in-ndis-6-20.md)。

有关 ndis 6.20 和更高版本 NDIS 的电源管理的详细信息，请参阅 [电源管理 (ndis 6.20) ](ndis-power-management-overview.md)。

## <a name="related-topics"></a>相关主题


[NDIS 6.30 中的电源管理增强](introduction-to-ndis-6-30.md)

 

 







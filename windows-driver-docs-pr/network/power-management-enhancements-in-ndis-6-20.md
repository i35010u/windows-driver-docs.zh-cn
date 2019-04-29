---
title: 在 NDIS 6.20 的电源管理增强功能
description: 引入了 NDIS 6.20 电源管理增强功能，以减少计算机的功率消耗
ms.assetid: 99900def-66f8-4ba1-a7c1-3a5e9f456ca1
keywords:
- NDIS 6.20 WDK、 电源管理增强功能
- 电源管理 WDK 网络 NDIS 6.20 增强功能
- 电源管理增强功能 WDK NDIS 6.20
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dee3a93e1a7ef7321c3ae8d8bd722c005ab75325
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356883"
---
# <a name="power-management-enhancements-in-ndis-620"></a>NDIS 6.20 中的电源管理增强





NDIS 6.20 引入了电源管理增强功能以减少计算机的功率消耗。 NDIS 6.20 电源管理支持是必需的 NDIS 6.20 和更高版本的驱动程序。

NDIS 6.20 电源管理接口是与 Nic 和不支持的最新的电源管理功能的微型端口驱动程序向后兼容。

NDIS 6.20 和更高版本支持中的电源管理界面：

-   唤醒 LAN (WOL) 模式的基于数据包类型除了 NDIS 6.1 和更早方法支持的偏移量和模式匹配。 因此，NDIS 6.20 和更高版本的 WOL 模式可以是多个特定于以避免不必要唤醒的事件。 例如，NIC 可以识别 TCP 同步 (SYN) 数据包。

-   协议卸载到 Nic 的一些最常用的协议。 协议卸载到 NIC，因为它可以代表计算机以避免不需要的唤醒的事件进行响应。 例如，NIC 可以处理无唤醒计算机的 IPv4 地址解析协议 (ARP) 和 IPv6 邻居招标 (NS) 协议数据包。

电源管理接口 NDIS 6.20 及更高版本还支持：

-   WOL WLAN 的增强功能。 如有必要，NIC 可以处理 IEEE 802.11 组临时密钥 (GTK) 重新生成密钥请求在低功耗状态。

-   媒体连接时，将计算机可以唤醒 NDIS 6.20 及更高版本。 媒体已断开连接时，操作系统将在低功耗状态 NIC。

NDIS 设备驱动程序界面元素的某些已过时的 NDIS 6.20 和更高版本的驱动程序。 有关已过时的接口的详细信息，请参阅[NDIS 6.20 中已过时接口](obsolete-interfaces-in-ndis-6-20.md)。

有关 NDIS 6.20 和更高版本的 NDIS 电源管理的详细信息，请参阅[电源管理 (NDIS 6.20)](power-management--ndis-6-20-.md)。

## <a name="related-topics"></a>相关主题


[在 NDIS 6.30 电源管理增强功能](introduction-to-ndis-6-30.md)

 

 







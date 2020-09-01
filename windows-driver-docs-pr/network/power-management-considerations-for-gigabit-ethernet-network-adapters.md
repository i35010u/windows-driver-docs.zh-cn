---
title: 千兆以太网网络适配器的电源管理注意事项
description: 千兆位以太网网络适配器的电源管理注意事项
ms.assetid: f195d295-0a2a-4c44-a3b4-217dfad76826
keywords:
- 电源管理 WDK 网络，千兆以太网 Nic
- 网络接口卡 WDK 网络，过渡电源状态
- Nic WDK 网络，过渡电源状态
- Nic WDK 网络，千兆以太网 Nic
- 网络接口卡 WDK 网络，千兆以太网 Nic
- 千兆以太网 Nic WDK 网络
- 电源管理 WDK NDIS 微型端口，转换电源状态
- 设备电源状态 WDK 网络
- 电源状态 WDK 网络
- 转换电源状态 WDK 网络
- 唤醒功能，WDK 网络，过渡电源状态
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c8f2a9c65b3178c899664c569b67c15003b85d9c
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212801"
---
# <a name="power-management-considerations-for-gigabit-ethernet-network-adapters"></a>千兆位以太网网络适配器的电源管理注意事项


如果千兆位以太网网络适配器的运行速率为每秒1000兆位 (Mbps) ，则会消耗大量电源。 在此类网络适配器转换到低功耗状态之前，通常会降低其链接速度，使网络适配器消耗更少的电量。 降低的链接速度使得网络适配器可以转换到低功耗状态。 在转换到低功耗状态的过程中更改链接速度时，网络适配器通常会在短时间内失去网络连接。

相反，当千兆以太网网络适配器从低功耗状态转换到完全打开状态时，网络适配器的链接速度将增加到其完全操作速率。 在此转换期间，网络适配器可能会短时间丢失连接。

当微型端口驱动程序的基础网络适配器正在转换到低功耗状态或从低功耗状态转换时，微型端口不能指示链接速度的更改或连接状态的更改。 有关指示链接速度变化的详细信息，请参阅 [**NDIS \_ 状态 \_ 链接 \_ 状态**](./ndis-status-link-state.md)。 有关指示连接状态更改的详细信息，请参阅 [指示连接状态](indicating-connection-status.md)。

 


---
title: NDIS 电源管理概述
description: NDIS 电源管理概述
ms.assetid: 8ae3803f-c3e4-4499-9e61-678f4ab61fbc
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e0cfd9044fbf8d6a5369a2ea40b3d77380ffa9a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562115"
---
# <a name="ndis-power-management-overview"></a>NDIS 电源管理概述





本部分概述与的 NDIS 6.20 驱动程序引入 Windows 7 中的电源管理界面提供的功能。

微型端口驱动程序和协议驱动程序支持 NDIS 6.20 和更高版本的 NDIS 必须支持 NDIS 6.20 电源管理接口。 但是，NDIS 提供到上一接口转换为较旧的网络适配器和 NDIS 6.1 或更早的微型端口驱动程序不支持 NDIS 6.20 电源管理功能的。 有关 NDIS 6.20 向后兼容性问题的详细信息，请参阅[NDIS 6.20 向后兼容性](ndis-6-20-backward-compatibility.md)。

支持 NDIS 6.20 电源管理接口：

-   根据数据包的 LAN 唤醒 (WOL) 模式此外类型为 NDIS 6.1 和更早的方法。 因此，NDIS 6.20 WOL 模式可以更具体，以避免不必要的唤醒事件。 例如，网络适配器可以确定 TCP 同步 (SYN) 数据包。 WOL 方法的详细信息，请参阅[WOL 方法在 NDIS 6.20](wol-methods-in-ndis-6-20.md)。

-   协议将给网络适配器卸载某些最常用的协议。 协议卸载到网络适配器，因为它可以代表计算机以避免不必要的唤醒事件做出响应。 例如，网络适配器可以处理无唤醒计算机的 IPv4 地址解析协议 (ARP) 和 IPv6 邻居招标 (NS) 协议数据包。 对卸载有关电源管理协议的详细信息，请参阅[协议将卸载 NDIS 电源管理的](protocol-offloads-for-ndis-power-management.md)。

有关 NDIS 用于设置低功耗状态和还原完整功能的 WOL 事件序列的信息，请参阅[低的电源可用于 LAN 唤醒](low-power-for-wake-on-lan.md)。

此外支持 NDIS 6.20 电源管理：

-   NDIS 6.20 可以返回到完整的电源状态的网络适配器，媒体连接时。 媒体已断开连接时，操作系统将在低功耗状态的网络适配器。 有关媒体断开连接时设置低功耗状态的详细信息，请参阅[媒体断开连接的低开机](low-power-on-media-disconnect.md)。

本部分包括以下主题：

[在 NDIS 6.20 WOL 方法](wol-methods-in-ndis-6-20.md)

[NDIS 电源管理的 WOL 模式](wol-patterns-for-ndis-power-management.md)

[NDIS 电源管理的协议卸载](protocol-offloads-for-ndis-power-management.md)

 

 






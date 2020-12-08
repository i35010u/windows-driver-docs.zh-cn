---
title: NDIS 电源管理概述
description: NDIS 电源管理概述
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c742a5b2012234fad85a99a906671ba162557f87
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831293"
---
# <a name="ndis-power-management-overview"></a>NDIS 电源管理概述





本部分概述了在 Windows 7 中引入的用于 NDIS 6.20 驱动程序的功能。

支持 ndis 6.20 和更高版本的 NDIS 的微型端口驱动程序和协议驱动程序必须支持 NDIS 6.20 电源管理接口。 但是，NDIS 为较旧的网络适配器以及不支持 NDIS 6.20 电源管理功能的 NDIS 6.1 或更低的微型端口驱动程序提供了以前的接口转换。 有关 NDIS 6.20 向后兼容性问题的详细信息，请参阅 [ndis 6.20 向后兼容性](ndis-6-20-backward-compatibility.md)。

NDIS 6.20 电源管理界面支持：

-   LAN 唤醒 (基于数据包类型的 WOL) 模式，以及 NDIS 6.1 及更低版本的方法。 因此，可以更具体地了解 NDIS 6.20 WOL 模式，以避免不必要的唤醒事件。 例如，网络适配器可以 (SYN) 数据包来识别 TCP 同步。 有关 WOL 方法的详细信息，请参阅 [NDIS 6.20 中的 WOL 方法](wol-methods-in-ndis-6-20.md)。

-   对于一些最常见的协议，将协议卸载到网络适配器。 由于协议已卸载到网络适配器，因此它可以代表计算机进行响应，以避免不需要的唤醒事件。 例如，网络适配器可以在不唤醒计算机的情况下，处理 (ARP) 和 IPv6 邻居请求 (NS) 协议数据包。 有关电源管理协议卸载的详细信息，请参阅 [NDIS 电源管理的协议卸载](protocol-offloads-for-ndis-power-management.md)。

有关 NDIS 用于设置低功耗状态和全部恢复功能的 WOL 事件序列的信息，请参阅 [LAN 唤醒的低功率](low-power-for-wake-on-lan.md)。

NDIS 6.20 电源管理还支持：

-   当媒体连接时，NDIS 6.20 可将网络适配器恢复为完全电源状态。 当媒体断开连接时，操作系统将网络适配器置于低功耗状态。 有关在媒体断开连接时设置低功耗状态的详细信息，请参阅 [Media Disconnect 断开连接](low-power-on-media-disconnect.md)。

本节包括下列主题：

[NDIS 6.20 中的 WOL 方法](wol-methods-in-ndis-6-20.md)

[NDIS 电源管理的 WOL 模式](wol-patterns-for-ndis-power-management.md)

[NDIS 电源管理的协议卸载](protocol-offloads-for-ndis-power-management.md)

 

 






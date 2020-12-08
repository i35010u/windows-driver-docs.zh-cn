---
title: 远程 NDIS OID
description: 远程 NDIS OID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e6c0ccebee1360dfdf8594c5b2c488002adc071
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840605"
---
# <a name="remote-ndis-oids"></a>远程 NDIS OID





本部分列出了远程 NDIS 以太网设备必需的和可选的 NDIS Oid。 此列表将考虑远程 NDIS 设备和远程 NDIS 微型端口驱动程序的唯一属性，因此该列表与正常的 NDIS 无连接微型端口驱动程序所支持的列表并不完全相同。 某些 Oid 为 *set* 和 *query* oid;如果将必需 OID 定义为两者，则远程 ndis [ \_ \_ 设置 \_ 消息](remote-ndis-set-msg.md) 和 [远程 \_ ndis \_ 查询 \_ 消息](remote-ndis-query-msg.md)的远程 ndis 设备必须支持它。 有关 Oid 的详细说明，请参阅 Microsoft Windows 驱动程序开发工具包 (DDK) 。

以下远程 NDIS Oid 列表分为两组：常规 OID 和802.3 特定 OID。 此外，每个组都包含一个 "统计信息 OID" 查询子节。 所有网络设备都需要常规 Oid。

-   [常规 OID](general-oids2.md)
-   [常规统计信息 OID](general-statistic-oids.md)
-   [802.3 OID](802-3-oids.md)
-   [802.3 统计信息 OID](802-3-statistic-oids.md)
-   [可选电源管理 OID](optional-power-management-oids.md)
-   [可选网络唤醒 OID](optional-network-wake-up-oids.md)

 

 






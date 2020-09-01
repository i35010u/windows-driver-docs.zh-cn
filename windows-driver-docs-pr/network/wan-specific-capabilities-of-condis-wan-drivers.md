---
title: CoNDIS WAN 驱动程序的 WAN 特定功能
description: CoNDIS WAN 驱动程序的 WAN 特定功能
ms.assetid: c4e8e0ae-7dd5-4c4e-900a-b1f7e5eecb16
keywords:
- CoNDIS WAN 驱动程序，与非 WAN CoNDIS 驱动程序
- 非 WAN CoNDIS 驱动程序 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 56dec80b087226e44abea5fe2d21e063023400d2
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209621"
---
# <a name="wan-specific-capabilities-of-condis-wan-drivers"></a>CoNDIS WAN 驱动程序的 WAN 特定功能





CoNDIS WAN 驱动程序不同于非 WAN CoNDIS 驱动程序，如下所示：

-   支持 TAPI 服务的 CoNDIS WAN 驱动程序使用 CO \_ ADDRESS \_ 系列 \_ TAPI \_ 代理地址系列。

-   CoNDIS WAN 驱动程序支持特定于 WAN 的 Oid： [oid \_ wan \_ 永久性 \_ 地址](/previous-versions/windows/hardware/network/ff561220(v=vs.85))、 [oid \_ wan \_ 当前 \_ 地址](/previous-versions/windows/hardware/network/ff561200(v=vs.85))和 [OID \_ wan \_ 中型 \_ 子类型](/previous-versions/windows/hardware/network/ff561216(v=vs.85))。

-   CoNDIS WAN 微型端口驱动程序支持一组 CoNDIS WAN Oid 来设置和查询操作特征。 有关 CoNDIS WAN Oid 的详细信息，请参阅 [CONDIS Wan Objects](/windows-hardware/drivers/ddi/ntddndis/index)。

-   CoNDIS WAN 微型端口驱动程序提供 TAPI 服务支持一组 CoNDIS TAPI Oid 来设置和查询操作特征。 有关 CoNDIS TAPI Oid 的详细信息，请参阅 [面向连接的 NDIS 的 TAPI 扩展](./tapi-extension-oids-for-connection-oriented-ndis.md)。

-   CoNDIS WAN 微型端口驱动程序支持一组特定于 WAN 的状态指示，表示链接状态的更改。 有关 CoNDIS WAN 微型端口驱动程序状态指示的详细信息，请参阅 [指示 CONDIS Wan 微型端口驱动程序状态](indicating-condis-wan-miniport-driver-status.md)。

-   CoNDIS WAN 微型端口驱动程序保留一组特定于 WAN 的统计信息。 [Oid \_ WAN \_ CO \_ 获取 \_ 统计 \_ 信息](./oid-wan-co-get-stats-info.md)OID 请求微型端口驱动程序返回统计信息。

-   CoNDIS WAN 微型端口驱动程序永远不会尝试循环回任何数据包;NDISWAN 提供环回支持。

 


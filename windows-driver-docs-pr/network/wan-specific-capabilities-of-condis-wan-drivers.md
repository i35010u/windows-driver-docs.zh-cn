---
title: CoNDIS WAN 驱动程序的 WAN 特定功能
description: CoNDIS WAN 驱动程序的 WAN 特定功能
ms.assetid: c4e8e0ae-7dd5-4c4e-900a-b1f7e5eecb16
keywords:
- CoNDIS WAN 的驱动程序 WDK 网络，与非 WAN CoNDIS 驱动程序
- 非 WAN CoNDIS 驱动程序 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2079dd4d442fc360a67c5d7075d7a7f083106d41
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384346"
---
# <a name="wan-specific-capabilities-of-condis-wan-drivers"></a>CoNDIS WAN 驱动程序的 WAN 特定功能





WAN 的 CoNDIS 驱动程序不同于非 WAN CoNDIS 驱动程序，如下所示：

-   WAN 的 CoNDIS 支持驱动程序的 TAPI 服务使用产生的 CO\_地址\_系列\_TAPI\_代理地址族。

-   WAN 的 CoNDIS 驱动程序支持特定于 WAN 的 Oid:[OID\_WAN\_永久\_地址](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff561220(v=vs.85))， [OID\_WAN\_当前\_地址](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff561200(v=vs.85))，并[OID\_WAN\_中等\_子类型](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff561216(v=vs.85))。

-   WAN 的 CoNDIS 微型端口驱动程序支持 CoNDIS WAN Oid 到集和查询操作特征的集。 有关的 CoNDIS WAN Oid 的详细信息，请参阅[CoNDIS WAN 对象](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/index)。

-   TAPI 服务提供的 CoNDIS WAN 微型端口驱动程序支持 CoNDIS TAPI Oid 到集和查询操作特征的集。 有关的 CoNDIS TAPI Oid 的详细信息，请参阅[Connection-Oriented ndis TAPI 扩展](https://docs.microsoft.com/windows-hardware/drivers/network/tapi-extension-oids-for-connection-oriented-ndis)。

-   WAN 的 CoNDIS 微型端口驱动程序支持一系列表示链接的状态更改的特定于 WAN 的状态指示。 有关的 CoNDIS WAN 微型端口驱动程序状态指示的详细信息，请参阅[，该值指示的 CoNDIS WAN 微型端口驱动程序状态](indicating-condis-wan-miniport-driver-status.md)。

-   WAN 的 CoNDIS 微型端口驱动程序保持一组特定于 WAN 的统计信息。 [OID\_WAN\_共同\_获取\_统计信息\_信息](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wan-co-get-stats-info)OID 请求要返回的统计信息的微型端口驱动程序。

-   永远不会尝试返回循环; 的任何数据包的 CoNDIS WAN 微型端口驱动程序NDISWAN 提供环回支持。

 

 






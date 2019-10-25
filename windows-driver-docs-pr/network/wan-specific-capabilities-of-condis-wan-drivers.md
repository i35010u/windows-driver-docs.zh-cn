---
title: CoNDIS WAN 驱动程序的 WAN 特定功能
description: CoNDIS WAN 驱动程序的 WAN 特定功能
ms.assetid: c4e8e0ae-7dd5-4c4e-900a-b1f7e5eecb16
keywords:
- CoNDIS WAN 驱动程序，与非 WAN CoNDIS 驱动程序
- 非 WAN CoNDIS 驱动程序 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ee176336f933f34b74eea39586a072b3b57ed7f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842935"
---
# <a name="wan-specific-capabilities-of-condis-wan-drivers"></a>CoNDIS WAN 驱动程序的 WAN 特定功能





CoNDIS WAN 驱动程序不同于非 WAN CoNDIS 驱动程序，如下所示：

-   支持 TAPI 服务的 CoNDIS WAN 驱动程序使用 CO\_地址\_系列\_TAPI\_代理地址系列。

-   CoNDIS WAN 驱动程序支持特定于 WAN 的 Oid： [oid\_wan\_永久\_地址](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff561220(v=vs.85))、 [oid\_wan\_当前\_地址](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff561200(v=vs.85))和[oid\_WAN\_MEDIUM\_子类型](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff561216(v=vs.85))。

-   CoNDIS WAN 微型端口驱动程序支持一组 CoNDIS WAN Oid 来设置和查询操作特征。 有关 CoNDIS WAN Oid 的详细信息，请参阅[CONDIS Wan Objects](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/index)。

-   CoNDIS WAN 微型端口驱动程序提供 TAPI 服务支持一组 CoNDIS TAPI Oid 来设置和查询操作特征。 有关 CoNDIS TAPI Oid 的详细信息，请参阅[面向连接的 NDIS 的 TAPI 扩展](https://docs.microsoft.com/windows-hardware/drivers/network/tapi-extension-oids-for-connection-oriented-ndis)。

-   CoNDIS WAN 微型端口驱动程序支持一组特定于 WAN 的状态指示，表示链接状态的更改。 有关 CoNDIS WAN 微型端口驱动程序状态指示的详细信息，请参阅[指示 CONDIS Wan 微型端口驱动程序状态](indicating-condis-wan-miniport-driver-status.md)。

-   CoNDIS WAN 微型端口驱动程序保留一组特定于 WAN 的统计信息。 [Oid\_WAN\_CO\_获取\_统计信息。\_INFO](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wan-co-get-stats-info) OID 请求微型端口驱动程序返回统计信息。

-   CoNDIS WAN 微型端口驱动程序永远不会尝试循环回任何数据包;NDISWAN 提供环回支持。

 

 






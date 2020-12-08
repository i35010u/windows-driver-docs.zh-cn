---
title: 以太网统计信息 OID
description: 本主题介绍以太网统计信息 Oid
keywords:
- 以太网统计信息 Oid，以太网 NDIS Oid，以太网 Oid WDK，以太网 Oid 网络
ms.date: 11/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a65788d0fce1dd7a6431a573d6f0ab30ff14635
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788451"
---
# <a name="ethernet-statistics-oids"></a>以太网统计信息 OID

下表总结了用于获取网络接口控制器（)  (Nic 的以太网统计信息的 Oid。

| 长度 | 查询 | 设置 | “属性” |
| --- | --- | --- | --- |
| 4 | O |   | [OID_802_3_RCV_OVERRUN](oid-802-3-rcv-overrun.md) |
| 4 | O |   | [OID_802_3_XMIT_DEFERRED](oid-802-3-xmit-deferred.md) |
| 4 | O |   | [OID_802_3_XMIT_HEARTBEAT_FAILURE](oid-802-3-xmit-heartbeat-failure.md) |
| 4 | O |   | [OID_802_3_XMIT_LATE_COLLISIONS](oid-802-3-xmit-late-collisions.md) |
| 4 | O |   | [OID_802_3_XMIT_MAX_COLLISIONS](oid-802-3-xmit-max-collisions.md) |
| 4 | O |   | [OID_802_3_XMIT_TIMES_CRS_LOST](oid-802-3-xmit-times-crs-lost.md) |
| 4 | O |   | [OID_802_3_XMIT_UNDERRUN](oid-802-3-xmit-underrun.md) |

> [!NOTE]
> 以下 Oid 在 NDIS 6.0 和更高版本中已过时：
> - OID_802_3_RCV_ERROR_ALIGNMENT
> - OID_802_3_XMIT_MORE_COLLISIONS
> - OID_802_3_XMIT_ONE_COLLISION


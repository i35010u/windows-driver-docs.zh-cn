---
title: 以太网统计信息 OID
description: 本主题描述以太网的统计信息 Oid
ms.assetid: b38ec79d-d8f3-46fa-9e6f-d42fa18f467c
keywords:
- 以太网统计信息 Oid，网络的以太网 NDIS Oid，以太网 Oid WDK 以太网 Oid
ms.date: 11/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15ca916da71bc065f6110428ed0606807ff817a2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368317"
---
# <a name="ethernet-statistics-oids"></a>以太网统计信息 OID

下表总结了用于获取网络接口控制器 (Nic) 的以太网统计信息的 Oid。

| 长度 | 查询 | 设置 | 名称 |
| --- | --- | --- | --- |
| 4 | O |   | [OID_802_3_RCV_OVERRUN](oid-802-3-rcv-overrun.md) |
| 4 | O |   | [OID_802_3_XMIT_DEFERRED](oid-802-3-xmit-deferred.md) |
| 4 | O |   | [OID_802_3_XMIT_HEARTBEAT_FAILURE](oid-802-3-xmit-heartbeat-failure.md) |
| 4 | O |   | [OID_802_3_XMIT_LATE_COLLISIONS](oid-802-3-xmit-late-collisions.md) |
| 4 | O |   | [OID_802_3_XMIT_MAX_COLLISIONS](oid-802-3-xmit-max-collisions.md) |
| 4 | O |   | [OID_802_3_XMIT_TIMES_CRS_LOST](oid-802-3-xmit-times-crs-lost.md) |
| 4 | O |   | [OID_802_3_XMIT_UNDERRUN](oid-802-3-xmit-underrun.md) |

> [!NOTE]
> 以下 Oid 是过时的 NDIS 6.0 及更高版本：
> - OID_802_3_RCV_ERROR_ALIGNMENT
> - OID_802_3_XMIT_MORE_COLLISIONS
> - OID_802_3_XMIT_ONE_COLLISION


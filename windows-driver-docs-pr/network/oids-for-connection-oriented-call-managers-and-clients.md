---
title: 面向连接的呼叫管理程序和客户端的 OID
description: 本主题介绍面向连接的呼叫管理器和客户端的 Oid。
keywords:
- 面向连接的呼叫管理程序和客户端的 OID
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2496c948df66f1caf48dddff2e25edaa7824c8e2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820562"
---
# <a name="oids-for-connection-oriented-call-managers-and-clients"></a>面向连接的呼叫管理程序和客户端的 OID

下表总结了面向连接的客户端可以发送给呼叫管理器或 MCM 驱动程序的 Oid，以及调用管理器或 MCM 驱动程序可以发送到面向连接的客户端的 Oid。 

在此表中，M 指示 OID 是必需的，而 O 指示它是可选的。

| 长度 | 查询 | 设置 | “属性” |
| --- | --- | --- | --- |
| 多种多样 |   | O | [OID_CO_ADD_ADDRESS](oid-co-add-address.md) |
| 多种多样 |   | O | [OID_CO_ADD_PVC](oid-co-add-pvc.md) |
| 0 |   | O | [OID_CO_ADDRESS_CHANGE](oid-co-address-change.md) |
| 0 |   | M | [OID_CO_AF_CLOSE](oid-co-af-close.md) |
| 多种多样 |   | O | [OID_CO_DELETE_ADDRESS](oid-co-delete-address.md) |
| 多种多样 |   | O | [OID_CO_DELETE_PVC](oid-co-delete-pvc.md) |
| 多种多样 | O |   | [OID_CO_GET_ADDRESSES](oid-co-get-addresses.md) |
|   |   |   | [OID_CO_GET_CALL_INFORMATION](oid-co-get-call-information.md) |
| 0 |   | O | [OID_CO_SIGNALING_DISABLED](oid-co-signaling-disabled.md) |
| 0 |   | O | [OID_CO_SIGNALING_ENABLED](oid-co-signaling-enabled.md) |


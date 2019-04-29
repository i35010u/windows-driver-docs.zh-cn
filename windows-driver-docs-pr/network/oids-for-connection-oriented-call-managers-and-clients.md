---
title: 面向连接的呼叫管理程序和客户端的 OID
description: 本主题介绍用于面向连接的调用管理器和客户端的 Oid。
ms.assetid: a2ffbfd4-a63e-41d1-ab57-0c23661148ca
keywords:
- 面向连接的呼叫管理程序和客户端的 OID
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b0dad3bd79b415aaf73248d1a8d5717557972a1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384223"
---
# <a name="oids-for-connection-oriented-call-managers-and-clients"></a>面向连接的呼叫管理程序和客户端的 OID

下表总结了面向连接的客户端可以发送，以调用管理器或 MCM 驱动程序和该调用管理器或 MCM 驱动程序可以将发送至面向连接的客户端的 Oid。 

在此表中，M 指示 OID 是必需的而 O 则指示它是可选的。

| 长度 | 查询 | 设置 | 名称 |
| --- | --- | --- | --- |
| 变化不定 |   | O | [OID_CO_ADD_ADDRESS](oid-co-add-address.md) |
| 变化不定 |   | O | [OID_CO_ADD_PVC](oid-co-add-pvc.md) |
| 0 |   | O | [OID_CO_ADDRESS_CHANGE](oid-co-address-change.md) |
| 0 |   | M | [OID_CO_AF_CLOSE](oid-co-af-close.md) |
| 变化不定 |   | O | [OID_CO_DELETE_ADDRESS](oid-co-delete-address.md) |
| 变化不定 |   | O | [OID_CO_DELETE_PVC](oid-co-delete-pvc.md) |
| 变化不定 | O |   | [OID_CO_GET_ADDRESSES](oid-co-get-addresses.md) |
|   |   |   | [OID_CO_GET_CALL_INFORMATION](oid-co-get-call-information.md) |
| 0 |   | O | [OID_CO_SIGNALING_DISABLED](oid-co-signaling-disabled.md) |
| 0 |   | O | [OID_CO_SIGNALING_ENABLED](oid-co-signaling-enabled.md) |


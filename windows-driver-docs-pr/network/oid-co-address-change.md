---
title: OID_CO_ADDRESS_CHANGE
description: 本主题介绍 OID_CO_ADDRESS_CHANGE 对象标识符 (OID)。
ms.assetid: 18b185dd-b282-4182-a761-008e5d0c88d7
keywords:
- OID_CO_ADDRESS_CHANGE
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: 057575360289eacbabdac36ca2356e9d91d86382
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555275"
---
# <a name="oidcoaddresschange"></a>OID_CO_ADDRESS_CHANGE

呼叫管理器向呼叫管理器，打开地址族每个客户端发送 OID_CO_ADDRESS_CHANGE OID。 在响应中调用管理器使用的交换机地址的更改会执行此操作。 例如，呼叫管理器发送此请求，如果有人将 NIC 从一台交换机断开连接，插入到另一个交换机。 每个通知客户端必须将 OID_CO_GET_ADDRESSES 查询发送到呼叫管理器，以检索当前有效的地址列表。

呼叫管理器还将 OID_CO_ADDRESS_CHANGE 发送到客户端后客户端与呼叫管理器中打开地址族。 这可确保交换机地址发生更改后，将打开地址族的客户端将收到更改通知。 客户端必须然后必须将发送 OID_CO_GET_ADDRESSES 查询给呼叫管理器。

## <a name="requirements"></a>要求

| | |
| --- | --- |
| 版本 | Windows Vista 及更高版本 |
| 标头 | Ntddndis.h （包括 Ndis.h） |


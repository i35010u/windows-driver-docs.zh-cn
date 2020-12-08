---
title: OID_CO_ADDRESS_CHANGE
description: 本主题介绍) OID_CO_ADDRESS_CHANGE 对象标识符 (OID。
keywords:
- OID_CO_ADDRESS_CHANGE
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: a416fe690d1f37d6f9f0485692a2c50beb3d2f70
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815927"
---
# <a name="oid_co_address_change"></a>OID_CO_ADDRESS_CHANGE

OID_CO_ADDRESS_CHANGE OID 由呼叫管理器发送到使用呼叫管理器打开地址族的每个客户端。 执行此操作是为了响应呼叫管理器使用的交换机地址的更改。 例如，如果某人从一个交换机断开 NIC，并将其插入另一个交换机，则呼叫管理器会发送此请求。 每个已通知客户端必须向呼叫管理器发送 OID_CO_GET_ADDRESSES 查询，以检索当前有效地址的列表。

调用管理器还会在客户端使用呼叫管理器打开地址族后立即将 OID_CO_ADDRESS_CHANGE 发送到客户端。 这可确保在交换机地址更改后打开地址族的客户端会收到更改通知。 然后，客户端必须将 OID_CO_GET_ADDRESSES 查询发送到呼叫管理器。

## <a name="requirements"></a>要求

**版本**： Windows Vista 和更高版本的 **标头**： Ntddndis (包括 Ndis .h) 


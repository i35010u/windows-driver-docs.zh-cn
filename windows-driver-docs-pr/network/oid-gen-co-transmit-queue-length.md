---
title: OID_GEN_CO_TRANSMIT_QUEUE_LENGTH
description: 本主题介绍 OID_GEN_CO_TRANSMIT_QUEUE_LENGTH 对象标识符（OID）。
ms.assetid: bd99e26d-abd4-4b71-8106-e474f61630ff
keywords:
- OID_GEN_CO_TRANSMIT_QUEUE_LENGTH
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: 976b978bb8d69ba95a01e45a1525593a0cf436e4
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917026"
---
# <a name="oid_gen_co_transmit_queue_length"></a>OID_GEN_CO_TRANSMIT_QUEUE_LENGTH

OID_GEN_CO_TRANSMIT_QUEUE_LENGTH OID 指定当前排队等待传输的 Pdu 数量，无论是在 NIC 上还是在驱动程序内部队列中。 返回的数字始终为当前排队的 Pdu 总数，其中可能包括在 NDIS 库中排队的未提交的发送请求。

## <a name="requirements"></a>要求

**版本**： Windows Vista 和更高版本的**标头**： Ntddndis （包括 Ndis .h）


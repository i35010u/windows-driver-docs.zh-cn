---
title: OID_GEN_CO_TRANSMIT_QUEUE_LENGTH
description: 本主题介绍 OID_GEN_CO_TRANSMIT_QUEUE_LENGTH 对象标识符 (OID)。
ms.assetid: bd99e26d-abd4-4b71-8106-e474f61630ff
keywords:
- OID_GEN_CO_TRANSMIT_QUEUE_LENGTH
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: e3a9020c9c1032acc979014be6564533c9b89ab3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386237"
---
# <a name="oidgencotransmitqueuelength"></a>OID_GEN_CO_TRANSMIT_QUEUE_LENGTH

OID_GEN_CO_TRANSMIT_QUEUE_LENGTH OID 指定的 Pdu 数当前正在排队以便传输，无论它们是在 NIC 或驱动程序内部队列中。 始终的 Pdu 总数当前正在排队，后者又可包含未提交的发送请求排队 NDIS 库中返回的数字。

## <a name="requirements"></a>要求

| | |
| --- | --- |
| Version | Windows Vista 及更高版本 |
| Header | Ntddndis.h （包括 Ndis.h） |


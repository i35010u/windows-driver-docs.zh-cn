---
title: 处理 CoNDIS 协议驱动程序中的状态指示
description: 处理 CoNDIS 协议驱动程序中的状态指示
ms.assetid: 948df51b-0561-4b67-b87f-e1652bb18772
keywords:
- 协议驱动程序 WDK 网络，CoNDIS
- NDIS 协议驱动程序 WDK，CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d8bc13179ced21f3a10e187c18da43d8803ccdb0
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211068"
---
# <a name="handling-status-indications-in-a-condis-protocol-driver"></a>处理 CoNDIS 协议驱动程序中的状态指示





协议驱动程序必须提供一个 [**ProtocolCoStatusEx**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_status_ex) 函数，NDIS 在基础驱动程序报告状态时调用该函数。

在基础驱动程序调用状态指示函数 (例如， [**NdisMCoIndicateStatusEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatestatusex)) 时，NDIS 调用了协议驱动程序的*ProtocolCoStatusEx*函数。 有关从微型端口驱动程序指示状态的详细信息，请参阅 [CoNDIS 微型端口驱动程序状态指示](condis-miniport-driver-status-indications.md)。

如果状态指示与 OID 请求关联，则基础驱动程序可以设置[**ndis \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的**DestinationHandle**和**RequestId**成员，其中包含状态信息，以便 ndis 可以向特定协议绑定提供状态指示。 有关 OID 请求的详细信息，请参阅 [CoNDIS Protocol DRIVER OID requests](condis-protocol-driver-oid-requests.md)。

 


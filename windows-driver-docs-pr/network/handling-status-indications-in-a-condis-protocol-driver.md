---
title: 处理 CoNDIS 协议驱动程序中的状态指示
description: 处理 CoNDIS 协议驱动程序中的状态指示
ms.assetid: 948df51b-0561-4b67-b87f-e1652bb18772
keywords:
- 协议驱动程序 WDK 网络的 CoNDIS
- NDIS 协议驱动程序 WDK CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e7a87e0f391e5c7919e388f4e7a569ce9edb73e1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381355"
---
# <a name="handling-status-indications-in-a-condis-protocol-driver"></a>处理 CoNDIS 协议驱动程序中的状态指示





协议驱动程序必须提供[ **ProtocolCoStatusEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_co_status_ex) NDIS 调用时基础驱动程序将状态报告函数。

NDIS 调用协议驱动程序*ProtocolCoStatusEx*函数后基础驱动程序调用的状态指示函数 (例如， [ **NdisMCoIndicateStatusEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcoindicatestatusex)). 指示从微型端口驱动程序状态的详细信息，请参阅[CoNDIS 微型端口驱动程序状态指示](condis-miniport-driver-status-indications.md)。

如果使用 OID 请求相关联的状态指示，则可以设置基础驱动程序**DestinationHandle**并**RequestId**的成员[ **NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)以便 NDIS 可以提供的状态指示特定的协议绑定到包含状态信息的结构。 有关 OID 的请求的详细信息，请参阅[CoNDIS 协议驱动程序 OID 请求](condis-protocol-driver-oid-requests.md)。

 

 






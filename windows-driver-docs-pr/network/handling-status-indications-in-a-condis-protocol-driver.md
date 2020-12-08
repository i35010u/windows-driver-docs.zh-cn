---
title: 处理 CoNDIS 协议驱动程序中的状态指示
description: 处理 CoNDIS 协议驱动程序中的状态指示
keywords:
- 协议驱动程序 WDK 网络，CoNDIS
- NDIS 协议驱动程序 WDK，CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 29ad79ab582a384ba4c90a96edcd310b5cd2e63d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840015"
---
# <a name="handling-status-indications-in-a-condis-protocol-driver"></a>处理 CoNDIS 协议驱动程序中的状态指示





协议驱动程序必须提供一个 [**ProtocolCoStatusEx**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_status_ex) 函数，NDIS 在基础驱动程序报告状态时调用该函数。

在基础驱动程序调用状态指示函数 (例如， [**NdisMCoIndicateStatusEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatestatusex)) 时，NDIS 调用了协议驱动程序的 *ProtocolCoStatusEx* 函数。 有关从微型端口驱动程序指示状态的详细信息，请参阅 [CoNDIS 微型端口驱动程序状态指示](condis-miniport-driver-status-indications.md)。

如果状态指示与 OID 请求关联，则基础驱动程序可以设置 [**ndis \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的 **DestinationHandle** 和 **RequestId** 成员，其中包含状态信息，以便 ndis 可以向特定协议绑定提供状态指示。 有关 OID 请求的详细信息，请参阅 [CoNDIS Protocol DRIVER OID requests](condis-protocol-driver-oid-requests.md)。

 


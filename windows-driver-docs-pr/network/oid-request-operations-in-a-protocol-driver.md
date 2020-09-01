---
title: 协议驱动程序中的 OID 请求操作
description: 协议驱动程序中的 OID 请求操作
ms.assetid: 767252a2-98de-4df2-89dc-ee48b2c7ca9d
keywords:
- 协议驱动程序 WDK 网络，OID 请求
- NDIS 协议驱动程序 WDK，OID 请求
- OID 请求 WDK 网络
- Oid WDK 网络，协议驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e15b5408cbe28ebbc430479bfc42c8f6fa88d236
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206025"
---
# <a name="oid-request-operations-in-a-protocol-driver"></a>协议驱动程序中的 OID 请求操作





在一个协议驱动程序中，OID 请求操作有两个不同的接口。 具有无连接下限的 NDIS 协议驱动程序调用 [**NdisOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest) 函数来启动 OID 请求。 具有无连接下限的 NDIS 协议驱动程序必须提供 [**ProtocolOidRequestComplete**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_oid_request_complete) 函数。 当基础驱动程序完成挂起的 OID 请求时，NDIS 将调用 *ProtocolOidRequestComplete* 。 有关无连接协议驱动程序中 OID 请求的详细信息，请参阅 [协议驱动程序 OID 请求](protocol-driver-oid-requests.md)。

面向连接的 NDIS (CoNDIS) 协议驱动程序调用 [**NdisCoOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest) 函数来启动 OID 请求。 CoNDIS 协议驱动程序必须提供 [**ProtocolCoOidRequestComplete**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_oid_request_complete) 函数。 当基础驱动程序完成挂起的 OID 请求时，NDIS 将调用 *ProtocolOidRequestComplete* 。 有关面向连接的协议驱动程序中 OID 请求的详细信息，请参阅 [面向连接的操作](connection-oriented-operations.md)。

有关 Oid 的详细信息，请参阅 [NDIS oid](/windows-hardware/drivers/ddi/_netvista/)。

 


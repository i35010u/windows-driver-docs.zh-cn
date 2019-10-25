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
ms.openlocfilehash: 45bb1bc83a95e36a36adfa4d7f8b4622b0fef0c9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844004"
---
# <a name="oid-request-operations-in-a-protocol-driver"></a>协议驱动程序中的 OID 请求操作





在一个协议驱动程序中，OID 请求操作有两个不同的接口。 具有无连接下限的 NDIS 协议驱动程序调用[**NdisOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest)函数来启动 OID 请求。 具有无连接下限的 NDIS 协议驱动程序必须提供[**ProtocolOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_oid_request_complete)函数。 当基础驱动程序完成挂起的 OID 请求时，NDIS 将调用*ProtocolOidRequestComplete* 。 有关无连接协议驱动程序中 OID 请求的详细信息，请参阅[协议驱动程序 OID 请求](protocol-driver-oid-requests.md)。

面向连接的 NDIS （CoNDIS）协议驱动程序调用[**NdisCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest)函数以启动 OID 请求。 CoNDIS 协议驱动程序必须提供[**ProtocolCoOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_oid_request_complete)函数。 当基础驱动程序完成挂起的 OID 请求时，NDIS 将调用*ProtocolOidRequestComplete* 。 有关面向连接的协议驱动程序中 OID 请求的详细信息，请参阅[面向连接的操作](connection-oriented-operations.md)。

有关 Oid 的详细信息，请参阅[NDIS oid](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)。

 

 






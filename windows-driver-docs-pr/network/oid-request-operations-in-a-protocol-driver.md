---
title: 协议驱动程序中的 OID 请求操作
description: 协议驱动程序中的 OID 请求操作
ms.assetid: 767252a2-98de-4df2-89dc-ee48b2c7ca9d
keywords:
- 协议驱动程序 WDK 网络、 OID 请求
- NDIS 协议驱动程序 WDK，OID 请求
- OID 请求 WDK 网络
- Oid WDK 网络协议驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: abd82494f48e218f1013a239faf4147b60466a13
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356129"
---
# <a name="oid-request-operations-in-a-protocol-driver"></a>协议驱动程序中的 OID 请求操作





有两个不同接口的 OID 协议驱动程序中的请求操作。 NDIS 协议具有较低的无连接边缘调用的驱动程序[ **NdisOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisoidrequest)函数以初始化 OID 请求。 无连接的下边缘与的 NDIS 协议驱动程序必须提供[ **ProtocolOidRequestComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_oid_request_complete)函数。 NDIS 调用*ProtocolOidRequestComplete*基础驱动程序时完成挂起的 OID 请求。 有关 OID 请求无连接协议驱动程序中的详细信息，请参阅[协议驱动程序 OID 请求](protocol-driver-oid-requests.md)。

面向连接的 NDIS (CoNDIS) 协议驱动程序调用[ **NdisCoOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscooidrequest)函数以初始化 OID 请求。 CoNDIS 协议驱动程序必须提供[ **ProtocolCoOidRequestComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_co_oid_request_complete)函数。 NDIS 调用*ProtocolOidRequestComplete*基础驱动程序时完成挂起的 OID 请求。 有关详细信息的 OID 请求在面向连接的协议驱动程序中，请参阅[Connection-Oriented 操作](connection-oriented-operations.md)。

有关 Oid 的详细信息，请参阅[NDIS Oid](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)。

 

 






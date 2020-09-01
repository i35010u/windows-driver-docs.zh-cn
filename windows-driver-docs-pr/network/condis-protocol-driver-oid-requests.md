---
title: CoNDIS 协议驱动程序 OID 请求
description: CoNDIS 协议驱动程序 OID 请求
ms.assetid: 1338d199-2cd8-430a-a0a5-95aaea04c384
keywords:
- 协议驱动程序 WDK 网络，CoNDIS
- NDIS 协议驱动程序 WDK，CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 68cc2b436ad83bde37c6f05524ab75ce4efbeb5e
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89218473"
---
# <a name="condis-protocol-driver-oid-requests"></a>CoNDIS 协议驱动程序 OID 请求





CoNDIS protocol 驱动程序（客户端或呼叫管理器）可以查询或设置微型端口驱动程序和其他协议驱动程序的操作参数。 CoNDIS 协议驱动程序还可以在 MCMs)  (的小型调用管理器中查询或设置信息。 有关 OID 请求和 MCMs 的详细信息，请参阅 [CONDIS MCM OID requests](condis-mcm-oid-requests.md)。

若要向基础驱动程序发起 OID 请求，协议驱动程序将调用 [**NdisCoOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest) 函数， *并将地址* 族 (AF) 句柄设置为 **NULL**。 若要向另一个 CoNDIS 协议驱动程序发起 OID 请求，协议驱动程序将调用 **NdisCoOidRequest** 并提供有效的 AF 句柄。

在协议驱动程序调用 **NdisCoOidRequest** 函数后，NDIS 将调用另一个驱动程序的 OID 请求函数 (基础驱动程序或其他 CoNDIS 协议驱动程序) 。 对于微型端口驱动程序，NDIS 会调用 [**MiniportCoOidRequest**](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request) 函数。 对于协议驱动程序，NDIS 会调用 [**ProtocolCoOidRequest**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_oid_request) 函数。

下图说明了定向到微型端口驱动程序的 OID 请求。

![说明定向到微型端口驱动程序的 oid 请求的关系图](images/protocolcorequest.png)

下图说明了定向到协议驱动程序的 OID 请求。

![说明定向到协议驱动程序的 oid 请求的关系图](images/clientcorequest.png)

若要同步完成， [**NdisCoOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest) 会返回 NDIS \_ 状态 \_ 成功或错误状态。 若要异步完成， **NdisCoOidRequest** 将返回 NDIS \_ 状态 "挂起" \_ 。

如果**NdisCoOidRequest**返回 NDIS \_ 状态 " \_ 挂起"，则在其他驱动程序通过调用[**NdisMCoOidRequestComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcooidrequestcomplete)函数或[**NDISCOOIDREQUESTCOMPLETE**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequestcomplete)函数完成 OID 请求之后，NDIS 会调用[**ProtocolCoOidRequestComplete**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_oid_request_complete)函数。 在这种情况下，NDIS 会将请求的结果传递到*ProtocolCoOidRequestComplete*的*OidRequest*参数。 NDIS 在*ProtocolCoOidRequestComplete*的*status*参数传递请求的最终状态。

如果[**NdisCoOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest)返回 ndis \_ 状态 \_ SUCCESS，它会在*OidRequest*参数点的[**ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构中返回查询请求的结果。 在这种情况下，NDIS 不会调用 *ProtocolCoOidRequestComplete* 函数。

如果基础驱动程序应将 OID 请求与后续状态指示相关联，则协议驱动程序应在**RequestId** NDIS **RequestHandle** \_ OID 请求结构中设置 RequestId 和 RequestHandle 成员 \_ 。 如果基础驱动程序产生状态指示，则驱动程序将[**ndis \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构中的**requestid**成员设置为从 ndis oid 请求结构的**requestid**成员到 \_ ndis \_ 状态指示结构中的**DestinationHandle**成员到 ndis \_ \_ oid 请求结构的**RequestHandle**成员的值 \_ \_ 的值。

当绑定处于 "正在*重新启动*"、"*正在运行*"、"*暂停*" 或 "已*暂停*" 状态时，驱动程序可以调用[**NdisCoOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest) 。

 


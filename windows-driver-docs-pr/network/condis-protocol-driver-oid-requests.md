---
title: CoNDIS 协议驱动程序 OID 请求
description: CoNDIS 协议驱动程序 OID 请求
ms.assetid: 1338d199-2cd8-430a-a0a5-95aaea04c384
keywords:
- 协议驱动程序 WDK 网络，CoNDIS
- NDIS 协议驱动程序 WDK，CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47e0f9f59d3679634f80fc444b814dc3f36675b1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835086"
---
# <a name="condis-protocol-driver-oid-requests"></a>CoNDIS 协议驱动程序 OID 请求





CoNDIS protocol 驱动程序（客户端或呼叫管理器）可以查询或设置微型端口驱动程序和其他协议驱动程序的操作参数。 CoNDIS 协议驱动程序还可以查询或设置微型端口调用管理器（MCMs）中的信息。 有关 OID 请求和 MCMs 的详细信息，请参阅[CONDIS MCM OID requests](condis-mcm-oid-requests.md)。

若要向基础驱动程序发起 OID 请求，协议驱动程序将调用[**NdisCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest)函数，并将*NdisAfHandle*参数处的地址族（AF）句柄设置为**NULL**。 若要向另一个 CoNDIS 协议驱动程序发起 OID 请求，协议驱动程序将调用**NdisCoOidRequest**并提供有效的 AF 句柄。

在协议驱动程序调用**NdisCoOidRequest**函数后，NDIS 将调用其他驱动程序（基础驱动程序或其他 CoNDIS 协议驱动程序）的 OID 请求函数。 对于微型端口驱动程序，NDIS 会调用[**MiniportCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request)函数。 对于协议驱动程序，NDIS 会调用[**ProtocolCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_oid_request)函数。

下图说明了定向到微型端口驱动程序的 OID 请求。

![说明定向到微型端口驱动程序的 oid 请求的关系图](images/protocolcorequest.png)

下图说明了定向到协议驱动程序的 OID 请求。

![说明定向到协议驱动程序的 oid 请求的关系图](images/clientcorequest.png)

若要同步完成， [**NdisCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest)会返回 NDIS\_状态\_成功或错误状态。 若要异步完成， **NdisCoOidRequest**将\_状态返回 NDIS 状态\_"挂起"。

如果**NdisCoOidRequest**返回 NDIS\_状态\_"挂起"，则在其他驱动程序完成 OID 请求之后， [**Ndis 将调用**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_oid_request_complete) [**NdisMCoOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcooidrequestcomplete)函数或[**NdisCoOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequestcomplete)函数。 在这种情况下，NDIS 会将请求的结果传递到*ProtocolCoOidRequestComplete*的*OidRequest*参数。 NDIS 在*ProtocolCoOidRequestComplete*的*status*参数传递请求的最终状态。

如果[**NdisCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest)\_SUCCESS 返回 NDIS\_状态，它将在*OidRequest*参数点的[**ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构中返回查询请求的结果。 在这种情况下，NDIS 不会调用*ProtocolCoOidRequestComplete*函数。

如果基础驱动程序应将 OID 请求与后续状态指示相关联，则协议驱动程序应将 NDIS 中的**RequestId**和**RequestHandle**成员设置\_OID\_请求结构。 如果基础驱动程序产生状态指示，驱动程序会将 Ndis 中的**requestid**成员[ **\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构设置为 Ndis\_OID 的**REQUESTID**成员的值\_请求NDIS 中的结构和**DestinationHandle**成员\_状态\_指示结构从 NDIS\_OID 的**REQUESTHANDLE**成员\_请求结构的值。

当绑定处于 "正在*重新启动*"、"*正在运行*"、"*暂停*" 或 "已*暂停*" 状态时，驱动程序可以调用[**NdisCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest) 。

 

 






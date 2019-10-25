---
title: CoNDIS MCM OID 请求
description: CoNDIS MCM OID 请求
ms.assetid: efddbcb0-98f1-4cd3-9707-f3ed17c20181
keywords:
- 微型端口呼叫管理器 WDK 网络，OID 请求
- MCMs WDK 网络，OID 请求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4fe8b5ebb15fd440f923f9511a7180ef4bc703c2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835154"
---
# <a name="condis-mcm-oid-requests"></a>CoNDIS MCM OID 请求





与其他 CoNDIS 调用管理器一样，微型端口调用管理器（MCMs）可以查询或设置 CoNDIS 客户端驱动程序的操作参数。 CoNDIS 客户端驱动程序可以查询或设置 MCM 的调用管理器参数或微型端口驱动程序参数。

若要向 CoNDIS 客户端驱动程序发起 OID 请求，MCM 会调用[**NdisMCmOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmoidrequest)函数。

下图说明了 MCM 产生的 OID 请求。

![说明 mcm 所源自的 oid 请求的关系图](images/mcmcorequest.png)

MCM 驱动程序调用[**NdisMCmOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmoidrequest)函数后，NDIS 将调用客户端驱动程序的[**ProtocolCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_oid_request)函数。

若要同步完成， **NdisMCmOidRequest**会返回 NDIS\_状态\_成功或错误状态。 若要异步完成， **NdisMCmOidRequest**将\_状态返回 NDIS 状态\_"挂起"。

如果[**NdisMCmOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmoidrequest)返回 NDIS\_状态\_挂起，ndis[**会在客户**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_oid_request_complete)端驱动程序通过调用[**NdisCoOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequestcomplete)才能. 在这种情况下，NDIS 会将请求的结果传递到*ProtocolCoOidRequestComplete*的*OidRequest*参数。 NDIS 在*ProtocolCoOidRequestComplete*的*status*参数传递请求的最终状态。

如果**NdisMCmOidRequest**\_SUCCESS 返回 NDIS\_状态，它将在*OidRequest*参数的[**ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构中返回查询请求的结果。 在这种情况下，NDIS 不调用 MCM 的*ProtocolCoOidRequestComplete*函数。

CoNDIS 客户端驱动程序可以查询或设置 MCMs 的 "呼叫管理器" 操作参数或微型端口操作参数。 若要发起对 MCM 调用管理器参数的 OID 请求，客户端将调用[**NdisCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest)函数并在*NdisAfHandle*参数处提供有效的地址族（AF）句柄。 若要为 MCM 微型端口参数发起 OID 请求，客户端将调用**NdisCoOidRequest**函数并将 AF 句柄设置为**NULL**。

在客户端调用**NdisCoOidRequest**函数后，NDIS 会调用[**MINIPORTCOOIDREQUEST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request)函数或 MCM 驱动程序的[**ProtocolCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_oid_request)函数。

下图说明了 MCM 的微型端口参数的 OID 请求。

![阐释 mcm 的微型端口参数的 oid 请求的关系图](images/protocol2mcmcorequest.png)

下图说明了 MCM 的调用管理器参数的 OID 请求。

![演示对 mcm 的调用管理器参数的 oid 请求的关系图](images/client2mcmcorequest.png)

若要同步完成， [**NdisCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest)会返回 NDIS\_状态\_成功或错误状态。 若要异步完成， [**ProtocolCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_oid_request)或[**MINIPORTCOOIDREQUEST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request)将返回 NDIS\_状态\_"挂起"。

如果*ProtocolCoOidRequest*或**MininportCoOidRequest**返回 NDIS\_状态\_挂起，ndis 将在 MCM 完成 OID 请求后调用客户端的[**ProtocolCoOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_oid_request_complete)函数，方法是调用[**NdisMCoOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcooidrequestcomplete)或[**NdisMCmOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmoidrequestcomplete)函数。 在这种情况下，NDIS 会将请求的结果传递到*ProtocolCoOidRequestComplete*的*OidRequest*参数。 NDIS 在*ProtocolCoOidRequestComplete*的*status*参数传递请求的最终状态。

如果[**NdisCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest)\_SUCCESS 返回 NDIS\_状态，它将在*OidRequest*参数的[**ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构中返回查询请求的结果。 在这种情况下，NDIS 不调用客户端的*ProtocolCoOidRequestComplete*函数。

 

 






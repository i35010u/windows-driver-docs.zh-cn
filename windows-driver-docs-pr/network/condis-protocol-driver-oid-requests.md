---
title: CoNDIS 协议驱动程序 OID 请求
description: CoNDIS 协议驱动程序 OID 请求
ms.assetid: 1338d199-2cd8-430a-a0a5-95aaea04c384
keywords:
- 协议驱动程序 WDK 网络的 CoNDIS
- NDIS 协议驱动程序 WDK CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8037f19e8a537ea226c40cc36025d258762f8cac
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385113"
---
# <a name="condis-protocol-driver-oid-requests"></a>CoNDIS 协议驱动程序 OID 请求





CoNDIS 协议驱动程序，客户端或调用管理器中，可以查询或设置操作参数的微型端口驱动程序和其他协议驱动程序。 CoNDIS 协议驱动程序还可使用查询或调用管理器 (MCMs) 中微型端口设置的信息。 有关 OID 的请求和 MCMs 的详细信息，请参阅[CoNDIS MCM OID 请求](condis-mcm-oid-requests.md)。

来自对基础驱动程序的 OID 请求，协议驱动程序调用[ **NdisCoOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscooidrequest)函数，并在设置地址系列 (AF) 句柄， *NdisAfHandle*参数为**NULL**。 打出到另一个的 CoNDIS 协议驱动程序的 OID 请求，协议驱动程序调用**NdisCoOidRequest** ，并提供有效的 AF 句柄。

协议驱动程序调用后**NdisCoOidRequest**函数，NDIS 调用 OID request 函数的其他驱动程序 （基础驱动程序或另一个的 CoNDIS 协议驱动程序）。 有关微型端口驱动程序，调用 NDIS [ **MiniportCoOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_co_oid_request)函数。 有关协议驱动程序，调用 NDIS [ **ProtocolCoOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_co_oid_request)函数。

下图说明了定向到微型端口驱动程序的 OID 请求。

![说明的 oid 请求定向到微型端口驱动程序的关系图](images/protocolcorequest.png)

下图说明了定向到协议驱动程序的 OID 请求。

![说明的 oid 请求定向到协议驱动程序的关系图](images/clientcorequest.png)

若要以同步方式，完成[ **NdisCoOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscooidrequest)返回 NDIS\_状态\_成功或错误状态。 若要以异步方式完成**NdisCoOidRequest**返回 NDIS\_状态\_PENDING。

如果**NdisCoOidRequest**返回 NDIS\_状态\_挂起、 NDIS 调用[ **ProtocolCoOidRequestComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_co_oid_request_complete)函数之后，其他驱动程序将通过调用完成 OID 请求[ **NdisMCoOidRequestComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcooidrequestcomplete)函数或[ **NdisCoOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscooidrequestcomplete)函数。 NDIS 在这种情况下，将在请求的结果传递*OidRequest*的参数*ProtocolCoOidRequestComplete*。 NDIS 将传递在请求的最终状态*状态*的参数*ProtocolCoOidRequestComplete*。

如果[ **NdisCoOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscooidrequest)返回 NDIS\_状态\_成功后，它将返回的结果中的查询请求[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构，在*OidRequest*参数所指向。 在这种情况下，未调用 NDIS *ProtocolCoOidRequestComplete*函数。

如果基础驱动程序应将与后续状态指示关联 OID 请求，应设置协议驱动程序**RequestId**并**RequestHandle** NDIS 中的成员\_OID\_请求结构。 如果基础驱动程序的状态指示，驱动程序设置**RequestId**中的成员[ **NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)结构中的值**RequestId**成员的 NDIS\_OID\_请求结构并**DestinationHandle**中 NDIS成员\_状态\_中的值指示结构**RequestHandle** NDIS 成员\_OID\_请求结构。

驱动程序可以调用[ **NdisCoOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscooidrequest)绑定正在*正在重新启动*，*运行*，*暂停*，或*已暂停*状态。

 

 






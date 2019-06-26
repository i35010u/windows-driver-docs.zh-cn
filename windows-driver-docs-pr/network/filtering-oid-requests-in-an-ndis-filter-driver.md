---
title: 在 NDIS 筛选器驱动程序中筛选 OID 请求
description: 在 NDIS 筛选器驱动程序中筛选 OID 请求
ms.assetid: 88bb8318-f19c-4d98-bb06-6120e6adb51d
keywords:
- Oid WDK 网络筛选器驱动程序
- 筛选 OID 请求中筛选器驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ecb6d34d40b620b1a2305d659805e15a253be507
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353333"
---
# <a name="filtering-oid-requests-in-an-ndis-filter-driver"></a>在 NDIS 筛选器驱动程序中筛选 OID 请求





筛选器驱动程序可以处理由过量驱动程序产生的 OID 请求。 NDIS 调用[ *FilterOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_oid_request)函数来处理每个 OID 请求。 筛选器驱动程序可以 OID 将请求转发到基础驱动程序通过调用[ **NdisFOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfoidrequest)函数。

NDIS 可以调用筛选器驱动程序[ *FilterCancelOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_cancel_oid_request)函数取消 OID 请求。 当调用 NDIS *FilterCancelOidRequest*，筛选器驱动程序应尝试调用[ **NdisFOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfoidrequest)函数越早越好。

下图说明了已筛选的 OID 请求。

![说明筛选的 oid 请求的关系图](images/requestfilter.png)

筛选器驱动程序可以完成 OID 请求，以同步方式还是以异步方式通过返回 NDIS\_状态\_成功或 NDIS\_状态\_PENDING，分别从[ *FilterOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_oid_request)。 *FilterOidRequest*可以还使用了错误状态以同步方式完成。

已成功处理的 OID 集请求的筛选器驱动程序必须设置**SupportedRevision**中的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)在从 OID 集请求返回的结构。 **SupportedRevision**成员通知有关哪些修订 OID 请求的发起方支持的驱动程序。 在 NDIS 结构中的版本信息有关的详细信息，请参阅[指定 NDIS 版本信息](specifying-ndis-version-information.md)。

如果*FilterOidRequest*返回 NDIS\_状态\_挂起状态，它必须调用[ **NdisFOidRequestComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfoidrequestcomplete)函数完成后OID 请求。 在这种情况下，驱动程序通过在请求的结果*OidRequest*的参数**NdisFOidRequestComplete**。 驱动程序通过在请求的最终状态*状态*的参数**NdisFOidRequestComplete**。

如果*FilterOidRequest*返回 NDIS\_状态\_成功后，它将返回的结果中的查询请求[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构，在*OidRequest*参数。 在这种情况下，该驱动程序不会调用**NdisFOidRequestComplete**函数。

OID 请求转发到基础驱动程序，筛选器驱动程序调用[ **NdisFOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfoidrequest)函数。 如果不应将请求转发到基础驱动程序，则筛选器驱动程序可以立即完成的请求。 若要完成没有转发的请求，则驱动程序可以返回 NDIS\_状态\_成功 （或错误状态），从*FilterOidRequest*，也可以调用**NdisFOidRequestComplete**后返回 NDIS\_状态\_PENDING。

**请注意**  驱动程序调用之前[ **NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfoidrequest)，该驱动程序必须分配[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构，并将请求信息传输到新的结构，通过调用[ **NdisAllocateCloneOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocatecloneoidrequest)。

 

转发的请求将继续由筛选器驱动程序发起的请求相同。 有关详细信息，请参阅[NDIS 筛选器驱动程序从生成 OID 请求](generating-oid-requests-from-an-ndis-filter-driver.md)。

基础驱动程序完成转发的请求后，筛选器驱动程序可以修改该响应，如有必要，并将其传递给过量驱动程序。

筛选器驱动程序可以接收来自过量驱动程序中时的 OID 请求*正在重新启动*，*运行*，*暂停*，或者*已暂停*状态。

**请注意**  微型端口驱动程序，如筛选器驱动程序可以接收只有一个 OID 请求一次。 NDIS 序列化到筛选器模块发送的请求，因为不能在调用筛选器驱动程序*FilterOidRequest*完成上一个请求之前。

 

下面是修改 OID 请求的筛选器驱动程序的示例：

-   筛选器驱动程序添加标头。 在此情况下，该驱动程序收到的响应的查询后[OID\_代\_最大\_帧\_大小](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-maximum-frame-size)从基础驱动程序，该筛选器中减去其标头的大小从响应中。 该驱动程序中减去其标头大小，因为驱动程序将插入前面每个发送数据包的标头，并在每个接收的数据包中移除的标头。

 

 






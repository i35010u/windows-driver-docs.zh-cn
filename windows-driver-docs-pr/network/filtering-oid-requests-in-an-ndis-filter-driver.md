---
title: 在 NDIS 筛选器驱动程序中筛选 OID 请求
description: 在 NDIS 筛选器驱动程序中筛选 OID 请求
ms.assetid: 88bb8318-f19c-4d98-bb06-6120e6adb51d
keywords:
- Oid WDK 网络，筛选器驱动程序
- 筛选筛选器驱动程序中的 OID 请求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0bba02584bf99913d22c01681e08fff486e1c03
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840490"
---
# <a name="filtering-oid-requests-in-an-ndis-filter-driver"></a>在 NDIS 筛选器驱动程序中筛选 OID 请求





筛选器驱动程序可以处理由过量驱动程序生成的 OID 请求。 NDIS 调用[*FilterOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_oid_request)函数来处理每个 OID 请求。 筛选器驱动程序可以通过调用[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)函数，将 OID 请求转发到基础驱动程序。

NDIS 可以调用筛选器驱动程序的[*FilterCancelOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_cancel_oid_request)函数来取消 OID 请求。 当 NDIS 调用*FilterCancelOidRequest*时，筛选器驱动程序应尽快尝试调用[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)函数。

下图说明了一个筛选的 OID 请求。

![说明已筛选 oid 请求的关系图](images/requestfilter.png)

筛选器驱动程序可以通过从[*FilterOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_oid_request)返回 NDIS\_状态\_SUCCESS 或 NDIS\_状态\_挂起，来同步或异步完成 OID 请求。 *FilterOidRequest*也可以通过错误状态同步完成。

成功处理 OID 集请求的筛选器驱动程序必须在从 OID 集请求返回时在[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构中设置**SupportedRevision**成员。 **SupportedRevision**成员向发起方通知请求驱动程序所支持的修订版本。 有关 NDIS 结构中的版本信息的详细信息，请参阅[指定 Ndis 版本信息](specifying-ndis-version-information.md)。

如果*FilterOidRequest*返回 NDIS\_状态\_"挂起"，则必须在完成 OID 请求后调用[**NdisFOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequestcomplete)函数。 在这种情况下，驱动程序会在**NdisFOidRequestComplete**的*OidRequest*参数传递请求的结果。 驱动程序通过**NdisFOidRequestComplete**的*status*参数传递请求的最终状态。

如果*FilterOidRequest*\_SUCCESS 返回 NDIS\_状态，它将在*OidRequest*参数的[**ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构中返回查询请求的结果。 在这种情况下，驱动程序不会调用**NdisFOidRequestComplete**函数。

若要将 OID 请求转发到底层驱动程序，筛选器驱动程序将调用[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)函数。 如果不应将请求转发到底层驱动程序，筛选器驱动程序可以立即完成请求。 若要在不转发的情况下完成请求，驱动程序可以从*FilterOidRequest*返回 NDIS\_状态\_成功（或错误状态），也可以在返回 NDIS\_状态后调用**NdisFOidRequestComplete**\_未.

**注意**  在驱动程序调用[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)之前，驱动程序必须通过调用[**NdisAllocateCloneOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatecloneoidrequest)将[**NDIS\_OID 分配\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构，并将请求信息传输到新的结构。

 

转发的请求继续与筛选器驱动程序启动的请求相同。 有关详细信息，请参阅[从 NDIS 筛选器驱动程序生成 OID 请求](generating-oid-requests-from-an-ndis-filter-driver.md)。

底层驱动程序完成转发的请求后，筛选器驱动程序可以修改响应（如有必要），并将其传递给过量驱动程序。

筛选器驱动程序可以在其处于*重新启动*、*正在运行*、*暂停*或*暂停*状态时接收来自过量驱动程序的 OID 请求。

**请注意**，  （如微型端口驱动程序），筛选器驱动程序一次只能接收一个 OID 请求。 因为 NDIS 序列化发送到筛选器模块的请求，所以在完成前一个请求之前，不能在*FilterOidRequest*上调用筛选器驱动程序。

 

下面是修改 OID 请求的筛选器驱动程序的示例：

-   筛选器驱动程序添加标头。 在这种情况下，当驱动程序收到对[OID\_GEN\_最大\_帧\_大小](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-maximum-frame-size)从底层驱动程序的查询的响应后，筛选器将从响应中减去其标头的大小。 驱动程序将其标头大小减至最小，因为驱动程序会在每个发送的数据包前面插入标头，并删除每个接收的数据包中的标头

 

 






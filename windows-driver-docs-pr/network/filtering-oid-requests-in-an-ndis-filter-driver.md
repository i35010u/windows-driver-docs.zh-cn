---
title: 在 NDIS 筛选器驱动程序中筛选 OID 请求
description: 在 NDIS 筛选器驱动程序中筛选 OID 请求
keywords:
- Oid WDK 网络，筛选器驱动程序
- 筛选筛选器驱动程序中的 OID 请求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c4d454a0991562f70a53abf8d215f43ae1ef5ca
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102249291"
---
# <a name="filtering-oid-requests-in-an-ndis-filter-driver"></a>在 NDIS 筛选器驱动程序中筛选 OID 请求





筛选器驱动程序可以处理由过量驱动程序生成的 OID 请求。 NDIS 调用 [*FilterOidRequest*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_oid_request) 函数来处理每个 OID 请求。 筛选器驱动程序可以通过调用 [**NdisFOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest) 函数，将 OID 请求转发到基础驱动程序。

NDIS 可以调用筛选器驱动程序的 [*FilterCancelOidRequest*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_cancel_oid_request) 函数来取消 OID 请求。 当 NDIS 调用 *FilterCancelOidRequest* 时，筛选器驱动程序应尽快尝试调用 [**NdisFOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest) 函数。

下图说明了一个筛选的 OID 请求。

![说明已筛选 oid 请求的关系图](images/requestfilter.png)

筛选器驱动程序可以通过 \_ \_ 分别从 FILTEROIDREQUEST 返回 ndis 状态成功或 ndis \_ 状态 \_ "挂起[](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_oid_request)" 或 "ndis 状态"，来同步或异步完成 OID 请求。 *FilterOidRequest* 也可以通过错误状态同步完成。

成功处理 OID 集请求的筛选器驱动程序必须在从 OID 集请求返回时在 [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构中设置 **SupportedRevision** 成员。 **SupportedRevision** 成员向发起方通知请求驱动程序所支持的修订版本。 有关 NDIS 结构中的版本信息的详细信息，请参阅 [指定 Ndis 版本信息](specifying-ndis-version-information.md)。

如果 *FilterOidRequest* 返回 NDIS \_ 状态 " \_ 挂起"，则必须在完成 OID 请求后调用 [**NdisFOidRequestComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequestcomplete) 函数。 在这种情况下，驱动程序会在 **NdisFOidRequestComplete** 的 *OidRequest* 参数传递请求的结果。 驱动程序通过 **NdisFOidRequestComplete** 的 *status* 参数传递请求的最终状态。

如果 *FilterOidRequest* 返回 ndis \_ 状态 \_ 成功，它会在 *OidRequest* 参数的 [**ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构中返回查询请求的结果。 在这种情况下，驱动程序不会调用 **NdisFOidRequestComplete** 函数。

若要将 OID 请求转发到底层驱动程序，筛选器驱动程序将调用 [**NdisFOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest) 函数。 如果不应将请求转发到底层驱动程序，筛选器驱动程序可以立即完成请求。 若要在不转发的情况下完成请求，驱动程序可以 \_ 从 FilterOidRequest 返回 ndis 状态 \_ 成功 (或) 状态，也可以在返回 ndis 状态 "挂起" 后调用 **NdisFOidRequestComplete** \_ \_ 。

**注意**  驱动程序调用 [**NdisFOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)之前，驱动程序必须分配一个 [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request) 结构，并通过调用 [**NdisAllocateCloneOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatecloneoidrequest)将请求信息传输到新的结构。

 

转发的请求继续与筛选器驱动程序启动的请求相同。 有关详细信息，请参阅 [从 NDIS 筛选器驱动程序生成 OID 请求](generating-oid-requests-from-an-ndis-filter-driver.md)。

底层驱动程序完成转发的请求后，筛选器驱动程序可以修改响应（如有必要），并将其传递给过量驱动程序。

筛选器驱动程序可以在其处于 *重新启动*、 *正在运行*、 *暂停* 或 *暂停* 状态时接收来自过量驱动程序的 OID 请求。

**注意**  与微型端口驱动程序一样，筛选器驱动程序一次只能接收一个 OID 请求。 因为 NDIS 序列化发送到筛选器模块的请求，所以在完成前一个请求之前，不能在 *FilterOidRequest* 上调用筛选器驱动程序。

 

下面是修改 OID 请求的筛选器驱动程序的示例：

-   筛选器驱动程序添加标头。 在这种情况下，当驱动程序收到对来自底层驱动程序的 [OID 生成 \_ \_ 最大 \_ 帧 \_ 大小](./oid-gen-maximum-frame-size.md) 的查询响应后，筛选器将从响应中减去其标头的大小。 驱动程序将其标头大小减至最小，因为驱动程序会在每个发送的数据包前面插入标头，并删除每个接收的数据包中的标头

 


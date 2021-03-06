---
title: 从 NDIS 筛选器驱动程序生成 OID 请求
description: 从 NDIS 筛选器驱动程序生成 OID 请求
keywords:
- Oid WDK 网络，筛选器驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 631c3449e5f4c4f974db9d931c21985c656959f2
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248227"
---
# <a name="generating-oid-requests-from-an-ndis-filter-driver"></a>从 NDIS 筛选器驱动程序生成 OID 请求





筛选器驱动程序可以通过调用 [**NdisFOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest) 函数来发起 OID 查询或设置对基础驱动程序的请求。

下图说明了由筛选器驱动程序生成的 OID 请求。

![说明由筛选器驱动程序生成的 oid 请求的关系图](images/filterrequest.png)

筛选器驱动程序调用 [**NdisFOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest) 函数后，NDIS 会调用下一底层驱动程序的请求函数。 有关微型端口驱动程序如何处理 OID 请求的详细信息，请参阅 [对适配器的 Oid 请求](miniport-adapter-oid-requests.md)。

若要同步完成， [**NdisFOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest) 会返回 NDIS \_ 状态 \_ 成功或错误状态。 若要异步完成， **NdisFOidRequest** 将返回 NDIS \_ 状态 "挂起" \_ 。

若要确定基础驱动程序成功处理的信息，则发出 OID 请求的筛选器驱动程序必须在 \_ \_ OID 请求返回后，在 NDIS OID 请求结构中检查 SupportedRevision 成员中的值。 有关 NDIS 版本信息的详细信息，请参阅 [指定 Ndis 版本信息](specifying-ndis-version-information.md)。

如果 [**NdisFOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest) 返回 NDIS \_ 状态 " \_ 挂起"，则在基础驱动程序完成 OID 请求后，NDIS 会调用 [*FilterOidRequestComplete*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_oid_request_complete) 函数。 在这种情况下，NDIS 会将请求的结果传递到 *FilterOidRequestComplete* 的 *OidRequest* 参数。 NDIS 在 *FilterOidRequestComplete* 的 *status* 参数传递请求的最终状态。

如果 [**NdisFOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)返回 ndis \_ 状态 \_ 成功，它会在 *OidRequest* 参数的 [**ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构中返回查询请求的结果。 在这种情况下，NDIS 不会调用 [*FilterOidRequestComplete*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_oid_request_complete) 函数。

当驱动程序处于 *重新启动*、*正在运行*、*暂停* 或 *暂停* 状态时，它可以调用 [**NdisFOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest) 。

**注意**  筛选器驱动程序应跟踪它所源自的 OID 请求，并确保在完成此类请求后，它不会调用 [**NdisFOidRequestComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequestcomplete) 函数。

 

 


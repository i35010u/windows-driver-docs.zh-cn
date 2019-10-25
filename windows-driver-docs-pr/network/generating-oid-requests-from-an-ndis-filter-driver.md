---
title: 从 NDIS 筛选器驱动程序生成 OID 请求
description: 从 NDIS 筛选器驱动程序生成 OID 请求
ms.assetid: 6567bf98-bf56-4337-8670-af4c78d2c947
keywords:
- Oid WDK 网络，筛选器驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: da0623e57bd66bd265fd579cb889384f54288ea5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842185"
---
# <a name="generating-oid-requests-from-an-ndis-filter-driver"></a>从 NDIS 筛选器驱动程序生成 OID 请求





筛选器驱动程序可以通过调用[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)函数来发起 OID 查询或设置对基础驱动程序的请求。

下图说明了由筛选器驱动程序生成的 OID 请求。

![说明由筛选器驱动程序生成的 oid 请求的关系图](images/filterrequest.png)

筛选器驱动程序调用[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)函数后，NDIS 会调用下一底层驱动程序的请求函数。 有关微型端口驱动程序如何处理 OID 请求的详细信息，请参阅[对适配器的 Oid 请求](miniport-adapter-oid-requests.md)。

若要同步完成， [**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)会返回 NDIS\_状态\_成功或错误状态。 若要异步完成， **NdisFOidRequest**将\_状态返回 NDIS 状态\_"挂起"。

若要确定基础驱动程序成功处理的信息，则发出 OID 请求的筛选器驱动程序必须在 SupportedRevision 成员中的成员中检查\_请求结构\_中的值。返回. 有关 NDIS 版本信息的详细信息，请参阅[指定 Ndis 版本信息](specifying-ndis-version-information.md)。

如果[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)返回 NDIS\_状态\_挂起，则在基础驱动程序完成 OID 请求后，ndis 将调用[*FilterOidRequestComplete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_oid_request_complete)函数。 在这种情况下，NDIS 会将请求的结果传递到*FilterOidRequestComplete*的*OidRequest*参数。 NDIS 在*FilterOidRequestComplete*的*status*参数传递请求的最终状态。

如果[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)\_SUCCESS 返回 NDIS\_状态，它将在*OidRequest*参数的[**ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构中返回查询请求的结果。 在这种情况下，NDIS 不会调用[*FilterOidRequestComplete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_oid_request_complete)函数。

当驱动程序处于*重新启动*、*正在运行*、*暂停*或*暂停*状态时，它可以调用[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest) 。

**请注意**  筛选器驱动程序应跟踪它所源自的 OID 请求，并确保在完成此类请求后，它不会调用[**NdisFOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequestcomplete)函数。

 

 

 






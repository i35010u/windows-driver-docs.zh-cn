---
title: 从 NDIS 协议驱动程序生成 OID 请求
description: 从 NDIS 协议驱动程序生成 OID 请求
ms.assetid: a27d1c9c-fc7e-414f-8cad-595e8d8fe8f8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd264775b9ebeca08eb4056749fd219c56766881
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207607"
---
# <a name="generating-oid-requests-from-an-ndis-protocol-driver"></a>从 NDIS 协议驱动程序生成 OID 请求





若要向底层驱动程序发起 OID 请求，协议将调用 [**NdisOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest) 函数。

下图说明了由协议驱动程序生成的 OID 请求。

![说明由协议驱动程序发起的 oid 请求的关系图](images/protocolrequest.png)

在协议驱动程序调用 [**NdisOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest) 函数后，NDIS 会调用下一底层驱动程序的请求函数。 有关微型端口驱动程序如何处理 OID 请求的详细信息，请参阅 [对适配器的 Oid 请求](miniport-adapter-oid-requests.md)。 有关筛选器驱动程序如何处理 OID 请求的详细信息，请参阅 [筛选器模块 OID 请求](filter-module-oid-requests.md)。

若要同步完成， **NdisOidRequest** 会返回 NDIS \_ 状态 \_ 成功或错误状态。 若要异步完成， **NdisOidRequest** 将返回 NDIS \_ 状态 "挂起" \_ 。

如果 **NdisOidRequest** 返回 NDIS \_ 状态 " \_ 挂起"，则在基础驱动程序完成 OID 请求后，NDIS 会调用 [**ProtocolOidRequestComplete**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_oid_request_complete) 函数。 在这种情况下，NDIS 会将请求的结果传递到*ProtocolOidRequestComplete*的*OidRequest*参数。 NDIS 在*ProtocolOidRequestComplete*的*status*参数传递请求的最终状态。

如果**NdisOidRequest**返回 ndis \_ 状态 \_ 成功，它会在*OidRequest*参数的[**ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构中返回查询请求的结果。 在这种情况下，NDIS 不会调用 *ProtocolOidRequestComplete* 函数。

若要确定基础驱动程序成功处理的信息，发出 OID 请求的协议驱动程序必须在**SupportedRevision** \_ \_ OID 请求返回后，在 NDIS OID 请求结构中检查 SupportedRevision 成员中的值。 有关 NDIS 版本信息的详细信息，请参阅 [指定 Ndis 版本信息](specifying-ndis-version-information.md)。

如果基础驱动程序应将 OID 请求与后续状态指示相关联，则协议驱动程序应在**RequestId** NDIS \_ OID 请求结构中设置 RequestId 成员 \_ 。 当基础驱动程序发出状态指示时，它会将[**NDIS \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构中的**RequestId**成员设置为 OID 请求中提供的值。

当绑定处于 "正在*重新启动*"、"*正在运行*"、"*暂停*" 或 "已*暂停*" 状态时，驱动程序可以调用**NdisOidRequest** 。

 


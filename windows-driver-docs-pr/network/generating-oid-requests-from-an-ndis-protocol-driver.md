---
title: 从 NDIS 协议驱动程序生成 OID 请求
description: 从 NDIS 协议驱动程序生成 OID 请求
ms.assetid: a27d1c9c-fc7e-414f-8cad-595e8d8fe8f8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd3a85ce6e319ac687303d5ad199d0c1e0ce7c33
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842183"
---
# <a name="generating-oid-requests-from-an-ndis-protocol-driver"></a>从 NDIS 协议驱动程序生成 OID 请求





若要向底层驱动程序发起 OID 请求，协议将调用[**NdisOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest)函数。

下图说明了由协议驱动程序生成的 OID 请求。

![说明由协议驱动程序发起的 oid 请求的关系图](images/protocolrequest.png)

在协议驱动程序调用[**NdisOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest)函数后，NDIS 会调用下一底层驱动程序的请求函数。 有关微型端口驱动程序如何处理 OID 请求的详细信息，请参阅[对适配器的 Oid 请求](miniport-adapter-oid-requests.md)。 有关筛选器驱动程序如何处理 OID 请求的详细信息，请参阅[筛选器模块 OID 请求](filter-module-oid-requests.md)。

若要同步完成， **NdisOidRequest**会返回 NDIS\_状态\_成功或错误状态。 若要异步完成， **NdisOidRequest**将\_状态返回 NDIS 状态\_"挂起"。

如果**NdisOidRequest**返回 NDIS\_状态\_挂起，则在基础驱动程序完成 OID 请求后，ndis 将调用[**ProtocolOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_oid_request_complete)函数。 在这种情况下，NDIS 会将请求的结果传递到*ProtocolOidRequestComplete*的*OidRequest*参数。 NDIS 在*ProtocolOidRequestComplete*的*status*参数传递请求的最终状态。

如果**NdisOidRequest**\_SUCCESS 返回 NDIS\_状态，它将在*OidRequest*参数的[**ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构中返回查询请求的结果。 在这种情况下，NDIS 不会调用*ProtocolOidRequestComplete*函数。

若要确定基础驱动程序已成功处理的信息，发出 OID 请求的协议驱动程序必须在 SupportedRevision 成员中的成员\_中检查\_请求结构中的值。返回. 有关 NDIS 版本信息的详细信息，请参阅[指定 Ndis 版本信息](specifying-ndis-version-information.md)。

如果基础驱动程序应将 OID 请求与后续状态指示相关联，则协议驱动程序应将 NDIS 中的**RequestId**成员设置\_OID\_请求结构。 当基础驱动程序发出状态指示时，它会将 NDIS 中的**RequestId**成员[ **\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构设置为 OID 请求中提供的值。

当绑定处于 "正在*重新启动*"、"*正在运行*"、"*暂停*" 或 "已*暂停*" 状态时，驱动程序可以调用**NdisOidRequest** 。

 

 






---
title: 处理微型端口适配器中的 OID 请求
description: 处理微型端口适配器中的 OID 请求
ms.assetid: 0819ef06-5715-4814-a1ed-ddc757728ec4
keywords:
- 微型端口驱动程序 WDK 网络，OID 请求
- Oid WDK 网络，微型端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eed5e5b7764959e68835f58974c1406f76f6ecf6
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211089"
---
# <a name="handling-oid-requests-in-a-miniport-adapter"></a>处理微型端口适配器中的 OID 请求





NDIS 调用微型端口驱动程序的 [*MiniportOidRequest*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request) 函数来提交 OID 请求，以查询或设置驱动程序中的信息。 NDIS 自行或代表调用[**NdisOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest)或[**NdisFOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)函数的过量驱动程序调用*MiniportOidRequest*函数。

NDIS 传递 *MiniportOidRequest* 一个指针，该指针指向包含请求信息的 [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request) 结构。 请求结构包含 OID \_ Xxx 标识符，该标识符指示请求的类型以及用于定义请求数据的其他成员。

Timeout 成员指定请求的超时 **值** （以秒为单位）。 如果超时在驱动程序完成请求之前过期，NDIS 可以重置驱动程序或取消请求。

**RequestId**成员指定请求的可选标识符。 微型端口驱动程序可以将状态指示的 **requestid** 成员设置为从关联 OID 请求的 **requestid** 成员获取的值。 通常，微型端口驱动程序可以忽略此成员。 如果驱动程序必须设置此成员，则特定 OID 的 "引用" 页将提供所需的值。 有关状态指示的详细信息，请参阅 [适配器状态指示](miniport-adapter-status-indications.md)。

成功处理 OID 集请求的微型端口驱动程序必须在从 OID 集请求返回时在[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构中设置**SupportedRevision**成员。 **SupportedRevision**成员向发起方通知驱动程序所支持的修订版本。 例如，微型端口驱动程序可以创建 Xxx \_ 版本 \_ 2 结构，提供适合于 Xxx \_ 版本1结构的值 \_ ，并使用零填充结构的其余部分。 微型端口驱动程序会 \_ \_ 在 **SupportedRevision** 成员中报告 Xxx 版本1。 在这种情况下，可以支持 Xxx 版本2的协议驱动程序 \_ \_ 将使用 \_ \_ 微型端口驱动程序支持的 xxx 版本1信息。 有关 NDIS 结构中的版本信息的详细信息，请参阅 [指定 Ndis 版本信息](specifying-ndis-version-information.md)。

微型端口驱动程序可以通过返回成功或失败状态来同步完成 OID 请求。

微型端口驱动程序可以通过返回 NDIS 状态 "挂起" 来异步完成 OID 请求 \_ \_ 。 在这种情况下，微型端口驱动程序必须调用 [**NdisMOidRequestComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete) 函数来完成该操作。

如果 *MiniportOidRequest* 返回 NDIS \_ 状态 \_ "挂起"，则在完成挂起的请求之前，NDIS 不会调用 *MiniportOidRequest* 的另一个请求。

NDIS 可以调用微型端口驱动程序的 [*MiniportCancelOidRequest*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_oid_request) 函数来取消 OID 请求。

 


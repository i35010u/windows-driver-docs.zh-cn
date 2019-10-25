---
title: 处理微型端口适配器中的 OID 请求
description: 处理微型端口适配器中的 OID 请求
ms.assetid: 0819ef06-5715-4814-a1ed-ddc757728ec4
keywords:
- 微型端口驱动程序 WDK 网络，OID 请求
- Oid WDK 网络，微型端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2bf869c2f8e395dfe3cc38196c82bd8567ffd840
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842574"
---
# <a name="handling-oid-requests-in-a-miniport-adapter"></a>处理微型端口适配器中的 OID 请求





NDIS 调用微型端口驱动程序的[*MiniportOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)函数来提交 OID 请求，以查询或设置驱动程序中的信息。 NDIS 自行或代表调用[**NdisOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest)或[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)函数的过量驱动程序调用*MiniportOidRequest*函数。

NDIS 将*MiniportOidRequest*指针传递到包含请求信息的[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构。 请求结构包含 OID\_Xxx 标识符，它指示请求的类型以及用于定义请求数据的其他成员。

Timeout 成员指定请求的超时**值**（以秒为单位）。 如果超时在驱动程序完成请求之前过期，NDIS 可以重置驱动程序或取消请求。

**RequestId**成员指定请求的可选标识符。 微型端口驱动程序可以将状态指示的**requestid**成员设置为从关联 OID 请求的**requestid**成员获取的值。 通常，微型端口驱动程序可以忽略此成员。 如果驱动程序必须设置此成员，则特定 OID 的 "引用" 页将提供所需的值。 有关状态指示的详细信息，请参阅[适配器状态指示](miniport-adapter-status-indications.md)。

成功处理 OID 集请求的微型端口驱动程序必须在从 OID 集请求返回时在[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构中设置**SupportedRevision**成员。 **SupportedRevision**成员向发起方通知驱动程序所支持的修订版本。 例如，微型端口驱动程序可以创建 Xxx\_修订版\_2 结构，提供适用于 Xxx\_修订版\_1 结构的值，并使用零填充结构的其余部分。 小型端口驱动程序会在**SupportedRevision**成员中报告 XXX\_修订版\_1。 在这种情况下，可以支持\_修订版\_2 的协议驱动程序将使用支持微型端口驱动程序的 Xxx\_修订版\_1 信息。 有关 NDIS 结构中的版本信息的详细信息，请参阅[指定 Ndis 版本信息](specifying-ndis-version-information.md)。

微型端口驱动程序可以通过返回成功或失败状态来同步完成 OID 请求。

微型端口驱动程序可以通过返回 NDIS\_状态\_挂起来异步完成 OID 请求。 在这种情况下，微型端口驱动程序必须调用[**NdisMOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)函数来完成该操作。

如果*MiniportOidRequest*返回 NDIS\_状态\_"挂起"，则在完成挂起的请求之前，NDIS 不*会调用适配器*的其他请求。

NDIS 可以调用微型端口驱动程序的[*MiniportCancelOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_oid_request)函数来取消 OID 请求。

 

 






---
title: CoNDIS 微型端口驱动程序 OID 请求
description: CoNDIS 微型端口驱动程序 OID 请求
keywords:
- 微型端口驱动程序 WDK 网络，CoNDIS
- NDIS 微型端口驱动程序 WDK，CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 33553962888bc295f77c73f65b136186710552be
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248587"
---
# <a name="condis-miniport-driver-oid-requests"></a>CoNDIS 微型端口驱动程序 OID 请求





NDIS 调用 CoNDIS 微型端口驱动程序的 [**MiniportCoOidRequest**](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request) 函数来提交 OID 请求，以查询或设置驱动程序中的信息。 NDIS *MiniportCoOidRequest* 代表或代表称为 [**NdisCoOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest) 函数的过量驱动程序调用。

NDIS 传递 *MiniportCoOidRequest* 一个指针，该指针指向包含请求信息的 [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request) 结构。 请求结构包含 OID \_ *Xxx* 标识符，该标识符指示请求的类型以及用于定义请求数据的其他成员。

Timeout 成员指定请求的超时 **值** （以秒为单位）。 如果超时在驱动程序完成请求之前过期，NDIS 可以重置驱动程序或取消请求。

**RequestId** 成员指定请求的可选标识符。 微型端口驱动程序可以将状态指示的 **RequestId** 成员设置为该驱动程序从关联 OID 请求的 **requestid** 成员那里获得的值。 通常，微型端口驱动程序可以忽略此成员。 如果驱动程序必须设置此成员，则驱动程序必须使用在特定 OID 的 "引用" 页中指定的其中一个必需值。 有关状态指示的详细信息，请参阅 [CoNDIS 微型端口驱动程序状态指示](condis-miniport-driver-status-indications.md)。

微型端口驱动程序可以通过返回成功或失败状态来同步完成 OID 请求。 驱动程序可以通过返回 NDIS 状态 "挂起" 来异步完成 OID 请求 \_ \_ 。 在这种情况下，驱动程序必须调用 [**NdisMCoOidRequestComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcooidrequestcomplete) 函数来完成该操作。

如果 *MiniportCoOidRequest* 函数返回 NDIS \_ 状态 \_ "挂起"，则在完成挂起的请求之前，NDIS 可以调用 *MiniportCoOidRequest* 的另一个请求。 应注意，这不同于对所有 OID 请求进行序列化的无连接 NDIS 接口。

NDIS 可以调用微型端口驱动程序的 [*MiniportCancelOidRequest*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_oid_request) 函数来取消 CoNDIS OID 请求。

 


---
title: CoNDIS 微型端口驱动程序 OID 请求
description: CoNDIS 微型端口驱动程序 OID 请求
ms.assetid: a283d430-f90c-4704-868b-f4086922737b
keywords:
- 微型端口驱动程序 WDK 网络的 CoNDIS
- NDIS 微型端口驱动程序 WDK CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ae657f4877940b44d9e737dbb9266709732f9a4d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379239"
---
# <a name="condis-miniport-driver-oid-requests"></a>CoNDIS 微型端口驱动程序 OID 请求





NDIS 调用的 CoNDIS 微型端口驱动程序的[ **MiniportCoOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_co_oid_request)函数提交 OID 请求查询或驱动程序中设置的信息。 NDIS 调用*MiniportCoOidRequest*代表其自身或代表名为基础驱动程序[ **NdisCoOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscooidrequest)函数。

将传递 NDIS *MiniportCoOidRequest*指向的指针[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构，其中包含请求信息。 请求结构包含 OID\_*Xxx*指示请求和其他成员定义的请求数据的类型的标识符。

**超时**成员指定一个超时，以秒为单位的请求。 NDIS 可以重置该驱动程序，或如果超时到期之前驱动程序完成请求取消请求。

**RequestId**成员指定为请求的可选标识符。 微型端口驱动程序可以设置**RequestId**驱动程序从获取的值的状态指示成员**RequestId**相关联的 OID 请求的成员。 通常情况下，微型端口驱动程序可以忽略此成员。 如果驱动程序必须设置此成员，该驱动程序必须使用一个特定的 OID 的参考页中指定所需值。 有关状态指示的详细信息，请参阅[CoNDIS 微型端口驱动程序状态指示](condis-miniport-driver-status-indications.md)。

微型端口驱动程序可以通过返回成功或失败状态以同步方式完成的 OID 请求。 该驱动程序可以以异步方式完成的 OID 请求，通过返回 NDIS\_状态\_PENDING。 在这种情况下，该驱动程序必须调用[ **NdisMCoOidRequestComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcooidrequestcomplete)函数来完成该操作。

如果*MiniportCoOidRequest*函数将返回 NDIS\_状态\_挂起状态，可以调用 NDIS *MiniportCoOidRequest*与另一个请求之前适配器挂起在请求完成。 您应注意这一点与其中序列化 OID 的所有请求的无连接的 NDIS 接口不同。

NDIS 可以调用微型端口驱动程序[ *MiniportCancelOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_cancel_oid_request)函数可以取消的 CoNDIS OID 请求。

 

 






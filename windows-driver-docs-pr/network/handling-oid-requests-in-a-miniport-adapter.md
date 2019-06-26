---
title: 处理微型端口适配器中的 OID 请求
description: 处理微型端口适配器中的 OID 请求
ms.assetid: 0819ef06-5715-4814-a1ed-ddc757728ec4
keywords:
- 微型端口驱动程序 WDK 网络、 OID 请求
- Oid WDK 网络，微型端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e4fe95a9af11595e2d4d80333ec1d7df5ca29f78
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379785"
---
# <a name="handling-oid-requests-in-a-miniport-adapter"></a>处理微型端口适配器中的 OID 请求





NDIS 调用微型端口驱动程序[ *MiniportOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_oid_request)函数提交 OID 请求查询或驱动程序中设置的信息。 NDIS 调用*MiniportOidRequest*代表其自身或代表的基础驱动程序调用的函数[ **NdisOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisoidrequest)或[ **NdisFOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfoidrequest)函数。

将传递 NDIS *MiniportOidRequest*指向的指针[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构，其中包含请求信息。 请求结构包含 OID\_Xxx 标识符，该值指示请求和其他成员定义的请求数据的类型。

**超时**成员指定一个超时，以秒为单位的请求。 NDIS 可以重置该驱动程序，或如果超时到期之前驱动程序完成请求取消请求。

**RequestId**成员指定为请求的可选标识符。 微型端口驱动程序可以设置**RequestId**成员为从获取值的状态指示**RequestId**相关联的 OID 请求的成员。 通常情况下，微型端口驱动程序可以忽略此成员。 如果驱动程序必须设置此成员，特定的 OID 的参考页提供了所需的值。 有关状态指示的详细信息，请参阅[适配器状态指示](miniport-adapter-status-indications.md)。

已成功处理的 OID 集请求的微型端口驱动程序必须设置**SupportedRevision**中的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)从此 OID 集请求返回时的结构。 **SupportedRevision**成员会通知驱动程序支持的修订版本的请求的发起程序。 例如，微型端口驱动程序可以创建 Xxx\_修订\_2 结构，提供适用于 Xxx 的值\_修订\_1 结构和填充了零结构的其余部分。 微型端口驱动程序会报告 Xxx\_修订\_中的 1 **SupportedRevision**成员。 在此情况下，一个协议驱动程序，可支持 Xxx\_修订\_2 将使用 Xxx\_修订\_1 微型端口驱动程序支持的信息。 在 NDIS 结构中的版本信息有关的详细信息，请参阅[指定 NDIS 版本信息](specifying-ndis-version-information.md)。

微型端口驱动程序可以通过返回成功或失败状态以同步方式完成的 OID 请求。

微型端口驱动程序可以以异步方式完成的 OID 请求，通过返回 NDIS\_状态\_PENDING。 在这种情况下，微型端口驱动程序必须调用[ **NdisMOidRequestComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismoidrequestcomplete)函数来完成该操作。

如果*MiniportOidRequest*返回 NDIS\_状态\_挂起状态，不会调用 NDIS *MiniportOidRequest*与另一个请求之前的挂起请求的适配器已完成。

NDIS 可以调用微型端口驱动程序[ *MiniportCancelOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_cancel_oid_request)函数取消 OID 请求。

 

 






---
title: 设置无连接微型端口驱动程序的信息
description: 设置无连接微型端口驱动程序的信息
ms.assetid: 406d844a-cc83-4cd6-a2d2-78e614aab900
keywords:
- 无连接驱动程序 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c4fa72085c28b1e5961d6cbc6be9c4f83492346
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375158"
---
# <a name="setting-information-for-a-connectionless-miniport-driver"></a>设置无连接微型端口驱动程序的信息





若要设置的无连接的微型端口驱动程序维护的 OID，绑定的协议调用[ **NdisOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisoidrequest) ，并将传递[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构，它指定的对象 (OID) 正被查询的和，它指向包含该对象应设置为值的缓冲区。 在调用**NdisOidRequest** NDIS 调用微型端口驱动程序将导致[ *MiniportOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_oid_request)函数，这将设置与所提供的值的对象。

在调用*MiniportOidRequest*可以同步或异步完成。 若要以异步方式完成的调用，微型端口驱动程序调用[ **NdisMOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismoidrequestcomplete)。 下图说明了设置信息 （每个绑定） 的无连接的微型端口驱动程序中。

![说明 （每个绑定） 的无连接的微型端口驱动程序中的设置信息的关系图](images/fig5-4.png)

 

 






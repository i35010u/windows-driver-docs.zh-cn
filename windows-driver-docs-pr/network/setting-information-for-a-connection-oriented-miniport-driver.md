---
title: 设置面向连接的微型端口驱动程序的信息
description: 设置面向连接的微型端口驱动程序的信息
ms.assetid: e31d2054-5982-4ba5-a9e9-133c0d4ed875
keywords:
- 面向连接的驱动程序 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc1a11d6877be8450840d405e1543ad6b8eab38a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375148"
---
# <a name="setting-information-for-a-connection-oriented-miniport-driver"></a>设置面向连接的微型端口驱动程序的信息





若要设置一个面向连接的微型端口驱动程序维护的 OID，绑定的协议调用[ **NdisCoOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscooidrequest) ，并将传递[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构，它指定的对象 (OID) 正被查询的和，它指向包含该对象应设置为值的缓冲区。 在调用**NdisCoOidRequest** NDIS 调用微型端口驱动程序将导致[ **MiniportCoOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_co_oid_request)函数，这将设置与所提供的值的对象。

在调用**NdisCoOidRequest**可以同步或异步完成。 若要以异步方式完成的调用，微型端口驱动程序调用[ **NdisCoOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscooidrequestcomplete)。 下图演示了面向连接的微型端口驱动程序中的设置信息。

![说明面向连接的微型端口驱动程序中的设置信息的关系图](images/fig5-3.png)

 

 






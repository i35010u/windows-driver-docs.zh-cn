---
title: 设置面向连接的微型端口驱动程序的信息
description: 设置面向连接的微型端口驱动程序的信息
keywords:
- 面向连接的驱动程序 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b018b0c4a408609f34f5df6793cd4243db3d0e8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795885"
---
# <a name="setting-information-for-a-connection-oriented-miniport-driver"></a>设置面向连接的微型端口驱动程序的信息





若要设置面向连接的微型端口驱动程序维护的 OID，绑定协议将调用 [**NdisCoOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest) ，并传递 [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request) 结构，该结构指定正在查询的对象 (OID) ，并指向包含应设置对象的值的缓冲区。 对 **NdisCoOidRequest** 的调用会使 NDIS 调用微型端口驱动程序的 [**MiniportCoOidRequest**](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request) 函数，该函数将对象设置为提供的值。

对 **NdisCoOidRequest** 的调用可同步或异步完成。 若要异步完成调用，微型端口驱动程序将调用 [**NdisCoOidRequestComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequestcomplete)。 下图说明了面向连接的微型端口驱动程序中的设置信息。

![说明面向连接的微型端口驱动程序中的设置信息的关系图](images/fig5-3.png)

 


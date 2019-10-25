---
title: 设置面向连接的微型端口驱动程序的信息
description: 设置面向连接的微型端口驱动程序的信息
ms.assetid: e31d2054-5982-4ba5-a9e9-133c0d4ed875
keywords:
- 面向连接的驱动程序 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e8be8e0180e640ab4a41a9ee139f3a1dd187a1a5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841944"
---
# <a name="setting-information-for-a-connection-oriented-miniport-driver"></a>设置面向连接的微型端口驱动程序的信息





若要设置面向连接的微型端口驱动程序维护的 OID，绑定协议将调用[**NdisCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest)并将[**NDIS\_OID 传递\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构，该结构指定正在查询的对象（OID），并指向缓冲区，其中包含应设置对象的值。 对**NdisCoOidRequest**的调用会使 NDIS 调用微型端口驱动程序的[**MiniportCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request)函数，该函数将对象设置为提供的值。

对**NdisCoOidRequest**的调用可同步或异步完成。 若要异步完成调用，微型端口驱动程序将调用[**NdisCoOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequestcomplete)。 下图说明了面向连接的微型端口驱动程序中的设置信息。

![说明面向连接的微型端口驱动程序中的设置信息的关系图](images/fig5-3.png)

 

 






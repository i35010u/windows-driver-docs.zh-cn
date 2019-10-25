---
title: 设置无连接微型端口驱动程序的信息
description: 设置无连接微型端口驱动程序的信息
ms.assetid: 406d844a-cc83-4cd6-a2d2-78e614aab900
keywords:
- 无连接驱动程序 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 96da894b88fa723ed6e5e3b5080dca66e4b087f4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841942"
---
# <a name="setting-information-for-a-connectionless-miniport-driver"></a>设置无连接微型端口驱动程序的信息





若要设置无连接微型端口驱动程序维护的 OID，绑定协议将调用[**NdisOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest) ，并将[**NDIS\_OID 传递\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构，该结构指定正在查询的对象（OID），并指向缓冲区，它包含应将对象设置为的值。 对**NdisOidRequest**的调用会使 NDIS 调用微型端口驱动程序的[*MiniportOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)函数，该函数将对象设置为提供的值。

对*MiniportOidRequest*的调用可同步或异步完成。 若要异步完成调用，微型端口驱动程序将调用[**NdisMOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)。 下图说明了如何在无连接微型端口驱动程序中设置信息（每个绑定）。

![演示如何在无连接微型端口驱动程序中设置信息的示意图（每个绑定）](images/fig5-4.png)

 

 






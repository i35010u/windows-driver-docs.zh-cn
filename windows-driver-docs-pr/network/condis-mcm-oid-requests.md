---
title: CoNDIS MCM OID 请求
description: CoNDIS MCM OID 请求
ms.assetid: efddbcb0-98f1-4cd3-9707-f3ed17c20181
keywords:
- 微型端口调用管理器 WDK 网络、 OID 请求
- MCMs WDK 网络、 OID 请求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: acb7bbd1f0b49740783a344976bc6c1ba4c89e65
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344315"
---
# <a name="condis-mcm-oid-requests"></a>CoNDIS MCM OID 请求





其他的 CoNDIS 调用管理器，如微型端口调用管理器 (MCMs) 可使用查询或设置操作参数的 CoNDIS 客户端驱动程序。 CoNDIS 客户端驱动程序可使用查询或设置调用管理器参数或 MCM 的微型端口驱动程序参数。

来自对 CoNDIS 客户端驱动程序的 OID 请求，MCM，请调用[ **NdisMCmOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff563548)函数。

下图说明了 MCM 发起的 OID 请求。

![说明 mcm 发起的 oid 请求的关系图](images/mcmcorequest.png)

MCM 驱动程序调用后[ **NdisMCmOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff563548)函数、 NDIS 调用[ **ProtocolCoOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff570254)的客户端函数驱动程序。

若要以同步方式，完成**NdisMCmOidRequest**返回 NDIS\_状态\_成功或错误状态。 若要以异步方式完成**NdisMCmOidRequest**返回 NDIS\_状态\_PENDING。

如果[ **NdisMCmOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff563548)返回 NDIS\_状态\_挂起、 NDIS 调用[ **ProtocolCoOidRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff570255)函数后的客户端驱动程序通过调用完成 OID 请求 MCM [ **NdisCoOidRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff561716)函数。 NDIS 在这种情况下，将在请求的结果传递*OidRequest*的参数*ProtocolCoOidRequestComplete*。 NDIS 将传递在请求的最终状态*状态*的参数*ProtocolCoOidRequestComplete*。

如果**NdisMCmOidRequest**返回 NDIS\_状态\_成功后，它将返回的结果中的查询请求[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构，在*OidRequest*参数。 在这种情况下，未调用 NDIS *ProtocolCoOidRequestComplete* MCM 的函数。

CoNDIS 客户端驱动程序可使用查询或调用管理器操作参数或微型端口操作参数的 MCMs 设置。 打出 MCM 调用管理器参数的 OID 请求，在客户端调用[ **NdisCoOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561711)函数，并提供有效的地址系列 (AF) 句柄在*NdisAfHandle*参数。 打出 MCM 微型端口参数的 OID 请求，在客户端调用**NdisCoOidRequest**函数，并设置 AF 句柄**NULL**。

在客户端调用后**NdisCoOidRequest**函数，NDIS 调用任一[ **MiniportCoOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff559362)函数或[ **ProtocolCoOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff570254) MCM 驱动程序的函数。

下图说明了 MCM 的微型端口参数的 OID 请求。

![说明 mcm 的微型端口参数的 oid 请求的关系图](images/protocol2mcmcorequest.png)

下图说明了 MCM 的调用管理器参数的 OID 请求。

![说明 mcm 的调用管理器参数的 oid 请求的关系图](images/client2mcmcorequest.png)

若要以同步方式，完成[ **NdisCoOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561711)返回 NDIS\_状态\_成功或错误状态。 若要以异步方式完成[ **ProtocolCoOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff570254)或[ **MiniportCoOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff559362)返回 NDIS\_状态\_PENDING。

如果*ProtocolCoOidRequest*或**MininportCoOidRequest**返回 NDIS\_状态\_挂起、 NDIS 调用[ **ProtocolCoOidRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff570255) MCM 完成 OID 请求通过调用后的客户端函数[ **NdisMCoOidRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563568)或[ **NdisMCmOidRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563551)函数。 NDIS 在这种情况下，将在请求的结果传递*OidRequest*的参数*ProtocolCoOidRequestComplete*。 NDIS 将传递在请求的最终状态*状态*的参数*ProtocolCoOidRequestComplete*。

如果[ **NdisCoOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561711)返回 NDIS\_状态\_成功后，它将返回的结果中的查询请求[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构，在*OidRequest*参数。 在这种情况下，NDIS 不调用客户端*ProtocolCoOidRequestComplete*函数。

 

 






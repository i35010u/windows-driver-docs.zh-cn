---
title: 从 NDIS 筛选器驱动程序生成 OID 请求
description: 从 NDIS 筛选器驱动程序生成 OID 请求
ms.assetid: 6567bf98-bf56-4337-8670-af4c78d2c947
keywords:
- Oid WDK 网络筛选器驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a42b1496e4539e05477b333be2bf9a3cb7b2894
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349904"
---
# <a name="generating-oid-requests-from-an-ndis-filter-driver"></a>从 NDIS 筛选器驱动程序生成 OID 请求





筛选器驱动程序可以发起 OID 查询或将请求设置为基础驱动程序，通过调用[ **NdisFOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561830)函数。

下图说明了由筛选器驱动程序产生的 OID 请求。

![说明由筛选器驱动程序产生的 oid 请求的关系图](images/filterrequest.png)

筛选器驱动程序调用后[ **NdisFOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561830)函数，NDIS 调用下一步基础驱动程序的请求功能。 有关微型端口驱动程序如何处理 OID 请求的详细信息，请参阅[适配器的 OID 请求](miniport-adapter-oid-requests.md)。

若要以同步方式，完成[ **NdisFOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561830)返回 NDIS\_状态\_成功或错误状态。 若要以异步方式完成**NdisFOidRequest**返回 NDIS\_状态\_PENDING。

若要确定哪些信息已成功处理由基础驱动程序发出 OID 的筛选器驱动程序的请求必须检查值**SupportedRevision**成员在 NDIS\_OID\_请求OID 请求返回的结构。 NDIS 版本信息有关的详细信息，请参阅[指定 NDIS 版本信息](specifying-ndis-version-information.md)。

如果[ **NdisFOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561830)返回 NDIS\_状态\_挂起、 NDIS 调用[ *FilterOidRequestComplete* ](https://msdn.microsoft.com/library/windows/hardware/ff549956)函数后基础驱动程序完成 OID 请求。 NDIS 在这种情况下，将在请求的结果传递*OidRequest*的参数*FilterOidRequestComplete*。 NDIS 将传递在请求的最终状态*状态*的参数*FilterOidRequestComplete*。

如果[ **NdisFOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561830)返回 NDIS\_状态\_成功后，它将返回的结果中的查询请求[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构，在*OidRequest*参数。 在这种情况下，未调用 NDIS [ *FilterOidRequestComplete* ](https://msdn.microsoft.com/library/windows/hardware/ff549956)函数。

驱动程序可以调用[ **NdisFOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561830)当它处于*正在重新启动*，*运行*，*暂停*，或*已暂停*状态。

**请注意**  筛选器驱动程序应跟踪的源自的 OID 请求并确保它不会调用[ **NdisFOidRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff561833)函数时此类请求已完成。

 

 

 






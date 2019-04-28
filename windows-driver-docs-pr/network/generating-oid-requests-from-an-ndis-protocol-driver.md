---
title: 从 NDIS 协议驱动程序生成 OID 请求
description: 从 NDIS 协议驱动程序生成 OID 请求
ms.assetid: a27d1c9c-fc7e-414f-8cad-595e8d8fe8f8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba05cb659bf9ae9ec87b28112152974e81fa22fd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349905"
---
# <a name="generating-oid-requests-from-an-ndis-protocol-driver"></a>从 NDIS 协议驱动程序生成 OID 请求





来自对基础驱动程序的 OID 请求，一种协议，请调用[ **NdisOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff563710)函数。

下图说明了由协议驱动程序产生的 OID 请求。

![说明由协议驱动程序产生的 oid 请求的关系图](images/protocolrequest.png)

协议驱动程序调用后[ **NdisOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff563710)函数，NDIS 调用下一步基础驱动程序的请求功能。 有关微型端口驱动程序如何处理 OID 请求的详细信息，请参阅[适配器的 OID 请求](miniport-adapter-oid-requests.md)。 有关筛选器驱动程序如何处理 OID 请求的详细信息，请参阅[筛选器模块 OID 请求](filter-module-oid-requests.md)。

若要以同步方式，完成**NdisOidRequest**返回 NDIS\_状态\_成功或错误状态。 若要以异步方式完成**NdisOidRequest**返回 NDIS\_状态\_PENDING。

如果**NdisOidRequest**返回 NDIS\_状态\_挂起、 NDIS 调用[ **ProtocolOidRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff570264)函数的后面基础驱动程序完成 OID 请求。 NDIS 在这种情况下，将在请求的结果传递*OidRequest*的参数*ProtocolOidRequestComplete*。 NDIS 将传递在请求的最终状态*状态*的参数*ProtocolOidRequestComplete*。

如果**NdisOidRequest**返回 NDIS\_状态\_成功后，它将返回的结果中的查询请求[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构，在*OidRequest*参数。 在这种情况下，未调用 NDIS *ProtocolOidRequestComplete*函数。

若要确定哪些信息已成功处理由基础驱动程序发出 OID 的协议驱动程序的请求必须检查值**SupportedRevision**成员在 NDIS\_OID\_请求OID 请求返回的结构。 NDIS 版本信息有关的详细信息，请参阅[指定 NDIS 版本信息](specifying-ndis-version-information.md)。

如果基础驱动程序应将与后续状态指示关联 OID 请求，应设置协议驱动程序**RequestId**成员在 NDIS\_OID\_请求结构。 当基础驱动程序发出的状态指示时，它会设置**RequestId**中的成员[ **NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)结构OID 请求中提供的值。

驱动程序可以调用**NdisOidRequest**绑定正在*正在重新启动*，*运行*，*暂停*，或*已暂停*状态。

 

 






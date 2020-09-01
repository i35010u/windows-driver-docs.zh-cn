---
title: 中间驱动程序查询和设置操作
description: 中间驱动程序查询和设置操作
ms.assetid: 68576241-20c1-4df4-ab2e-20ab89e67763
keywords:
- 中间驱动程序 WDK 网络，查询操作
- NDIS 中间驱动程序 WDK，查询操作
- 中间驱动程序 WDK 网络，设置操作
- NDIS 中间驱动程序 WDK，设置操作
- 查询操作 WDK NDIS 中间
- 设置操作 WDK NDIS 中间
- Oid WDK 网络，中间驱动程序查询和集
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 968647059e76452b48fb3e7d314e9131325fbbc1
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215622"
---
# <a name="intermediate-driver-query-and-set-operations"></a>中间驱动程序查询和设置操作





在成功绑定到基础微型端口适配器并初始化其虚拟微型端口后，中间驱动程序将查询基础微型端口适配器的操作特征并设置其自己的内部状态。 如果适合，中间驱动程序还会将此类参数作为与基础微型端口适配器的绑定的预测缓冲区大小进行协商。 与基础微型端口适配器关联的大多数属性都将传递到[*ProtocolBindAdapterEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)函数的*BindParameters*参数中的中间驱动程序。 中间驱动程序应使用传递给 *ProtocolBindAdapterEx*的值（如果可能），而不是发出 OID 查询。 但是，具有无连接下限的中间驱动程序可以通过调用 [**NdisOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest)发出 OID 查询。 具有面向连接的下边缘的中间驱动程序可以通过调用 [**NdisCoOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest)发出 OID 查询。

中间驱动程序还可以从更高级别的驱动程序通过其 [*MiniportOidRequest*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request) 函数接收查询和设置请求。 驱动程序可以对这些请求做出响应或将它们向下传递到底层驱动程序。 中间驱动程序对查询和集的响应方式取决于实现。

**注意**   中间驱动程序的行为也可能受到虚拟微型端口和基础微型端口驱动程序的电源状态的影响。 若要了解有关查询和设置操作的电源状态的效果的详细信息，请参阅 [处理集电源请求](handling-a-set-power-request.md)。

 

"网络参考" 部分包含有关常规、面向连接的、nonmedia 特定的 Oid 以及中间驱动程序开发人员所需的特定于媒体的 Oid 的信息。

以下主题提供有关发出和响应中间驱动程序中的查询和集的其他信息：

[从中间驱动程序发出设置和查询请求](issuing-set-and-query-requests-from-an-intermediate-driver.md)

[在中间驱动程序中响应设置和查询请求](responding-to-sets-and-queries-in-an-intermediate-driver.md)

 


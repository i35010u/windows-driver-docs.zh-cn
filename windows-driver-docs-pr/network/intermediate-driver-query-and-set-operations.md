---
title: 中间驱动程序查询和设置操作
description: 中间驱动程序查询和设置操作
ms.assetid: 68576241-20c1-4df4-ab2e-20ab89e67763
keywords:
- 中间驱动程序 WDK 网络，查询操作
- NDIS 中间层驱动程序 WDK、 查询操作
- 中间驱动程序 WDK 网络，集合操作
- NDIS 中间层驱动程序 WDK，集合操作
- 查询操作 WDK NDIS 中间
- 集运算 WDK NDIS 中间
- Oid WDK 网络、 中间驱动程序查询和设置
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 81343b88aac5279865f3e7dc8101696ba39b470d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385253"
---
# <a name="intermediate-driver-query-and-set-operations"></a>中间驱动程序查询和设置操作





它已成功绑定到基础的微型端口适配器并初始化其虚拟微型端口后，中间驱动程序查询操作基础的微型端口适配器的特征，并设置其自己的内部状态。 如果适用，中间驱动程序还协商与基础的微型端口适配器绑定的预测先行缓冲区大小作为此类参数。 大多数与基础的微型端口适配器相关联的属性传递给中间驱动程序在*BindParameters*的参数[ *ProtocolBindAdapterEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_bind_adapter_ex)函数。 中间驱动程序应使用的值传递给*ProtocolBindAdapterEx*，如果可能，而不是发出 OID 查询。 但是，使用无连接的下边缘中间驱动程序可以发出 OID 查询通过调用[ **NdisOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisoidrequest)。 使用面向连接的下边缘中间驱动程序可以通过调用发出 OID 查询[ **NdisCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscooidrequest)。

中间的驱动程序还可以接收查询并将请求设置为从更高级别驱动程序通过其[ *MiniportOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_oid_request)函数。 该驱动程序可以响应这些请求，或将其传递到基础驱动程序。 中间的驱动程序如何响应查询和集取决于实现。

**请注意**  中间驱动程序的行为也会受到虚拟微型端口和基础微型端口驱动程序的电源状态。 若要了解有关对查询的电源状态影响的详细信息和设置操作，请参阅[处理设置 Power 请求](handling-a-set-power-request.md)。

 

网络参考部分包含有关所有常规、 面向连接的、 特定于 nonmedia 的 Oid 和所需的特定于媒体的 Oid 中间驱动程序开发人员感兴趣的信息。

以下主题提供有关颁发和响应的查询的其他信息，并在中间的驱动程序设置：

[发出从中间驱动程序集和查询请求](issuing-set-and-query-requests-from-an-intermediate-driver.md)

[中间的驱动程序中的集和查询响应](responding-to-sets-and-queries-in-an-intermediate-driver.md)

 

 






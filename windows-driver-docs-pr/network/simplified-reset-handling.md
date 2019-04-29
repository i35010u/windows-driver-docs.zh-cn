---
title: 简化的重置处理
description: 简化的重置处理
ms.assetid: ac07bfe3-9144-422a-96ca-d2ca2cc6861d
keywords:
- NDIS 微型端口驱动程序 WDK，重置微型端口适配器
- 重置微型端口适配器
- 适配器 WDK 网络重置操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d01b62f1e761d1eb962061bf45ad15a206f48675
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356856"
---
# <a name="simplified-reset-handling"></a>简化的重置处理





NDIS 6.0 和更高版本的驱动程序不重置微型端口适配器为取消发送或 OID 的请求。 相反，NDIS 提供发送取消和 OID 请求取消函数。

NDIS 微型端口驱动程序可以完成或取消挂起的发送操作或挂起的 OID 请求在任何时间--之前或之后完成重置。 微型端口驱动程序没有接收到相对于重置请求时跟踪的。 此外，驱动程序无需重置完成同步已取消的请求。

有关详细信息，请参阅[取消发送操作](canceling-a-send-operation.md)，[适配器的 OID 请求](miniport-adapter-oid-requests.md)，[协议驱动程序 OID 请求](protocol-driver-oid-requests.md)，和[筛选器模块 OID请求](filter-module-oid-requests.md)。

 

 






---
title: 简化的重置处理
description: 简化的重置处理
keywords:
- NDIS 微型端口驱动程序 WDK，重置微型端口适配器
- 重置微型端口适配器
- 适配器 WDK 网络，重置操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db28c947fd8e65aebbac3c946118d2c8c25a2e84
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797913"
---
# <a name="simplified-reset-handling"></a>简化的重置处理





NDIS 6.0 和更高版本的驱动程序不会重置微型端口适配器以取消发送请求或 OID 请求。 取而代之的是，NDIS 提供发送取消和 OID 请求取消函数。

NDIS 微型端口驱动程序可随时完成或取消挂起的发送操作或挂起的 OID 请求，无论是在完成重置之前还是之后。 微型端口驱动程序无需跟踪收到有关重置的请求的时间。 此外，驱动程序不需要在完成重置后同步已取消的请求。

有关详细信息，请参阅 [取消发送操作](canceling-a-send-operation.md)、 [OID 请求适配器](miniport-adapter-oid-requests.md)、 [协议驱动程序 Oid 请求](protocol-driver-oid-requests.md)和 [筛选器模块 oid 请求](filter-module-oid-requests.md)。

 

 






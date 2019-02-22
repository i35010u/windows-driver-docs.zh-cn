---
title: NDIS 网络接口
description: NDIS 网络接口
ms.assetid: a1d062d4-3d4b-4244-b851-667d708810db
keywords:
- NDIS WDK，网络接口
- NDIS 网络接口 WDK
- 网络接口 WDK
- NDISIF WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac4c312b31feb1872a999fc43a2c5245f142c1cd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554609"
---
# <a name="ndis-network-interfaces"></a>NDIS 网络接口





若要支持管理信息基础 (MIB)，NDIS 管理本地计算机的网络接口信息的集合。 NDIS 接口提供程序到 NDIS 提供有关某些网络接口的信息。 NDIS 提供了一个代理注册接口的接口提供程序，并处理接口的微型端口适配器提供程序请求和筛选器模块。 因此，没有 NDIS 驱动程序所需网络接口提供程序。

但是，所有的 NDIS 网络驱动程序类型可以将注册为接口提供程序。 此类驱动程序注册的网络接口，并提供回调函数以响应接口 OID 请求。 NDIS 接口提供程序通常提供有关接口的不能直接访问到 NDIS 和不受 NDIS 代理接口提供程序的信息。 例如，MUX 中间驱动程序可以有其虚拟微型端口和基础适配器之间的内部接口。

本部分包括：

[NDIS 网络接口的概述](overview-of-ndis-network-interfaces.md)

[注册为接口提供程序](registering-as-an-interface-provider.md)

[管理 NDIS 网络接口](managing-ndis-network-interfaces.md)

[处理 OID 查询和 NDIS 接口提供程序中的集请求](handling-oid-query-and-set-requests-in-an-ndis-interface-provider.md)

[映射到 NDIS Oid 的 NDIS 网络接口](mapping-of-ndis-network-interfaces-to-ndis-oids.md)

 

 






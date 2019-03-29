---
title: 管理 NDIS 网络接口
description: 管理 NDIS 网络接口
ms.assetid: b4c61b8a-a3ef-449d-9bce-853d91911dc4
keywords:
- NDIS 网络接口 WDK，管理
- 网络接口 WDK，管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 173a4fd8912f5bd27b8230b44b1dc800cd6202e0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577259"
---
# <a name="managing-ndis-network-interfaces"></a>管理 NDIS 网络接口





NDIS 网络接口提供程序注册 NDIS 网络接口。 在注册之前接口，接口提供程序获取[ **NET\_LUID** ](https://msdn.microsoft.com/library/windows/hardware/ff568747)该接口的值。 NDIS 为指定接口的索引 ( *IfIndex*在 RFC 2863) 到已注册的接口。

NDIS 还提供了驱动程序可用于管理界面堆栈表中的条目的服务 (*ifStackTable*在 RFC 2863)。

本部分包括：

[NET\_LUID 值](net-luid-value.md)

[使用 NET\_LUID 索引](using-a-net-luid-index.md)

[注册网络接口](registering-a-network-interface.md)

[取消注册的网络接口](deregistering-a-network-interface.md)

[映射网络\_LUID 值到接口索引](mapping-a-net-luid-value-to-an-interface-index.md)

[NET\_微型端口适配器和筛选器模块的 LUID 值](net-luid-values-for-miniport-adapters-and-filter-modules.md)

[维护网络接口堆栈](maintaining-a-network-interface-stack.md)

 

 






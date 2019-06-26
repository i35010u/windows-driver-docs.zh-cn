---
title: 管理 NDIS 网络接口
description: 管理 NDIS 网络接口
ms.assetid: b4c61b8a-a3ef-449d-9bce-853d91911dc4
keywords:
- NDIS 网络接口 WDK，管理
- 网络接口 WDK，管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 410a7003ce97ffb2f9f8cf15ff61c51f8d8d80ab
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356149"
---
# <a name="managing-ndis-network-interfaces"></a>管理 NDIS 网络接口





NDIS 网络接口提供程序注册 NDIS 网络接口。 在注册之前接口，接口提供程序获取[ **NET\_LUID** ](https://docs.microsoft.com/windows/desktop/api/ifdef/ns-ifdef-net_luid_lh)该接口的值。 NDIS 为指定接口的索引 ( *IfIndex*在 RFC 2863) 到已注册的接口。

NDIS 还提供了驱动程序可用于管理界面堆栈表中的条目的服务 (*ifStackTable*在 RFC 2863)。

本部分包括：

[NET\_LUID 值](net-luid-value.md)

[使用 NET\_LUID 索引](using-a-net-luid-index.md)

[注册网络接口](registering-a-network-interface.md)

[取消注册的网络接口](deregistering-a-network-interface.md)

[映射网络\_LUID 值到接口索引](mapping-a-net-luid-value-to-an-interface-index.md)

[NET\_微型端口适配器和筛选器模块的 LUID 值](net-luid-values-for-miniport-adapters-and-filter-modules.md)

[维护网络接口堆栈](maintaining-a-network-interface-stack.md)

 

 






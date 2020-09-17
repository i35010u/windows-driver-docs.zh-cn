---
title: 将 NET_LUID 值映射到接口索引
description: 将 NET_LUID 值映射到接口索引
ms.assetid: a535d886-186e-4abe-9ca0-ebef262614b3
keywords:
- NDIS 网络接口 WDK，NET_LUID
- 网络接口 WDK，NET_LUID
- NET_LUID
- 映射 NET_LUID 值
- 接口索引 WDK 网络
- 索引操作 WDK 网络接口
- 本地唯一标识符 WDK 网络接口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d3cb2ce39a6f0d7aaefb5d328beca2a28d51f9b
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715738"
---
# <a name="mapping-a-net_luid-value-to-an-interface-index"></a>将 NET \_ LUID 值映射到接口索引





NDIS 提供服务来获取给定 [**NET \_ LUID**](/windows/win32/api/ifdef/ns-ifdef-net_luid_lh) 值的接口索引，反之亦然。 请注意，NET \_ LUID 值是接口的永久性标识，与特定 NET LUID 值相对应的接口索引 \_ 可能会更改，即使计算机未重新启动 (例如，当已禁用并重新启用关联的微型端口适配器时，将更改筛选器模块，因为已禁用并重新启用了关联的微型端口适配器) 。

NDIS 提供以下映射函数：

-   [**NdisIfGetInterfaceIndexFromNetLuid**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifgetinterfaceindexfromnetluid)

-   [**NdisIfGetNetLuidFromInterfaceIndex**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifgetnetluidfrominterfaceindex)

\_ \_ \_ \_ 如果 \_ 已注册的接口列表中不存在给定的 NET LUID 或接口索引，则这些函数将返回 NDIS 状态接口。

 


---
title: 微型端口适配器和筛选器模块的 NET_LUID 值
description: 微型端口适配器和筛选器模块的 NET_LUID 值
ms.assetid: d9135438-3399-4845-a28d-d445471cb41d
keywords:
- NDIS 网络接口 WDK，NET_LUID
- 网络接口 WDK，NET_LUID
- NET_LUID
- 微型端口适配器 WDK 网络，NET_LUID 值
- 筛选器模块 WDK 网络，NET_LUID 值
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a57f15cf664a23fe31629e7a1976c1959aa950e5
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210715"
---
# <a name="net_luid-values-for-miniport-adapters-and-filter-modules"></a>\_微型端口适配器和筛选器模块的 NET LUID 值





对于每个微型端口适配器 (，NDIS 为每个微型端口适配器注册接口，) 并筛选每个筛选器模块) 的驱动程序 (。 协议驱动程序可以通过使用其绑定句柄，为驱动程序绑定到的微型端口适配器查询 NDIS 作为接口索引和 [**NET \_ LUID**](/windows/desktop/api/ifdef/ns-ifdef-net_luid_lh) 值。 例如，MUX 中间驱动程序的协议驱动程序下边缘可能会获取 NET \_ LUID 值以指定其内部接口的分层顺序。

协议驱动程序将 *NdisBindingHandle* 参数中的绑定句柄传递到 [**NdisIfQueryBindingIfIndex**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifquerybindingifindex) 函数，并在 \_ 筛选器堆栈的顶部和底部接收接口索引和网络 LUID 值。 或者，协议驱动程序可以在 [**NDIS \_ 绑定 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters) 结构中检索这些值。

微型端口驱动程序还可以通过使用 NDIS 微型端口适配器句柄，查询 NDIS 以获得微型端口适配器的接口索引。 小型端口驱动程序 \_ 在 [**NDIS \_ 微型端口 \_ 初始 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_init_parameters) 结构中接收接口索引和 NET LUID 值。

筛选器驱动程序 \_ 在 [**NDIS \_ 筛选器 \_ 附加 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_attach_parameters) 结构中获取筛选器模块的接口索引和 NET LUID 值。

 


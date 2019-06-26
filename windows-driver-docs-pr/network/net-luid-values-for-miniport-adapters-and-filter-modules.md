---
title: 微型端口适配器和筛选器模块的 NET_LUID 值
description: 微型端口适配器和筛选器模块的 NET_LUID 值
ms.assetid: d9135438-3399-4845-a28d-d445471cb41d
keywords:
- NDIS 网络接口 WDK，NET_LUID
- 网络接口 WDK，NET_LUID
- NET_LUID
- 微型端口适配器 WDK 网络 NET_LUID 值
- 筛选器模块 WDK 网络 NET_LUID 值
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2513d1b70eefcb35f4b749d10a756c5a2d110053
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386334"
---
# <a name="netluid-values-for-miniport-adapters-and-filter-modules"></a>NET\_微型端口适配器和筛选器模块的 LUID 值





NDIS 注册代表微型端口驱动程序 （适用于每个微型端口适配器） 和 （适用于每个筛选器模块） 的筛选器驱动程序的接口。 协议驱动程序可以查询的接口索引 NDIS 和[ **NET\_LUID** ](https://docs.microsoft.com/windows/desktop/api/ifdef/ns-ifdef-net_luid_lh)驱动程序通过使用其绑定句柄绑定到的微型端口适配器的值。 例如，协议驱动程序的 MUX 中间驱动程序的下边缘可以获取 NET\_LUID 值，以指定其内部接口的分层顺序。

协议驱动程序将在绑定句柄传递*NdisBindingHandle*参数[ **NdisIfQueryBindingIfIndex** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisifquerybindingifindex)函数，并接收接口索引和 NET\_顶部和底部的筛选器堆栈的接口的 LUID 值。 或者，协议驱动程序可以检索这些值在[ **NDIS\_绑定\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_bind_parameters)结构。

微型端口驱动程序还可以查询 NDIS 的微型端口适配器的接口索引使用 NDIS 微型端口适配器句柄。 微型端口驱动程序接收的接口索引和 NET\_中的 LUID 值[ **NDIS\_微型端口\_INIT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_init_parameters)结构。

筛选器驱动程序获取的接口索引和 NET\_LUID 值中的筛选器模块[ **NDIS\_筛选器\_附加\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_filter_attach_parameters)结构。

 

 






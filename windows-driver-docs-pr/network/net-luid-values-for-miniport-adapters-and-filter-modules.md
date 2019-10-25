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
ms.openlocfilehash: 8a78f97ef22bd710dfbc3beff83df4a5a1340481
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827236"
---
# <a name="net_luid-values-for-miniport-adapters-and-filter-modules"></a>微型端口适配器和筛选器模块的 NET\_LUID 值





NDIS 代表微型端口驱动程序（适用于每个微型端口适配器）和筛选器驱动程序（适用于每个筛选器模块）注册接口。 协议驱动程序可以通过使用其绑定句柄，查询用于驱动程序绑定到的微型端口适配器的 "NDIS" 的接口索引和[**NET\_LUID**](https://docs.microsoft.com/windows/desktop/api/ifdef/ns-ifdef-net_luid_lh)值。 例如，MUX 中间驱动程序的协议驱动程序下边缘可能会获取 NET\_LUID 值以指定其内部接口的分层顺序。

协议驱动程序将*NdisBindingHandle*参数中的绑定句柄传递到[**NdisIfQueryBindingIfIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifquerybindingifindex)函数，并为筛选器堆栈的顶部和底部的接口接收接口索引和 NET\_LUID 值。 或者，协议驱动程序可以在[**NDIS\_绑定\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)结构中检索这些值。

微型端口驱动程序还可以通过使用 NDIS 微型端口适配器句柄，查询 NDIS 以获得微型端口适配器的接口索引。 微型端口驱动程序在[**NDIS\_微型端口\_初始化\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_init_parameters)结构中接收接口索引和 NET\_LUID 值。

筛选器驱动程序为 NDIS\_筛选器中的筛选器模块获取接口索引和 NET\_LUID 值[ **\_附加\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_attach_parameters)结构。

 

 






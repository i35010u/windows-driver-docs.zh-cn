---
title: 处理接口对象查询请求
description: 处理接口对象查询请求
ms.assetid: c4dc4d9e-52ea-477f-9bc8-cf04ccaa73b2
keywords:
- NDIS 网络接口 WDK，查询请求
- 网络接口 WDK，查询请求
- Oid WDK 网络，网络接口
- OID 请求 WDK 网络
- 查询请求 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e50e7ee63e2f0c8c49234c07b11fdf20a32d312c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842113"
---
# <a name="handling-an-interface-object-query-request"></a>处理接口对象查询请求





为了获取与 interface 对象关联的当前值，NDIS 调用接口提供程序的[**ProviderQueryObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-if_query_object)函数。 如果成功处理了查询请求或 NDIS\_状态\_*Xxx*错误代码，则此函数将返回 NDIS\_状态\_成功。

有关接口提供程序特定 OID 请求的列表，请参阅[NDIS 网络接口 oid](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-network-interface-oids)。 有关 NDIS 用于提供程序、微型端口适配器和筛选器模块以支持网络接口对象的 Oid 列表，请参阅[用于 OID 映射的 Ndis 网络接口](mapping-of-ndis-network-interfaces-to-ndis-oids.md)。

[**ProviderQueryObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-if_query_object)的*ProviderIfContext*参数处的句柄标识接口提供程序在调用[**NdisIfRegisterInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifregisterinterface)函数以注册接口时传递到 NDIS 的上下文区域。 *ObjectId*参数为正在查询的对象指定 OID。 *POutputBufferLength*和*pOutputBuffer*参数分别提供指向输出缓冲区的结果长度和指向输出缓冲区的指针的指针。

 

 






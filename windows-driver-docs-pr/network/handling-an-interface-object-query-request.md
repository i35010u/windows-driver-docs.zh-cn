---
title: 处理接口对象查询请求
description: 处理接口对象查询请求
ms.assetid: c4dc4d9e-52ea-477f-9bc8-cf04ccaa73b2
keywords:
- NDIS 网络接口 WDK、 查询请求
- 网络接口 WDK，查询请求
- Oid WDK 网络，网络接口
- OID 请求 WDK 网络
- 查询请求 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c43078a26f669bd24d431918cf533e91d2c0c0c3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366631"
---
# <a name="handling-an-interface-object-query-request"></a>处理接口对象查询请求





若要获取与接口对象相关联的当前值，NDIS 调用的接口提供[ **ProviderQueryObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-if_query_object)函数。 此函数将返回 NDIS\_状态\_成功，如果已成功处理查询请求或 NDIS\_状态\_*Xxx*错误代码，否则为。

接口提供程序特定 OID 请求的列表，请参阅[NDIS 网络接口 Oid](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-network-interface-oids)。 有关与提供程序使用 NDIS 的 Oid 的列表，微型端口适配器和筛选器模块以支持网络接口对象，请参阅[NDIS OID 映射的网络接口](mapping-of-ndis-network-interfaces-to-ndis-oids.md)。

在句柄*ProviderIfContext*的参数[ **ProviderQueryObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-if_query_object)标识接口提供程序传递到 NDIS 时调用它的上下文区域[ **NdisIfRegisterInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisifregisterinterface)函数来注册接口。 *ObjectId*参数指定要查询的对象的 OID。 *POutputBufferLength*并*pOutputBuffer*参数分别提供了指向生成的输出缓冲区长度的指针和指向输出缓冲区的指针。

 

 






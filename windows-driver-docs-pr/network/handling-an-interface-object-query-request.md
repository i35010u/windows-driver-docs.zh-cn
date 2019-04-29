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
ms.openlocfilehash: fd2909df9c04a23d7eecd7726dad76b191b1827e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349749"
---
# <a name="handling-an-interface-object-query-request"></a>处理接口对象查询请求





若要获取与接口对象相关联的当前值，NDIS 调用的接口提供[ **ProviderQueryObject** ](https://msdn.microsoft.com/library/windows/hardware/ff570399)函数。 此函数将返回 NDIS\_状态\_成功，如果已成功处理查询请求或 NDIS\_状态\_*Xxx*错误代码，否则为。

接口提供程序特定 OID 请求的列表，请参阅[NDIS 网络接口 Oid](https://msdn.microsoft.com/library/windows/hardware/ff566545)。 有关与提供程序使用 NDIS 的 Oid 的列表，微型端口适配器和筛选器模块以支持网络接口对象，请参阅[NDIS OID 映射的网络接口](mapping-of-ndis-network-interfaces-to-ndis-oids.md)。

在句柄*ProviderIfContext*的参数[ **ProviderQueryObject** ](https://msdn.microsoft.com/library/windows/hardware/ff570399)标识接口提供程序传递到 NDIS 时调用它的上下文区域[ **NdisIfRegisterInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff562715)函数来注册接口。 *ObjectId*参数指定要查询的对象的 OID。 *POutputBufferLength*并*pOutputBuffer*参数分别提供了指向生成的输出缓冲区长度的指针和指向输出缓冲区的指针。

 

 






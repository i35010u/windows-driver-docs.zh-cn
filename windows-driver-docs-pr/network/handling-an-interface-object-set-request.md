---
title: 处理接口对象设置请求
description: 处理接口对象设置请求
ms.assetid: aed27b0b-fff5-4e9f-b368-526a8bf79c59
keywords:
- NDIS 网络接口 WDK 中，将请求设置
- WDK 中，将请求设置为网络接口
- Oid WDK 网络，网络接口
- OID 请求 WDK 网络
- 设置请求 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5490124d6aacac6018d3846709813b58b0011dcd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371235"
---
# <a name="handling-an-interface-object-set-request"></a>处理接口对象设置请求


若要设置与接口对象相关联的数据，NDIS 调用的接口提供[ **ProviderSetObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-if_set_object)函数。 此函数将返回 NDIS\_状态\_成功，如果已成功更改数据或 NDIS\_状态\_*Xxx*错误代码，否则为。

接口提供程序特定 OID 请求的列表，请参阅[NDIS 网络接口 Oid](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-network-interface-oids)。 有关与提供程序使用 NDIS 的 Oid 的列表，微型端口适配器和筛选器模块以支持网络接口对象，请参阅[NDIS OID 映射的网络接口](mapping-of-ndis-network-interfaces-to-ndis-oids.md)。

在句柄*ProviderIfContext*的参数[ **ProviderSetObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-if_set_object)标识接口提供程序传递到 NDIS 时调用它的上下文区域[ **NdisIfRegisterInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisifregisterinterface)函数来注册接口。 *ObjectId*参数指定要设置的对象的 OID。 *InputBufferLength*并*pInputBuffer*参数分别提供的输入的缓冲区和指向输入缓冲区的长度。

 

 






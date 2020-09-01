---
title: 查询 Hyper-V 可扩展交换机配置
description: 查询 Hyper-V 可扩展交换机配置
ms.assetid: AF646860-01AB-4F4B-84F8-B570054B10FC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d1499b2c791766eb18f70aac6eba0db3adba9e1
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215120"
---
# <a name="querying-the-hyper-v-extensible-switch-configuration"></a>查询 Hyper-V 可扩展交换机配置


Hyper-v 可扩展交换机接口包含由可扩展交换机扩展颁发的对象标识符 (OID) 请求，以查询可扩展交换机、其端口和其网络适配器连接的当前配置。 这些请求包括以下 Oid：

<a href="" id="oid-switch-nic-array"></a>[OID \_ 交换机 \_ NIC \_ 阵列](./oid-switch-nic-array.md)  
此 OID 查询请求返回一个数组。 数组中的每个元素指定与可扩展交换机端口关联的网络适配器的配置参数。

<a href="" id="oid-switch-parameters"></a>[OID \_ 开关 \_ 参数](./oid-switch-parameters.md)  
此 OID 查询请求返回可扩展交换机的当前配置。

<a href="" id="oid-switch-port-array"></a>[OID \_ 交换机 \_ 端口 \_ 数组](./oid-switch-port-array.md)  
此 OID 查询请求返回一个数组。 数组中的每个元素都指定可扩展交换机端口的配置参数。

<a href="" id="oid-switch-port-property-enum"></a>[OID \_ 交换机 \_ 端口 \_ 属性 \_ 枚举](./oid-switch-port-property-enum.md)  
此 OID 方法请求返回一个数组。 数组中的每个元素都为指定的可扩展交换机端口指定了策略的属性。

<a href="" id="oid-switch-property-enum"></a>[OID \_ 开关 \_ 属性 \_ 枚举](./oid-switch-property-enum.md)  
此 OID 方法请求返回一个数组。 数组中的每个元素指定可扩展交换机策略的属性。

**注意**   当交换机扩展绑定到 Hyper-v 可扩展交换机时，它必须首先发出[oid \_ 交换机 \_ 参数](./oid-switch-parameters.md)OID，才能获取基本交换机信息。 如果[**NDIS \_ 开关 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_parameters)结构的**IsActive**成员为 FALSE，则在开关完成激活之前，扩展不能发出其他查询 oid。 在这种情况下， **NetEventSwitchActivate** [**NET \_ PNP \_ 事件**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event) 通知指定了交换机激活事件。 如果在 bind 时 **IsActive** 成员为 TRUE，则扩展可以安全地发出其他查询 oid。 在 Hyper-v 可扩展交换机尚未完成激活的情况下查询配置会导致扩展具有未完成的交换机配置初始视图。

 

**注意**   当某个扩展生成自己的 OID 请求时，它将以与任何 NDIS 筛选器驱动程序相同的方式执行此功能。 有关如何执行此操作的详细信息，请参阅 [从 NDIS 筛选器驱动程序生成 OID 请求](generating-oid-requests-from-an-ndis-filter-driver.md)。

 

有关可扩展交换机 OID 请求的控制路径的详细信息，请参阅 [OID 请求的 Hyper-v 可扩展交换机控制路径](hyper-v-extensible-switch-control-path-for-oid-requests.md)。

 


---
title: 查询 Hyper-V 可扩展交换机配置
description: 查询 Hyper-V 可扩展交换机配置
ms.assetid: AF646860-01AB-4F4B-84F8-B570054B10FC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f52dd8578dd8f3f2a3d09317c3584b2d218c721
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379211"
---
# <a name="querying-the-hyper-v-extensible-switch-configuration"></a>查询 Hyper-V 可扩展交换机配置


HYPER-V 可扩展交换机接口包括颁发的可扩展交换机扩展来查询可扩展交换机、 其端口和其网络适配器连接的当前配置的对象标识符 (OID) 请求。 这些请求包括下列 Oid:

<a href="" id="oid-switch-nic-array"></a>[OID\_交换机\_NIC\_数组](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-array)  
此 OID 查询请求返回一个数组。 数组中的每个元素指定与可扩展交换机端口相关联的网络适配器的配置参数。

<a href="" id="oid-switch-parameters"></a>[OID\_交换机\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-parameters)  
此 OID 查询请求返回可扩展交换机的当前配置。

<a href="" id="oid-switch-port-array"></a>[OID\_交换机\_端口\_数组](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-array)  
此 OID 查询请求返回一个数组。 数组中的每个元素指定可扩展交换机端口的配置参数。

<a href="" id="oid-switch-port-property-enum"></a>[OID\_交换机\_端口\_属性\_枚举](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-enum)  
此 OID 方法请求返回一个数组。 数组中的每个元素指定用于指定可扩展交换机端口的策略的属性。

<a href="" id="oid-switch-property-enum"></a>[OID\_交换机\_属性\_枚举](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-enum)  
此 OID 方法请求返回一个数组。 数组中的每个元素指定可扩展交换机策略的属性。

**请注意**  时的交换机扩展的 hyper-v 可扩展交换机绑定，必须首先发出[OID\_切换\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-parameters)OID 获取基本交换机的信息。 如果**IsActive**的成员[ **NDIS\_开关\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_parameters)结构是 FALSE，该扩展必须发出其他查询 Oid直到开关已完成激活。 在这种情况下， **NetEventSwitchActivate** [ **NET\_PNP\_事件**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_pnp_event)通知指定开关激活事件。 如果**IsActive**成员为 TRUE 时绑定，扩展可以安全地发出其他查询 Oid。 Hyper-v 可扩展交换机未完成激活时查询的配置将导致具有一个不完整的初始视图的交换机配置的扩展。

 

**请注意**  时扩展插件可生成其自己的 OID 请求，做到这一点的相同方式任何 NDIS 筛选器驱动程序。 有关如何执行此操作的详细信息，请参阅[NDIS 筛选器驱动程序从生成 OID 请求](generating-oid-requests-from-an-ndis-filter-driver.md)。

 

可扩展交换机 OID 请求的控制路径的详细信息，请参阅[HYPER-V 可扩展交换机控件路径的 OID 请求](hyper-v-extensible-switch-control-path-for-oid-requests.md)。

 

 






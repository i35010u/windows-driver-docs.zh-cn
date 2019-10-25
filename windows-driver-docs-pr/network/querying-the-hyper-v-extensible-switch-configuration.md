---
title: 查询 Hyper-V 可扩展交换机配置
description: 查询 Hyper-V 可扩展交换机配置
ms.assetid: AF646860-01AB-4F4B-84F8-B570054B10FC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21a8115003c16d79c0c40807eda5f9224062ad5b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844879"
---
# <a name="querying-the-hyper-v-extensible-switch-configuration"></a>查询 Hyper-V 可扩展交换机配置


Hyper-v 可扩展交换机接口包含由可扩展交换机扩展颁发的对象标识符（OID）请求，以查询可扩展交换机、其端口和其网络适配器连接的当前配置。 这些请求包括以下 Oid：

<a href="" id="oid-switch-nic-array"></a>[OID\_交换机\_NIC\_数组](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-array)  
此 OID 查询请求返回一个数组。 数组中的每个元素指定与可扩展交换机端口关联的网络适配器的配置参数。

<a href="" id="oid-switch-parameters"></a>[OID\_SWITCH\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-parameters)  
此 OID 查询请求返回可扩展交换机的当前配置。

<a href="" id="oid-switch-port-array"></a>[OID\_交换机\_端口\_数组](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-array)  
此 OID 查询请求返回一个数组。 数组中的每个元素都指定可扩展交换机端口的配置参数。

<a href="" id="oid-switch-port-property-enum"></a>[OID\_SWITCH\_端口\_属性\_枚举](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-enum)  
此 OID 方法请求返回一个数组。 数组中的每个元素都为指定的可扩展交换机端口指定了策略的属性。

<a href="" id="oid-switch-property-enum"></a>[OID\_SWITCH\_属性\_枚举](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-enum)  
此 OID 方法请求返回一个数组。 数组中的每个元素指定可扩展交换机策略的属性。

**请注意**  交换机扩展绑定到 Hyper-v 可扩展交换机时，它必须首先颁发[OID\_交换机\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-parameters)OID 才能获取基本交换机信息。 如果[**NDIS\_交换机**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_parameters)的**ISACTIVE**成员\_参数结构为 FALSE，则在切换完成激活之前，扩展不能发出其他查询 oid。 在这种情况下， **NetEventSwitchActivate** [**NET\_PNP\_事件**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event)通知指定了交换机激活事件。 如果在 bind 时**IsActive**成员为 TRUE，则扩展可以安全地发出其他查询 oid。 在 Hyper-v 可扩展交换机尚未完成激活的情况下查询配置会导致扩展具有未完成的交换机配置初始视图。

 

**请注意**  扩展会生成自己的 OID 请求时，它将以与任何 NDIS 筛选器驱动程序相同的方式执行此项。 有关如何执行此操作的详细信息，请参阅[从 NDIS 筛选器驱动程序生成 OID 请求](generating-oid-requests-from-an-ndis-filter-driver.md)。

 

有关可扩展交换机 OID 请求的控制路径的详细信息，请参阅[OID 请求的 Hyper-v 可扩展交换机控制路径](hyper-v-extensible-switch-control-path-for-oid-requests.md)。

 

 






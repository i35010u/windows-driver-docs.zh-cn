---
title: 端口策略概述
description: 端口策略概述
ms.assetid: 9FA63E67-F5CC-4508-A36F-7A5956568D0E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: efb0e8968ef4fe2e8f174721d814e44400047e27
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843726"
---
# <a name="overview-of-port-policies"></a>端口策略概述


从 NDIS 6.30 开始，Hyper-v 可扩展交换机端口支持以下类型的策略：

<a href="" id="built-in-port-policies"></a>内置端口策略  
内置端口策略指定可扩展交换机接口强制执行的属性。 可扩展交换机驱动程序堆栈中的扩展未预配这些策略的属性。

内置端口策略包括访问控制列表（Acl）和服务质量（QoS）属性。 当数据包到达入口数据路径上的可扩展交换机的微型端口边缘时，交换机将筛选数据包并强制实施这些策略。 如果数据包通过了筛选，则交换机会将数据包转发到传出数据路径，以便进行额外的处理，并按过量扩展进行筛选。

有关可扩展交换机数据路径的详细信息，请参阅[Hyper-v 可扩展交换机数据路径](hyper-v-extensible-switch-data-path.md)。

<a href="" id="standard-port-policies"></a>标准端口策略  
标准端口策略指定安全性、配置文件或虚拟 LAN （VLAN）属性。 这些属性由可扩展交换机的协议边缘发出的对象标识符（OID）请求进行设置。 如果未在可扩展交换机数据路径中安装和启用转发扩展，则会通过基础可扩展交换机的小型端口边缘来强制执行这些策略。 否则，如果转发扩展允许设置策略，则会强制执行这些策略。

标准端口属性由[**NDIS\_交换机\_端口\_属性\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_switch_port_property_type)枚举值指定为**NdisSwitchPortPropertyTypeSecurity**、 **NdisSwitchPortPropertyTypeVlan**和**NdisSwitchPortPropertyTypeProfile**。

**请注意**  如果转发扩展不管理或强制执行 VLAN 端口属性，则它必须返回\_不\_[OID](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-add)的\_数据的状态\_\_\_\_\_\_\_\_[](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-update) VLAN 端口属性的属性类型为**NdisSwitchPortPropertyTypeVlan**。

 

<a href="" id="custom-port-policies"></a>自定义端口策略  
自定义端口策略指定由独立软件供应商（ISV）定义的专有属性。 这些属性由可扩展交换机的可扩展交换机协议边缘发出的 OID 请求进行设置，并由管理自定义端口策略的基础扩展强制执行。

自定义端口属性通过托管对象格式（MOF）类定义来定义。 ISV 通过 MOF 类定义定义自定义端口属性的格式。 MOF 文件注册到 WMI 管理层后，会将基础扩展设置为自定义端口策略。

自定义端口属性由 NDIS 指定[ **\_交换机\_端口\_属性\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_switch_port_property_type)枚举值为**NdisSwitchPortPropertyTypeCustom**。 每个自定义端口属性都通过 GUID 值进行唯一定义。 该扩展插件管理已为其配置了属性 GUID 值的自定义端口属性。

**请注意**  用属性的 GUID 值配置扩展的方法对于 ISV 是专有的。

 

标准和自定义端口策略通过以下 OID 请求进行预配：

-   协议边缘发出 oid 设置[oid\_SWITCH\_端口\_属性的请求\_添加](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-add)以通知基础扩展添加标准或自定义端口属性。

-   协议边缘颁发 oid [\_SWITCH\_端口\_\_属性](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-update)的 oid 设置请求，以将更新的基础扩展通知到标准或自定义端口属性。

-   协议边缘颁发 oid [\_SWITCH\_端口\_属性\_DELETE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-delete)请求，以通知基础扩展删除标准或自定义端口属性。

转发扩展可以通过 vetoing OID 请求来阻止预配新的或更新的端口策略。 此扩展通过以下方式实现此功能：完成 OID 请求，状态\_数据\_不\_接受。 如果扩展不否决 OID 请求，则必须调用[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)将 oid 请求向下转发到可扩展的交换机控制路径。

**请注意**  如果扩展不否决 OID 请求，则会在请求完成时监视状态。 此扩展将执行此操作，以确定可扩展交换机控制路径中的基础扩展或可扩展交换机接口是否否决了 OID 请求。

 

有关如何管理端口策略和属性的详细信息，请参阅[管理端口策略](managing-port-policies.md)。

 

 






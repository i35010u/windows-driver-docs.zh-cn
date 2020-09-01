---
title: 交换机策略概述
description: 交换机策略概述
ms.assetid: DB9368CE-96D4-48C9-AE18-601EE4A09001
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 86daa25e01d2cd7852b675ea431e9e4051c9c2a7
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207855"
---
# <a name="overview-of-switch-policies"></a>交换机策略概述


从 NDIS 6.30 开始，Hyper-v 可扩展交换机支持以下类型的策略：

<a href="" id="built-in-switch-policies"></a>内置交换机策略  
内置交换机策略指定可扩展交换机接口强制执行的属性。 可扩展交换机驱动程序堆栈中的扩展未预配这些策略的属性。

内置交换机策略包含的属性通常会影响交换机配置，但不影响单个交换机端口上的通信流。 例如，一个这样的内置策略会将开关配置为允许硬件卸载到支持单一根 i/o 虚拟化 (SR-IOV) 接口的物理适配器。 有关此接口的详细信息，请参阅 [单一根 I/o 虚拟化 (sr-iov) ](overview-of-single-root-i-o-virtualization--sr-iov-.md)。

<a href="" id="custom-switch-policies"></a>自定义交换机策略  
自定义交换机策略指定由独立软件供应商 (ISV) 定义的专有属性。 这些属性由可扩展交换机的协议边缘设置，并由管理自定义交换机策略的基础扩展强制执行。

ISV 定义自定义交换机属性的格式。 自定义交换机属性的格式是 ISV 专用的。

自定义开关属性是通过 (MOF) 类定义的托管对象格式定义的。 MOF 文件注册到 WMI 管理层后，会将基础扩展设置为自定义交换机策略。

自定义开关属性由**NdisSwitchPropertyTypeCustom**的[**NDIS \_ 开关 \_ 属性 \_ 类型**](/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_switch_property_type)枚举值指定。 每个自定义开关属性都通过 GUID 值进行唯一定义。 该扩展插件管理已为其配置了属性 GUID 值的自定义交换机属性。

**注意**   使用属性的 GUID 值配置扩展的方法对于 ISV 是专有的。

 

自定义交换机策略通过以下 OID 请求进行预配：

-   协议边缘发出 oid 设置 [oid \_ 开关 \_ 属性 \_ ADD](./oid-switch-property-add.md) 的请求，以通知基础扩展添加了自定义的切换属性。

-   协议边缘发出 OID [ \_ 开关 \_ 属性 \_ 更新](./oid-switch-property-update.md) 请求，以将更新的基础扩展通知给自定义的切换属性。

-   协议边缘发出 oid [ \_ 开关 \_ 属性 \_ DELETE](./oid-switch-property-delete.md) 请求，以通知基础扩展删除自定义开关属性。

转发扩展可以通过 vetoing OID 请求来阻止预配新的或已更新的交换机策略。 此扩展通过完成 OID 请求来实现此功能，但状态 \_ 数据 \_ 不 \_ 被接受。 如果扩展不否决 OID 请求，则必须调用 [**NdisFOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest) 将 oid 请求向下转发到可扩展的交换机控制路径。

**注意**   如果扩展不否决 OID 请求，则会在请求完成时监视状态。 此扩展将执行此操作，以确定可扩展交换机控制路径中的基础扩展或可扩展交换机接口是否否决了 OID 请求。

 

有关如何管理交换机策略和属性的详细信息，请参阅 [管理交换机策略](managing-switch-policies.md)。

 


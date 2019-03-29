---
title: 交换机策略概述
description: 交换机策略概述
ms.assetid: DB9368CE-96D4-48C9-AE18-601EE4A09001
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de8a6e03b8b3b9607ec440675ac56e009267d4ef
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564090"
---
# <a name="overview-of-switch-policies"></a>交换机策略概述


从 NDIS 6.30 开始，HYPER-V 可扩展交换机支持以下类型的策略：

<a href="" id="built-in-switch-policies"></a>内置交换机策略  
内置交换机策略指定强制实施由可扩展交换机接口的属性。 可扩展交换机驱动程序堆栈中的扩展将不设置这些策略的属性。

内置交换机策略包括在一般情况下会影响的交换机配置，但不是会通过单独的交换机端口影响流量流的属性。 例如，内置策略配置交换机以允许到支持的单个根 I/O 虚拟化 (SR-IOV) 接口的物理适配器的硬件卸载功能。 有关此接口的详细信息，请参阅[单根 I/O 虚拟化 (SR-IOV)](overview-of-single-root-i-o-virtualization--sr-iov-.md)。

<a href="" id="custom-switch-policies"></a>自定义开关策略  
自定义开关策略指定由独立软件供应商 (ISV) 定义的专用属性。 这些属性通过可扩展交换机的协议边缘预配和管理自定义开关策略的基础扩展插件强制执行。

ISV 定义自定义开关属性的格式。 自定义开关属性的格式是专有的 ISV。

自定义开关属性定义通过托管的对象格式 (MOF) 的类定义。 MOF 文件注册到 WMI 管理层后，使用自定义开关策略预配的基础扩展。

通过指定自定义开关属性[ **NDIS\_切换\_属性\_类型**](https://msdn.microsoft.com/library/windows/hardware/hh598257)枚举值的**NdisSwitchPropertyTypeCustom**。 每个自定义开关属性唯一地定义通过 GUID 值。 扩展可用于管理这些自定义开关属性为其配置了该属性的 GUID 值。

**请注意**  与属性的 GUID 值配置该扩展的方法是为 ISV 专有。

 

自定义开关策略是通过以下 OID 请求预配：

-   协议边缘发出的 OID 集请求[OID\_切换\_属性\_添加](https://msdn.microsoft.com/library/windows/hardware/hh598280)通知添加自定义开关属性的基础扩展。

-   协议边缘发出的 OID 集请求[OID\_切换\_属性\_更新](https://msdn.microsoft.com/library/windows/hardware/hh598283)通知的自定义开关属性的更新的基础扩展。

-   协议边缘发出的 OID 集请求[OID\_切换\_属性\_删除](https://msdn.microsoft.com/library/windows/hardware/hh598281)通知的自定义开关属性删除基础扩展。

转发扩展可以阻止通过禁止 OID 请求设置新的或更新的交换机策略。 通过完成状态为 OID 请求的扩展插件实现这\_数据\_不\_已接受。 如果扩展不能阻止 OID 请求，它必须调用[ **NdisFOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561830)下可扩展交换机控制路径 OID 请求转发。

**请注意**  如果扩展不能阻止 OID 请求，它监视的状态，当请求完成。 扩展插件这样做是为了确定 OID 请求已被否决的可扩展交换机控制路径中的基础扩展或可扩展交换机接口。

 

有关如何管理交换机策略和属性的详细信息，请参阅[管理切换策略](managing-switch-policies.md)。

 

 






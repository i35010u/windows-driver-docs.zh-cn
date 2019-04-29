---
title: 端口策略概述
description: 端口策略概述
ms.assetid: 9FA63E67-F5CC-4508-A36F-7A5956568D0E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ef4dc49e1f5b526ff568bd82c58208e54bd804c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360195"
---
# <a name="overview-of-port-policies"></a>端口策略概述


从 NDIS 6.30 开始，HYPER-V 可扩展交换机端口支持以下类型的策略：

<a href="" id="built-in-port-policies"></a>内置端口策略  
内置端口策略指定强制实施由可扩展交换机接口的属性。 可扩展交换机驱动程序堆栈中的扩展将不设置这些策略的属性。

内置端口策略包括访问控制列表 (Acl) 和质量的服务 (QoS) 属性。 当数据包到达微型端口边缘的可扩展交换机的入口数据路径时，此开关对包进行过滤，并强制实施这些策略。 如果数据包通过筛选，交换机将向上出口数据路径用于其他处理和通过过量扩展筛选数据包转发。

有关可扩展交换机数据路径的详细信息，请参阅[HYPER-V 可扩展交换机数据路径](hyper-v-extensible-switch-data-path.md)。

<a href="" id="standard-port-policies"></a>标准端口策略  
标准端口策略指定安全、 配置文件或虚拟 LAN (VLAN) 属性。 这些属性由对象标识符 (OID) 请求颁发可扩展交换机的协议边缘的预配。 如果未安装和启用可扩展交换机数据路径中的转发扩展，这些策略会强制执行基础可扩展交换机的微型端口边缘。 否则，转发扩展实施这些策略，如果它可以使策略将其预配。

通过指定标准端口属性[ **NDIS\_交换机\_端口\_属性\_类型**](https://msdn.microsoft.com/library/windows/hardware/hh598242)枚举值的**NdisSwitchPortPropertyTypeSecurity**， **NdisSwitchPortPropertyTypeVlan**，和**NdisSwitchPortPropertyTypeProfile**。

**请注意**  如果转发扩展不管理或强制实施 VLAN 端口属性，它必须返回状态\_数据\_不\_接受[OID\_交换机\_端口\_属性\_添加](https://msdn.microsoft.com/library/windows/hardware/hh598275)并[OID\_开关\_端口\_属性\_更新](https://msdn.microsoft.com/library/windows/hardware/hh598278)的添加或更新请求属性。 VLAN 端口属性的属性类型为**NdisSwitchPortPropertyTypeVlan**。

 

<a href="" id="custom-port-policies"></a>自定义端口策略  
自定义端口策略指定由独立软件供应商 (ISV) 定义的专用属性。 OID 请求颁发的可扩展交换机协议边缘的可扩展交换机和管理自定义端口策略的基础扩展插件强制实施由预配这些属性。

自定义端口属性定义通过托管的对象格式 (MOF) 的类定义。 ISV 定义通过 MOF 类定义的自定义端口属性的格式。 MOF 文件注册到 WMI 管理层后，使用自定义端口策略预配的基础扩展。

通过指定自定义端口属性[ **NDIS\_交换机\_端口\_属性\_类型**](https://msdn.microsoft.com/library/windows/hardware/hh598242)枚举值的**NdisSwitchPortPropertyTypeCustom**。 通过 GUID 值唯一地定义每个自定义端口属性。 扩展可用于管理为其配置了该属性的 GUID 值使用这些自定义端口属性。

**请注意**  与属性的 GUID 值配置该扩展的方法是为 ISV 专有。

 

标准和自定义端口策略是通过以下 OID 请求预配：

-   协议边缘发出的 OID 集请求[OID\_交换机\_端口\_属性\_添加](https://msdn.microsoft.com/library/windows/hardware/hh598275)通知添加一个标准或自定义端口属性的基础扩展。

-   协议边缘发出的 OID 集请求[OID\_交换机\_端口\_属性\_更新](https://msdn.microsoft.com/library/windows/hardware/hh598278)通知到标准或自定义端口属性更新的基础扩展。

-   协议边缘发出的 OID 集请求[OID\_交换机\_端口\_属性\_删除](https://msdn.microsoft.com/library/windows/hardware/hh598276)通知的标准或自定义端口属性删除基础扩展。

转发扩展可以阻止通过禁止 OID 请求设置新的或更新端口策略。 通过完成状态为 OID 请求的扩展插件实现这\_数据\_不\_已接受。 如果扩展不能阻止 OID 请求，它必须调用[ **NdisFOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561830)下可扩展交换机控制路径 OID 请求转发。

**请注意**  如果扩展不能阻止 OID 请求，它监视的状态，当请求完成。 扩展插件这样做是为了确定 OID 请求已被否决的可扩展交换机控制路径中的基础扩展或可扩展交换机接口。

 

有关如何管理端口策略和属性的详细信息，请参阅[管理端口策略](managing-port-policies.md)。

 

 






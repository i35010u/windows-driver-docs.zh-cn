---
title: 管理端口策略
description: 管理端口策略
ms.assetid: 46394916-6558-4BDA-8920-E3C5378823BE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 916a50af47ca454e754ab8d32d52c5ddbca53d09
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576557"
---
# <a name="managing-port-policies"></a>管理端口策略


筛选和转发扩展的 HYPER-V 可扩展交换机可以提供标准和自定义端口属性的属性。 预配后，这些扩展执行时获取可扩展交换机入口数据路径上的数据包中筛选出的策略。 有关这些策略的详细信息，请参阅[端口策略](port-policies.md)。

HYPER-V 可扩展交换机接口使用以下对象标识符 (Oid) 来预配筛选和转发扩展的标准和自定义端口策略属性：

<a href="" id="oid-switch-port-property-add"></a>[OID\_交换机\_端口\_属性\_添加](https://msdn.microsoft.com/library/windows/hardware/hh598275)  
通知的 WMI 管理层的属性添加的基础扩展的可扩展交换机的协议边缘颁发此 OID 集请求。 **InformationBuffer**的[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向[ **NDIS\_交换机\_端口\_属性\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh598238)结构。

**请注意**  来指定自定义端口属性时[ **NDIS\_开关\_端口\_属性\_类型**](https://msdn.microsoft.com/library/windows/hardware/hh598242)枚举值**NdisSwitchPortPropertyTypeCustom**。 通过指定标准端口属性**NDIS\_交换机\_端口\_属性\_类型**枚举值的**NdisSwitchPortPropertyTypeSecurity**， **NdisSwitchPortPropertyTypeVlan**，和**NdisSwitchPortPropertyTypeProfile**。

 

<a href="" id="oid-switch-port-property-update"></a>[OID\_交换机\_端口\_属性\_更新](https://msdn.microsoft.com/library/windows/hardware/hh598278)  
要通知的 WMI 管理层的属性更新的基础扩展的可扩展交换机的协议边缘颁发此 OID 集请求。 **InformationBuffer**的[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向[ **NDIS\_交换机\_端口\_属性\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh598238)结构。

<a href="" id="oid-switch-port-property-delete"></a>[OID\_交换机\_端口\_属性\_删除](https://msdn.microsoft.com/library/windows/hardware/hh598276)  
通知的 WMI 管理层的属性删除基础扩展的可扩展交换机的协议边缘颁发此 OID 集请求。 **InformationBuffer**的[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向[ **NDIS\_交换机\_端口\_属性\_删除\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh598232)结构。

<a href="" id="oid-switch-port-property-enum"></a>[OID\_交换机\_端口\_属性\_枚举](https://msdn.microsoft.com/library/windows/hardware/hh598277)  
该扩展会发送此 OID 方法请求以查询的可扩展交换机上的指定端口的当前配置的属性的可扩展交换机的基础微型端口边缘。 **InformationBuffer**的[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向缓冲区的指针。 此缓冲区包含以下数据：

-   [ **NDIS\_交换机\_端口\_属性\_枚举\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh598236)结构，它指定策略参数指定的端口的枚举。

-   一个数组[ **NDIS\_交换机\_端口\_属性\_枚举\_信息**](https://msdn.microsoft.com/library/windows/hardware/hh598233)结构。 每个这些结构包含可扩展交换机端口策略的属性有关的信息。

    **请注意**  如果**NumProperties**的成员[ **NDIS\_交换机\_端口\_属性\_枚举\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh598236)结构设置为零，否[ **NDIS\_交换机\_端口\_属性\_枚举\_信息** ](https://msdn.microsoft.com/library/windows/hardware/hh598233)返回结构。

     

**请注意**  扩展不是源自 OID 的集请求[OID\_交换机\_端口\_属性\_添加](https://msdn.microsoft.com/library/windows/hardware/hh598275)。 [OID\_交换机\_端口\_属性\_更新](https://msdn.microsoft.com/library/windows/hardware/hh598278)，或[OID\_交换机\_端口\_属性\_删除](https://msdn.microsoft.com/library/windows/hardware/hh598276).

 

可扩展的交换机扩展必须处理的 OID 集请求时请遵循以下准则[OID\_切换\_端口\_属性\_添加](https://msdn.microsoft.com/library/windows/hardware/hh598275)， [OID\_交换机\_端口\_属性\_更新](https://msdn.microsoft.com/library/windows/hardware/hh598278)，或[OID\_开关\_端口\_属性\_删除](https://msdn.microsoft.com/library/windows/hardware/hh598276):

-   该扩展不能修改[ **NDIS\_交换机\_端口\_属性\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh598238)或[ **NDIS\_交换机\_端口\_属性\_删除\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh598232)与 OID 请求关联的结构。

-   如果扩展可用于管理属性，扩展必须处理这些 OID 请求。 具体取决于 OID 请求，该扩展必须检查的以下成员[ **NDIS\_交换机\_端口\_属性\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh598238)或[ **NDIS\_交换机\_端口\_属性\_删除\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh598232)结构以确定是否它管理端口属性：

    -   **PropertyType**成员。 此成员指定端口属性的类型。 自定义端口的属性具有**PropertyType**的成员值**NdisSwitchPortPropertyTypeCustom**。 标准端口属性具有其他属性类型值。 例如，标准 VLAN 端口策略具有的属性类型值**NdisSwitchPortPropertyTypeVlan**。

    -   **PropertyId**成员。 此成员指定自定义端口属性的专有 GUID 值。 此 GUID 值创建的独立软件供应商 (ISV)，管理员也可定义自定义可扩展交换机属性的格式。

        **请注意**  扩展必须忽略此成员的标准端口策略。

         

-   扩展必须处理[OID\_交换机\_端口\_属性\_更新](https://msdn.microsoft.com/library/windows/hardware/hh598278)集请求，如果该扩展以前预配具有匹配的端口属性以下的成员[ **NDIS\_交换机\_属性\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh598255)结构：

    -   **PropertyType**成员。

    -   **PropertyId**成员。

        **请注意**  扩展必须忽略此成员的标准端口策略。

         

    -   **PropertyVersion**成员。 此成员指定扩展的预配时使用的端口属性的版本。

    -   **PropertyInstanceId**成员。 此成员指定扩展的预配时使用的端口属性的实例。

-   添加或更新它所管理的端口策略来筛选或转发扩展可以禁止。 通过完成状态为 OID 请求的扩展插件实现这\_数据\_不\_已接受。

    **请注意**  捕获扩展不能阻止添加或更新的端口策略。 相反，它必须转发 OID 请求下可扩展交换机控制路径。

     

-   转发扩展可能会不支持的标准端口属性或属性是否与自己的策略配置具有冲突的 OID 请求失败。 在这种情况下，该扩展必须完成 OID 请求并返回相应的 NDIS 状态代码来报告失败。

-   如果扩展已成功处理的标准端口策略 OID 集请求，它必须完成 OID 请求，并必须将其转发可扩展交换机控制路径下。

-   如果捕获或筛选扩展已成功处理的自定义端口策略 OID 集请求，它必须完成 OID 请求，并必须将其转发可扩展交换机控制路径下。

    如果转发扩展已成功处理的自定义端口策略 OID 集请求，它必须完成 OID 请求，并返回相应的 NDIS\_状态\_*Xxx*值。

-   如果扩展不会完成 OID 集请求，它必须调用[ **NdisFOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561830)可扩展交换机在驱动程序堆栈的下层 OID 请求转发。 在这种情况下，扩展应监视 OID 来检测基础扩展是否已失败 OID 请求的完成状态。

 

 






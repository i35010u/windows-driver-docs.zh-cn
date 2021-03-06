---
title: 管理交换机策略
description: 管理交换机策略
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 68103e9a2b8394e0e7a4dbdb30941faf7da99a4b
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248064"
---
# <a name="managing-switch-policies"></a>管理交换机策略


可以通过自定义交换机属性的属性设置 hyper-v 可扩展交换机筛选和转发扩展。 预配后，这些扩展将在筛选器传入数据路径的可扩展交换机上时强制执行策略。 有关这些策略的详细信息，请参阅 [交换机策略](switch-policies.md)。

Hyper-v 可扩展交换机接口使用以下对象标识符 (Oid) 使用自定义交换机策略的属性预配筛选和转发扩展：

<a href="" id="oid-switch-property-add"></a>[OID \_ 开关 \_ 属性 \_ 添加](./oid-switch-property-add.md)  
此 OID 集请求由可扩展交换机的协议边缘发出，用于通知基础扩展在 WMI 管理层添加属性的情况。 [**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 包含指向 [**ndis \_ SWITCH \_ 属性 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_parameters)结构的指针。

**注意** 自定义开关属性由 **NdisSwitchPropertyTypeCustom** 的 [**NDIS \_ 开关 \_ 属性 \_ 类型**](/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_switch_property_type)枚举值指定。

 

<a href="" id="oid-switch-property-update"></a>[OID \_ 开关 \_ 属性 \_ 更新](./oid-switch-property-update.md)  
此 OID 集请求由可扩展交换机的协议边缘发出，用于在 WMI 管理层通知基础属性更新的基础扩展。 [**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 包含指向 [**ndis \_ SWITCH \_ 属性 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_parameters)结构的指针。

<a href="" id="oid-switch-property-delete"></a>[OID \_ 开关 \_ 属性 \_ 删除](./oid-switch-property-delete.md)  
此 OID 集请求由可扩展交换机的协议边缘发出，用于通知基础扩展在 WMI 管理层删除属性的情况。 [**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 包含指向 [**ndis \_ 交换机 \_ 属性 \_ 删除 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_delete_parameters)结构的指针。

<a href="" id="oid-switch-property-enum"></a>[OID \_ 开关 \_ 属性 \_ 枚举](./oid-switch-property-enum.md)  
此 OID 方法请求是由扩展发送的，用于查询可扩展交换机的基础微型端口边缘，以了解有关可扩展交换机上当前配置的开关属性的信息。 [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 包含指向缓冲区的指针。 此缓冲区包含以下数据：

-   [**NDIS \_ 交换机 \_ 属性 \_ 枚举 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_enum_parameters)结构，指定交换机策略的属性枚举参数。

-   [**NDIS \_ 开关 \_ 属性 \_ 枚举 \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_enum_info)结构的数组。 其中每个结构都包含有关交换机策略的属性的信息。

    **注意** 如果 [**ndis \_ 交换机 \_ 属性 \_ Enum \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_enum_parameters)结构的 **NumProperties** 成员设置为零，则不会返回 [**ndis \_ 交换机 \_ 属性 \_ 枚举 \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_enum_info)结构。

     

**注意**  此扩展不能发起 oid 设置 [oid \_ 开关 \_ 属性 \_ ADD](./oid-switch-property-add.md)的请求。 [OID \_开关 \_ 属性 \_ 更新](./oid-switch-property-update.md)或 [OID \_ 开关 \_ 属性 \_ 删除](./oid-switch-property-delete.md)。

 

当可扩展交换机扩展处理 [oid \_ 开关 \_ 属性 \_ 添加](./oid-switch-property-add.md)、 [oid \_ 开关属性 \_ \_ 更新](./oid-switch-property-update.md)或 [oid \_ 开关 \_ 属性 \_ 删除](./oid-switch-property-delete.md)时，必须遵循以下准则：

-   扩展不得修改与 OID 请求关联的 [**ndis \_ 开关 \_ 属性 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_parameters) 或 [**ndis \_ 交换机 \_ 属性 \_ DELETE \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_delete_parameters) 结构。

-   如果先前已设置了与 [**ndis \_ 开关 \_ 属性 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_parameters)或 [**ndis \_ 开关 \_ 属性 \_ 删除 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_delete_parameters)结构的以下成员相匹配的 SWITCH 属性，则扩展必须处理 [oid \_ 开关 \_ 属性 \_ 更新](./oid-switch-property-update.md)或 [oid \_ 开关 \_ 属性 \_ 删除](./oid-switch-property-delete.md)集请求：

    -   指定开关属性类型的 **PropertyType** 成员。

        **注意**  从 NDIS 6.30 开始，仅 **NdisSwitchPropertyTypeCustom** 的开关属性由 [**ndis \_ 开关 \_ 属性 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_parameters) 或 [**ndis \_ 开关 \_ 属性 \_ DELETE \_ PARAMETERS**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_delete_parameters) 结构指定。

         

    -   指定扩展识别的专有 GUID 值的 **PropertyId** 成员。 此 GUID 值由独立的软件供应商创建 (ISV) ，后者还定义自定义可扩展交换机策略属性的格式。

        **注意**  自定义的可扩展交换机策略属性包含在 [**NDIS \_ 交换机 \_ 属性 \_ 自定义**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_custom) 结构内。

         

-   如果扩展处理这些 OID 集请求，则扩展必须更新或删除与 [**NDIS \_ switch \_ 属性 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_parameters) 结构的以下成员匹配的开关策略：

    -   指定可扩展交换机策略版本的 **PropertyVersion** 成员。

    -   指定可扩展交换机策略实例的 **PropertyInstanceId** 成员。

    如果这些成员的值与以前预配了该扩展的 switch 策略属性不匹配，则该扩展必须使具有 NDIS \_ 状态无效参数的 OID 设置请求 \_ 失败 \_ 。 否则，扩展必须完成 OID 集请求并返回 NDIS \_ 状态 \_ 成功。

-   筛选或转发扩展可以否决添加、删除或更新交换机策略。 此扩展通过完成 OID 请求来实现此功能，但状态 \_ 数据 \_ 不 \_ 被接受。

    **注意**  捕获扩展不得禁止添加或更新交换机策略。 相反，它必须将 OID 请求向下转发到可扩展交换机控制路径。

     

-   如果捕获或筛选扩展成功处理自定义交换机策略的 OID 集请求，则它不能完成 OID 请求，必须将其向下转发到可扩展的交换机控制路径。

    如果转发扩展插件成功处理自定义交换机策略的 OID 集请求，则必须完成 OID 请求并返回相应的 NDIS \_ 状态 \_ *Xxx* 值。

-   如果扩展不能完成 OID 集请求，则它必须调用 [**NdisFOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest) 来向下扩展 oid 请求，使其关闭可扩展交换机驱动程序堆栈。 在这种情况下，扩展应监视 OID 的完成状态，以检测基础扩展是否已失败 OID 请求。

 


---
title: 管理端口策略
description: 管理端口策略
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37874fc0e5295724f9274638bb6edd2ea9a2d9b0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802355"
---
# <a name="managing-port-policies"></a>管理端口策略


可以通过标准端口属性和自定义端口属性的属性预配 hyper-v 可扩展交换机筛选和转发扩展。 预配后，这些扩展将在筛选器传入数据路径的可扩展交换机上时强制执行策略。 有关这些策略的详细信息，请参阅 [端口策略](port-policies.md)。

Hyper-v 可扩展交换机接口使用以下对象标识符 (Oid) 使用标准端口策略和自定义端口策略的属性预配筛选和转发扩展：

<a href="" id="oid-switch-port-property-add"></a>[OID \_ 交换机 \_ 端口 \_ 属性 \_ 添加](./oid-switch-port-property-add.md)  
此 OID 集请求由可扩展交换机的协议边缘发出，用于通知基础扩展在 WMI 管理层添加属性的情况。 [**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 **InformationBuffer** 包含指向 [**NDIS \_ 交换机 \_ 端口 \_ 属性 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_parameters)结构的指针。

**注意**  自定义端口属性由 [**NDIS \_ 交换机 \_ 端口 \_ 属性 \_ 类型**](/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_switch_port_property_type) 枚举值 **NdisSwitchPortPropertyTypeCustom** 指定。 标准端口属性由 **NdisSwitchPortPropertyTypeSecurity**、 **NdisSwitchPortPropertyTypeVlan** 和 **NdisSwitchPortPropertyTypeProfile** 的 **NDIS \_ 交换机 \_ 端口 \_ 属性 \_ 类型** 枚举值指定。

 

<a href="" id="oid-switch-port-property-update"></a>[OID \_ 交换机 \_ 端口 \_ 属性 \_ 更新](./oid-switch-port-property-update.md)  
此 OID 集请求是由可扩展交换机的协议边缘发出的，用于在 WMI 管理层通知基础属性的更新的基础扩展。 [**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 **InformationBuffer** 包含指向 [**NDIS \_ 交换机 \_ 端口 \_ 属性 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_parameters)结构的指针。

<a href="" id="oid-switch-port-property-delete"></a>[OID \_ 交换机 \_ 端口 \_ 属性 \_ 删除](./oid-switch-port-property-delete.md)  
此 OID 集请求由可扩展交换机的协议边缘发出，用于通知基础扩展在 WMI 管理层删除属性的情况。 [**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 **InformationBuffer** 包含指向 [**NDIS \_ 交换机 \_ 端口 \_ 属性 \_ DELETE \_ PARAMETERS**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_delete_parameters)结构的指针。

<a href="" id="oid-switch-port-property-enum"></a>[OID \_ 交换机 \_ 端口 \_ 属性 \_ 枚举](./oid-switch-port-property-enum.md)  
此 OID 方法请求由该扩展插件发送，用于查询可扩展交换机上有关当前配置属性的可扩展交换机的基础微型端口边缘。 [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 **InformationBuffer** 包含指向缓冲区的指针。 此缓冲区包含以下数据：

-   [**NDIS \_ 交换机 \_ 端口 \_ 属性 \_ 枚举 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_enum_parameters)结构，为指定端口的策略枚举指定参数。

-   [**NDIS \_ 交换机 \_ 端口 \_ 属性 \_ 枚举 \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_enum_info)结构的数组。 其中每个结构都包含有关可扩展交换机端口策略的属性的信息。

    **注意** 如果 [**ndis \_ 交换机 \_ 端口 \_ 属性 " \_ 枚举 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_enum_parameters)结构" 的 **NumProperties** 成员设置为零，则不会返回 [**ndis \_ 交换机 \_ 端口 \_ 属性 \_ 枚举 \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_enum_info)结构。

     

**注意**  此扩展不能发起 oid 设置 [oid \_ 交换机 \_ 端口 \_ 属性 \_ ADD](./oid-switch-port-property-add.md)的请求。 [OID \_交换机 \_ 端口 \_ 属性 \_ 更新](./oid-switch-port-property-update.md)或 [OID \_ 交换机 \_ 端口 \_ 属性 \_ 删除](./oid-switch-port-property-delete.md)。

 

当可扩展交换机扩展处理 [oid \_ 交换机 \_ 端口 \_ 属性 \_ 添加](./oid-switch-port-property-add.md)、 [oid \_ 交换机 \_ 端口 \_ 属性 \_ 更新](./oid-switch-port-property-update.md)或 [oid \_ 交换机 \_ 端口 \_ 属性 \_ 删除](./oid-switch-port-property-delete.md)时，必须遵循以下准则：

-   扩展不得修改与 OID 请求关联的 [**ndis \_ 交换机 \_ 端口 \_ 属性 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_parameters) 或 [**ndis \_ 交换机 \_ 端口 \_ 属性 \_ 删除 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_delete_parameters) 结构。

-   如果扩展插件管理属性，则必须处理这些 OID 请求。 根据 OID 请求，扩展必须检查 [**ndis \_ 交换机 \_ 端口 \_ 属性 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_parameters) 或 [**ndis \_ 交换机 \_ 端口 \_ 属性 " \_ 删除 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_delete_parameters) 结构" 的以下成员，以确定它是否管理端口属性：

    -   **PropertyType** 成员。 此成员指定端口属性的类型。 自定义端口属性的 **PropertyType** 成员值为 **NdisSwitchPortPropertyTypeCustom**。 标准端口属性具有其他属性类型值。 例如，标准 VLAN 端口策略的属性类型值为 " **NdisSwitchPortPropertyTypeVlan**"。

    -   **PropertyId** 成员。 此成员为自定义端口属性指定一个专用 GUID 值。 此 GUID 值是由独立软件供应商 (ISV) 创建的，它也定义自定义可扩展交换机属性的格式。

        **注意**  此扩展必须忽略标准端口策略的此成员。

         

-   如果先前预配了某个端口属性的端口属性与 [**NDIS \_ 交换机 \_ 属性 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_parameters)结构的以下成员匹配，则扩展必须处理 [OID \_ 交换机 \_ 端口 \_ 属性 \_ 更新](./oid-switch-port-property-update.md)集请求：

    -   **PropertyType** 成员。

    -   **PropertyId** 成员。

        **注意**  此扩展必须忽略标准端口策略的此成员。

         

    -   **PropertyVersion** 成员。 此成员指定设置扩展时所用的端口属性的版本。

    -   **PropertyInstanceId** 成员。 此成员指定为其预配扩展的端口属性的实例。

-   筛选或转发扩展可以拒绝添加或更新它所管理的端口策略。 此扩展通过完成 OID 请求来实现此功能，但状态 \_ 数据 \_ 不 \_ 被接受。

    **注意**  捕获扩展不得禁止添加或更新端口策略。 相反，它必须将 OID 请求向下转发到可扩展交换机控制路径。

     

-   转发扩展可能会导致不支持的标准端口属性的 OID 请求失败，或者属性是否与自身的策略配置冲突。 在这种情况下，扩展必须完成 OID 请求并返回相应的 NDIS 状态代码以报告失败。

-   如果扩展已成功处理标准端口策略的 OID 集请求，则它不能完成 OID 请求，必须将其向下转发到可扩展的交换机控制路径。

-   如果捕获或筛选扩展成功处理自定义端口策略的 OID 集请求，则它不能完成 OID 请求，必须将其向下转发到可扩展的交换机控制路径。

    如果转发扩展插件成功处理自定义端口策略的 OID 集请求，则必须完成 OID 请求并返回相应的 NDIS \_ 状态 \_ *Xxx* 值。

-   如果扩展不能完成 OID 集请求，则它必须调用 [**NdisFOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest) 来向下扩展 oid 请求，使其关闭可扩展交换机驱动程序堆栈。 在这种情况下，扩展应监视 OID 的完成状态，以检测基础扩展是否已失败 OID 请求。

 


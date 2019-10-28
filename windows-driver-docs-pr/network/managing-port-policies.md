---
title: 管理端口策略
description: 管理端口策略
ms.assetid: 46394916-6558-4BDA-8920-E3C5378823BE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 70c44e036cb0d0a7f4eea4a3039e6a8dc9272221
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844116"
---
# <a name="managing-port-policies"></a>管理端口策略


可以通过标准端口属性和自定义端口属性的属性预配 hyper-v 可扩展交换机筛选和转发扩展。 预配后，这些扩展将在筛选器传入数据路径的可扩展交换机上时强制执行策略。 有关这些策略的详细信息，请参阅[端口策略](port-policies.md)。

Hyper-v 可扩展交换机接口使用以下对象标识符（Oid）来设置具有标准和自定义端口策略属性的筛选和转发扩展：

<a href="" id="oid-switch-port-property-add"></a>[OID\_SWITCH\_端口\_属性\_添加](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-add)  
此 OID 集请求由可扩展交换机的协议边缘发出，用于通知基础扩展在 WMI 管理层添加属性的情况。 [ **\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**包含指向[**ndis\_SWITCH\_端口\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_parameters)结构的指针。\_

**请注意**  自定义端口属性由[**NDIS\_交换机\_端口\_属性\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_switch_port_property_type)枚举值**指定。** 标准端口属性由**NDIS\_交换机\_端口指定\_属性\_类型**枚举值（ **NdisSwitchPortPropertyTypeSecurity**、 **NdisSwitchPortPropertyTypeVlan**）和**NdisSwitchPortPropertyTypeProfile**。

 

<a href="" id="oid-switch-port-property-update"></a>[OID\_交换机\_端口\_属性\_更新](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-update)  
此 OID 集请求是由可扩展交换机的协议边缘发出的，用于在 WMI 管理层通知基础属性的更新的基础扩展。 [ **\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**包含指向[**ndis\_SWITCH\_端口\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_parameters)结构的指针。\_

<a href="" id="oid-switch-port-property-delete"></a>[OID\_SWITCH\_端口\_属性\_DELETE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-delete)  
此 OID 集请求由可扩展交换机的协议边缘发出，用于通知基础扩展在 WMI 管理层删除属性的情况。 [ **\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**包含指向[**NDIS\_SWITCH\_端口\_\_DELETE\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_delete_parameters)结构的指针。

<a href="" id="oid-switch-port-property-enum"></a>[OID\_SWITCH\_端口\_属性\_枚举](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-enum)  
此 OID 方法请求由该扩展插件发送，用于查询可扩展交换机上有关当前配置属性的可扩展交换机的基础微型端口边缘。 [ **\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**包含指向缓冲区的指针。 此缓冲区包含以下数据：

-   [**NDIS\_交换机\_端口\_属性\_枚举\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_enum_parameters)结构，该结构指定指定端口的策略枚举的参数。

-   一组[**NDIS\_交换机\_端口\_属性\_枚举\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_enum_info)结构。 其中每个结构都包含有关可扩展交换机端口策略的属性的信息。

    **请注意**  如果 NDIS\_的**NumProperties**成员[**切换\_端口\_属性\_枚举\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_enum_parameters)结构设置为零，则不[**NDIS\_交换机\_端口\_返回\_枚举\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_enum_info)结构的属性。

     

**请注意**  扩展不能[\_SWITCH\_端口\_属性端口\_属性](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-add)中产生 oid 设置请求。 [Oid\_switch\_端口\_属性\_UPDATE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-update)或 OID\_\_DELETE\_\_[属性](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-delete)。

 

可扩展交换机扩展在处理 Oid 的 OID 集请求时必须遵循这些准则[\_switch\_端口\_属性\_ADD](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-add)， [OID\_switch\_端口](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-update)\_[\_SWITCH\_端口\_属性\_DELETE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-delete)：\_

-   扩展不能修改[**ndis\_交换机\_端口\_属性\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_parameters)或[**NDIS\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_delete_parameters)\_\_DELETE\_参数结构与 OID 请求关联的。\_

-   如果扩展插件管理属性，则必须处理这些 OID 请求。 根据 OID 请求，扩展必须检查[**ndis\_交换机\_端口\_属性\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_parameters)或 ndis\_\_\_\_@no_ [ **_t_12_ 参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_delete_parameters)结构，以确定它是否管理端口属性：\_

    -   **PropertyType**成员。 此成员指定端口属性的类型。 自定义端口属性的**PropertyType**成员值为**NdisSwitchPortPropertyTypeCustom**。 标准端口属性具有其他属性类型值。 例如，标准 VLAN 端口策略的属性类型值为 " **NdisSwitchPortPropertyTypeVlan**"。

    -   **PropertyId**成员。 此成员为自定义端口属性指定一个专用 GUID 值。 此 GUID 值是由独立软件供应商（ISV）创建的，后者还定义自定义可扩展交换机属性的格式。

        **请注意**  扩展必须忽略标准端口策略的此成员。

         

-   如果先前预配了该扩展，并且该扩展以前使用的端口属性与 NDIS\_SWITCH 的以下成员相匹配，则扩展必须处理[OID\_交换机\_端口\_属性\_更新](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-update)集请求[ **\_属性\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_parameters)结构：

    -   **PropertyType**成员。

    -   **PropertyId**成员。

        **请注意**  扩展必须忽略标准端口策略的此成员。

         

    -   **PropertyVersion**成员。 此成员指定设置扩展时所用的端口属性的版本。

    -   **PropertyInstanceId**成员。 此成员指定为其预配扩展的端口属性的实例。

-   筛选或转发扩展可以拒绝添加或更新它所管理的端口策略。 此扩展通过以下方式实现此功能：完成 OID 请求，状态\_数据\_不\_接受。

    **注意**  捕获扩展不得禁止添加或更新端口策略。 相反，它必须将 OID 请求向下转发到可扩展交换机控制路径。

     

-   转发扩展可能会导致不支持的标准端口属性的 OID 请求失败，或者属性是否与自身的策略配置冲突。 在这种情况下，扩展必须完成 OID 请求并返回相应的 NDIS 状态代码以报告失败。

-   如果扩展已成功处理标准端口策略的 OID 集请求，则它不能完成 OID 请求，必须将其向下转发到可扩展的交换机控制路径。

-   如果捕获或筛选扩展成功处理自定义端口策略的 OID 集请求，则它不能完成 OID 请求，必须将其向下转发到可扩展的交换机控制路径。

    如果转发扩展插件成功处理自定义端口策略的 OID 集请求，则它必须完成 OID 请求并返回相应的 NDIS\_状态\_*Xxx*值。

-   如果扩展不能完成 OID 集请求，则它必须调用[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)来向下扩展 oid 请求，使其关闭可扩展交换机驱动程序堆栈。 在这种情况下，扩展应监视 OID 的完成状态，以检测基础扩展是否已失败 OID 请求。

 

 






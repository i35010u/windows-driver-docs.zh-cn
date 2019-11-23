---
title: 管理交换机策略
description: 管理交换机策略
ms.assetid: F2261CA6-2D7A-4499-82F9-7E2D7C9C908D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed25735cc1e83bbef24b1fcc8fd179de9a5d1ce4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844111"
---
# <a name="managing-switch-policies"></a>管理交换机策略


可以通过自定义交换机属性的属性设置 hyper-v 可扩展交换机筛选和转发扩展。 预配后，这些扩展将在筛选器传入数据路径的可扩展交换机上时强制执行策略。 有关这些策略的详细信息，请参阅[交换机策略](switch-policies.md)。

Hyper-v 可扩展交换机接口使用以下对象标识符（Oid）来预配具有自定义交换机策略属性的筛选和转发扩展：

<a href="" id="oid-switch-property-add"></a>[OID\_SWITCH\_属性\_添加](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-add)  
此 OID 集请求由可扩展交换机的协议边缘发出，用于通知基础扩展在 WMI 管理层添加属性的情况。 [ **\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**包含指向[**ndis\_SWITCH\_属性的指针\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_parameters)结构。

**请注意**  自定义交换机属性由[**NDIS\_交换机\_属性\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_switch_property_type)枚举值**指定。**

 

<a href="" id="oid-switch-property-update"></a>[OID\_SWITCH\_属性\_更新](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-update)  
此 OID 集请求由可扩展交换机的协议边缘发出，用于在 WMI 管理层通知基础属性更新的基础扩展。 [ **\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**包含指向[**ndis\_SWITCH\_属性的指针\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_parameters)结构。

<a href="" id="oid-switch-property-delete"></a>[OID\_SWITCH\_属性\_DELETE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-delete)  
此 OID 集请求由可扩展交换机的协议边缘发出，用于通知基础扩展在 WMI 管理层删除属性的情况。 [ **\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**包含指向[**ndis\_SWITCH\_属性的指针\_删除\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_delete_parameters)结构。

<a href="" id="oid-switch-property-enum"></a>[OID\_SWITCH\_属性\_枚举](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-enum)  
此 OID 方法请求是由扩展发送的，用于查询可扩展交换机的基础微型端口边缘，以了解有关可扩展交换机上当前配置的开关属性的信息。 [ **\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**包含指向缓冲区的指针。 此缓冲区包含以下数据：

-   [**NDIS\_交换机\_属性\_枚举\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_enum_parameters)结构，该结构指定交换机策略的属性枚举参数。

-   一组[**NDIS\_交换机\_属性\_枚举\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_enum_info)结构。 其中每个结构都包含有关交换机策略的属性的信息。

    **请注意**  如果[**ndis\_SWITCH\_\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_enum_parameters)的**NumProperties**成员设置为0，则不会返回[**ndis\_交换机\_属性\_枚举\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_enum_info)结构。\_

     

**请注意**  扩展不能[\_SWITCH\_属性\_"添加](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-add)" 来发起 oid 设置 oid。 [Oid\_switch\_属性\_UPDATE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-update)或[oid\_switch\_DELETE\_属性](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-delete)。

 

可扩展交换机扩展在处理 Oid 的 OID 集请求时必须遵循这些准则[\_switch\_属性\_添加](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-add)、 [oid\_开关\_属性\_UPDATE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-update)或 OID\_\_[删除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-delete)：\_

-   扩展不能修改[**ndis\_交换机\_属性\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_parameters)或[**ndis\_交换机\_删除**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_delete_parameters)与 OID 请求关联\_参数结构。\_

-   如果以前已设置了一个开关属性，且该扩展以前已设置了一个开关属性，而该扩展已设置了与[**ndis\_开关\_属性\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_parameters)\_\_属性\_参数或[**ndis\_switch**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_delete_parameters)\_属性\_\_参数结构相同的 switch 属性，则该扩展必须处理[OID\_switch 属性\_UPDATE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-update)或[oid\_开关](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-delete)

    -   指定开关属性类型的**PropertyType**成员。

        **请注意**  从 Ndis 6.30 开始，仅**NdisSwitchPropertyTypeCustom**的 switch 属性由[**NDIS\_switch\_属性指定，\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_parameters)或[**ndis\_\_DELETE\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_delete_parameters)结构。\_

         

    -   指定扩展识别的专有 GUID 值的**PropertyId**成员。 此 GUID 值是由独立软件供应商（ISV）创建的，该供应商还定义自定义可扩展交换机策略属性的格式。

        **请注意**  自定义可扩展交换机策略属性包含在[**NDIS\_switch\_属性\_自定义**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_custom)结构内。

         

-   如果扩展处理这些 OID 集请求，则扩展必须更新或删除与[**NDIS\_switch\_属性\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_parameters)结构中的以下成员相匹配的开关策略：

    -   指定可扩展交换机策略版本的**PropertyVersion**成员。

    -   指定可扩展交换机策略实例的**PropertyInstanceId**成员。

    如果这些成员的值与先前预配了该扩展的 switch 策略属性不匹配，则该扩展必须使具有 NDIS\_状态\_无效\_参数的 OID set 请求失败。 否则，扩展必须完成 OID 集请求并返回 NDIS\_状态\_成功。

-   筛选或转发扩展可以否决添加、删除或更新交换机策略。 此扩展通过以下方式实现此功能：完成 OID 请求，状态\_数据\_不\_接受。

    **注意**  捕获扩展不得禁止添加或更新交换机策略。 相反，它必须将 OID 请求向下转发到可扩展交换机控制路径。

     

-   如果捕获或筛选扩展成功处理自定义交换机策略的 OID 集请求，则它不能完成 OID 请求，必须将其向下转发到可扩展的交换机控制路径。

    如果转发扩展插件成功处理自定义交换机策略的 OID 集请求，则它必须完成 OID 请求并返回相应的 NDIS\_状态\_*Xxx*值。

-   如果扩展不能完成 OID 集请求，则它必须调用[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)来向下扩展 oid 请求，使其关闭可扩展交换机驱动程序堆栈。 在这种情况下，扩展应监视 OID 的完成状态，以检测基础扩展是否已失败 OID 请求。

 

 






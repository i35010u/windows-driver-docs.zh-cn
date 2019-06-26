---
title: 管理交换机策略
description: 管理交换机策略
ms.assetid: F2261CA6-2D7A-4499-82F9-7E2D7C9C908D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fbc7257f64b01b06d706dd5d461fbbab0c6922f7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375231"
---
# <a name="managing-switch-policies"></a>管理交换机策略


筛选和转发扩展的 HYPER-V 可扩展交换机可以提供自定义开关属性的属性。 预配后，这些扩展执行时获取可扩展交换机入口数据路径上的数据包中筛选出的策略。 有关这些策略的详细信息，请参阅[交换机策略](switch-policies.md)。

HYPER-V 可扩展交换机接口使用以下对象标识符 (Oid) 来预配筛选和转发扩展的自定义开关策略属性：

<a href="" id="oid-switch-property-add"></a>[OID\_交换机\_属性\_添加](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-add)  
通知的 WMI 管理层的属性添加的基础扩展的可扩展交换机的协议边缘颁发此 OID 集请求。 **InformationBuffer**的[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含一个指向[ **NDIS\_交换机\_属性\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_property_parameters)结构。

**请注意**  通过指定自定义开关属性[ **NDIS\_切换\_属性\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ne-ntddndis-_ndis_switch_property_type) 的枚举值**NdisSwitchPropertyTypeCustom**。

 

<a href="" id="oid-switch-property-update"></a>[OID\_交换机\_属性\_更新](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-update)  
要通知的 WMI 管理层的属性更新的基础扩展的可扩展交换机的协议边缘颁发此 OID 集请求。 **InformationBuffer**的[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含一个指向[ **NDIS\_交换机\_属性\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_property_parameters)结构。

<a href="" id="oid-switch-property-delete"></a>[OID\_交换机\_属性\_删除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-delete)  
要通知的 WMI 管理层的属性删除基础扩展的可扩展交换机的协议边缘颁发此 OID 集请求。 **InformationBuffer**的[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含一个指向[ **NDIS\_交换机\_属性\_删除\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_property_delete_parameters)结构。

<a href="" id="oid-switch-property-enum"></a>[OID\_交换机\_属性\_枚举](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-enum)  
该扩展会发送此 OID 方法请求以查询有关可扩展交换机上的当前配置的交换机属性的可扩展交换机的基础的微型端口边缘。 **InformationBuffer**的[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含一个指向缓冲区的指针。 此缓冲区包含以下数据：

-   [ **NDIS\_切换\_属性\_枚举\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_property_enum_parameters)结构，它指定为属性枚举的开关参数策略。

-   一个数组[ **NDIS\_交换机\_属性\_枚举\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_property_enum_info)结构。 每个这些结构包含有关交换机策略的属性的信息。

    **请注意**  如果**NumProperties**的成员[ **NDIS\_交换机\_属性\_枚举\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_property_enum_parameters)结构设置为零，否[ **NDIS\_交换机\_属性\_枚举\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_property_enum_info)返回结构。

     

**请注意**  扩展不是源自 OID 的集请求[OID\_交换机\_属性\_添加](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-add)。 [OID\_交换机\_属性\_更新](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-update)，或[OID\_开关\_属性\_删除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-delete)。

 

可扩展的交换机扩展必须处理的 OID 集请求时请遵循以下准则[OID\_切换\_属性\_添加](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-add)， [OID\_交换机\_属性\_更新](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-update)，或[OID\_交换机\_属性\_删除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-delete):

-   该扩展不能修改[ **NDIS\_交换机\_属性\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_property_parameters)或[ **NDIS\_开关\_属性\_删除\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_property_delete_parameters)与 OID 请求关联的结构。

-   扩展必须处理[OID\_交换机\_属性\_更新](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-update)或[OID\_交换机\_属性\_删除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-delete)如果该扩展之前已设置了与交换机属性相匹配的以下成员的集请求[ **NDIS\_切换\_属性\_参数** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_port_property_parameters)或[ **NDIS\_开关\_属性\_删除\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_property_delete_parameters)结构：

    -   **PropertyType**指定开关属性类型的成员。

        **请注意**  从 NDIS 6.30 开始，只能在切换的属性**NdisSwitchPropertyTypeCustom**所指定的[ **NDIS\_切换\_属性\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_port_property_parameters)或[ **NDIS\_开关\_属性\_删除\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_property_delete_parameters)结构。

         

    -   **PropertyId**成员，用于指定扩展识别的专有 GUID 值。 此 GUID 值创建的独立软件供应商 (ISV)，管理员也可定义自定义可扩展交换机策略属性的格式。

        **请注意**  中包含自定义可扩展交换机策略属性[ **NDIS\_切换\_属性\_自定义**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_property_custom)结构。

         

-   如果该扩展处理这些 OID 集请求，该扩展必须更新或删除交换机策略相匹配的以下成员[ **NDIS\_切换\_属性\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_property_parameters)结构：

    -   **PropertyVersion**成员，指定的可扩展交换机策略的版本。

    -   **PropertyInstanceId**成员，指定可扩展交换机策略的实例。

    如果这些成员的值与为其扩展之前已设置了一个交换机策略属性不匹配，该扩展必须故障 OID 集请求使用 NDIS\_状态\_无效\_参数。 否则为该扩展必须完成 OID 集请求并返回 NDIS\_状态\_成功。

-   添加、 删除或更新的交换机策略来筛选或转发扩展可以禁止。 通过完成状态为 OID 请求的扩展插件实现这\_数据\_不\_已接受。

    **请注意**  捕获扩展不能阻止添加或更新的交换机策略。 相反，它必须转发 OID 请求下可扩展交换机控制路径。

     

-   如果捕获或筛选扩展已成功处理的自定义开关策略 OID 集请求，它必须完成 OID 请求，并必须将其转发可扩展交换机控制路径下。

    如果转发扩展已成功处理的自定义开关策略 OID 集请求，它必须完成 OID 请求，并返回相应的 NDIS\_状态\_*Xxx*值。

-   如果扩展不会完成 OID 集请求，它必须调用[ **NdisFOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfoidrequest)可扩展交换机在驱动程序堆栈的下层 OID 请求转发。 在这种情况下，扩展应监视 OID 来检测基础扩展是否已失败 OID 请求的完成状态。

 

 






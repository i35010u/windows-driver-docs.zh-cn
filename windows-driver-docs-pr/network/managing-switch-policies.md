---
title: 管理交换机策略
description: 管理交换机策略
ms.assetid: F2261CA6-2D7A-4499-82F9-7E2D7C9C908D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3645f6da02e6d0d1db8a939ea616b452d4531b0d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567647"
---
# <a name="managing-switch-policies"></a>管理交换机策略


筛选和转发扩展的 HYPER-V 可扩展交换机可以提供自定义开关属性的属性。 预配后，这些扩展执行时获取可扩展交换机入口数据路径上的数据包中筛选出的策略。 有关这些策略的详细信息，请参阅[交换机策略](switch-policies.md)。

HYPER-V 可扩展交换机接口使用以下对象标识符 (Oid) 来预配筛选和转发扩展的自定义开关策略属性：

<a href="" id="oid-switch-property-add"></a>[OID\_交换机\_属性\_添加](https://msdn.microsoft.com/library/windows/hardware/hh598280)  
通知的 WMI 管理层的属性添加的基础扩展的可扩展交换机的协议边缘颁发此 OID 集请求。 **InformationBuffer**的[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向[ **NDIS\_交换机\_属性\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh598255)结构。

**请注意**  通过指定自定义开关属性[ **NDIS\_切换\_属性\_类型**](https://msdn.microsoft.com/library/windows/hardware/hh598257) 的枚举值**NdisSwitchPropertyTypeCustom**。

 

<a href="" id="oid-switch-property-update"></a>[OID\_交换机\_属性\_更新](https://msdn.microsoft.com/library/windows/hardware/hh598283)  
要通知的 WMI 管理层的属性更新的基础扩展的可扩展交换机的协议边缘颁发此 OID 集请求。 **InformationBuffer**的[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向[ **NDIS\_交换机\_属性\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh598255)结构。

<a href="" id="oid-switch-property-delete"></a>[OID\_交换机\_属性\_删除](https://msdn.microsoft.com/library/windows/hardware/hh598281)  
要通知的 WMI 管理层的属性删除基础扩展的可扩展交换机的协议边缘颁发此 OID 集请求。 **InformationBuffer**的[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向[ **NDIS\_交换机\_属性\_删除\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh598249)结构。

<a href="" id="oid-switch-property-enum"></a>[OID\_交换机\_属性\_枚举](https://msdn.microsoft.com/library/windows/hardware/hh598282)  
该扩展会发送此 OID 方法请求以查询有关可扩展交换机上的当前配置的交换机属性的可扩展交换机的基础的微型端口边缘。 **InformationBuffer**的[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向缓冲区的指针。 此缓冲区包含以下数据：

-   [ **NDIS\_切换\_属性\_枚举\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh598253)结构，它指定为属性枚举的开关参数策略。

-   一个数组[ **NDIS\_交换机\_属性\_枚举\_信息**](https://msdn.microsoft.com/library/windows/hardware/hh598250)结构。 每个这些结构包含有关交换机策略的属性的信息。

    **请注意**  如果**NumProperties**的成员[ **NDIS\_交换机\_属性\_枚举\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh598253)结构设置为零，否[ **NDIS\_交换机\_属性\_枚举\_信息**](https://msdn.microsoft.com/library/windows/hardware/hh598250)返回结构。

     

**请注意**  扩展不是源自 OID 的集请求[OID\_交换机\_属性\_添加](https://msdn.microsoft.com/library/windows/hardware/hh598280)。 [OID\_交换机\_属性\_更新](https://msdn.microsoft.com/library/windows/hardware/hh598283)，或[OID\_开关\_属性\_删除](https://msdn.microsoft.com/library/windows/hardware/hh598281)。

 

可扩展的交换机扩展必须处理的 OID 集请求时请遵循以下准则[OID\_切换\_属性\_添加](https://msdn.microsoft.com/library/windows/hardware/hh598280)， [OID\_交换机\_属性\_更新](https://msdn.microsoft.com/library/windows/hardware/hh598283)，或[OID\_交换机\_属性\_删除](https://msdn.microsoft.com/library/windows/hardware/hh598281):

-   该扩展不能修改[ **NDIS\_交换机\_属性\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh598255)或[ **NDIS\_开关\_属性\_删除\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh598249)与 OID 请求关联的结构。

-   扩展必须处理[OID\_交换机\_属性\_更新](https://msdn.microsoft.com/library/windows/hardware/hh598283)或[OID\_交换机\_属性\_删除](https://msdn.microsoft.com/library/windows/hardware/hh598281)如果该扩展之前已设置了与交换机属性相匹配的以下成员的集请求[ **NDIS\_切换\_属性\_参数** ](https://msdn.microsoft.com/library/windows/hardware/hh598238)或[ **NDIS\_开关\_属性\_删除\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh598249)结构：

    -   **PropertyType**指定开关属性类型的成员。

        **请注意**  从 NDIS 6.30 开始，只能在切换的属性**NdisSwitchPropertyTypeCustom**所指定的[ **NDIS\_切换\_属性\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh598238)或[ **NDIS\_开关\_属性\_删除\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh598249)结构。

         

    -   **PropertyId**成员，用于指定扩展识别的专有 GUID 值。 此 GUID 值创建的独立软件供应商 (ISV)，管理员也可定义自定义可扩展交换机策略属性的格式。

        **请注意**  中包含自定义可扩展交换机策略属性[ **NDIS\_切换\_属性\_自定义**](https://msdn.microsoft.com/library/windows/hardware/hh598247)结构。

         

-   如果该扩展处理这些 OID 集请求，该扩展必须更新或删除交换机策略相匹配的以下成员[ **NDIS\_切换\_属性\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh598255)结构：

    -   **PropertyVersion**成员，指定的可扩展交换机策略的版本。

    -   **PropertyInstanceId**成员，指定可扩展交换机策略的实例。

    如果这些成员的值与为其扩展之前已设置了一个交换机策略属性不匹配，该扩展必须故障 OID 集请求使用 NDIS\_状态\_无效\_参数。 否则为该扩展必须完成 OID 集请求并返回 NDIS\_状态\_成功。

-   添加、 删除或更新的交换机策略来筛选或转发扩展可以禁止。 通过完成状态为 OID 请求的扩展插件实现这\_数据\_不\_已接受。

    **请注意**  捕获扩展不能阻止添加或更新的交换机策略。 相反，它必须转发 OID 请求下可扩展交换机控制路径。

     

-   如果捕获或筛选扩展已成功处理的自定义开关策略 OID 集请求，它必须完成 OID 请求，并必须将其转发可扩展交换机控制路径下。

    如果转发扩展已成功处理的自定义开关策略 OID 集请求，它必须完成 OID 请求，并返回相应的 NDIS\_状态\_*Xxx*值。

-   如果扩展不会完成 OID 集请求，它必须调用[ **NdisFOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561830)可扩展交换机在驱动程序堆栈的下层 OID 请求转发。 在这种情况下，扩展应监视 OID 来检测基础扩展是否已失败 OID 请求的完成状态。

 

 






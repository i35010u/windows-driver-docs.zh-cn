---
title: 管理自定义端口功能状态信息
description: 管理自定义端口功能状态信息
ms.assetid: C989888B-1636-488A-80BF-13D136312417
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1734c3c7d7828fed318dc6a196166be49808a43
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89218044"
---
# <a name="managing-custom-port-feature-status-information"></a>管理自定义端口功能状态信息


Hyper-v 可扩展交换机接口使用以下对象标识符 (OID) 来查询可扩展交换机端口的自定义状态信息。 此状态信息称为 *端口功能状态* 信息：

<a href="" id="oid-switch-port-feature-status-query"></a>[OID \_ 交换机 \_ 端口 \_ 功能 \_ 状态 \_ 查询](./oid-switch-port-feature-status-query.md)  
此 OID 方法请求由可扩展交换机的协议边缘发出，以获取指定端口属性的自定义功能状态信息。

成功从此 OID 方法请求返回后， [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向缓冲区的指针。 此缓冲区包含以下数据：

-   [**NDIS \_ 交换机 \_ 端口 \_ 功能 \_ 状态 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_feature_status_parameters)结构，指定要返回的自定义功能状态信息。

    **注意**   对于自定义功能状态， **FeatureStatusType**成员设置为**NdisSwitchPortPropertyTypeCustom**。

     

-   " [**NDIS \_ 交换机 \_ 端口" \_ 功能 \_ 状态 \_ 自定义**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_feature_status_custom) 结构，其中包含有关分配给可扩展交换机端口的自定义属性的状态信息。

    当可扩展交换机的协议边缘发出 [OID \_ 交换机 \_ 端口 \_ 功能 \_ 状态 \_ 查询](./oid-switch-port-feature-status-query.md) 请求时，它会将 **FeatureStatusCustomBufferLength** 和 **FeatureStatusCustomBufferOffset** 成员设置为 **InformationBuffer** 成员中的一个位置，扩展可使用该位置返回功能状态信息。

可扩展交换机扩展在收到 [oid \_ 交换机 \_ 端口 \_ 功能 \_ 状态 \_ 查询](./oid-switch-port-feature-status-query.md)的 oid 方法请求时必须遵循以下准则：

-   如果扩展插件管理的自定义可扩展交换机端口属性与[**NDIS \_ 交换机 \_ 端口 \_ 功能 \_ 状态 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_feature_status_parameters)结构的**FeatureStatusId**成员匹配，则必须处理 OID 请求。

-   如果扩展处理 OID 方法请求，则它必须返回与 [**NDIS \_ 交换机 \_ 端口 \_ 功能 \_ 状态 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_feature_status_parameters) 结构指定的参数匹配的功能状态信息。

    如果功能状态缓冲区太小，则扩展必须对具有 NDIS \_ 状态无效长度的 OID 请求 \_ 失败 \_ 。 扩展必须设置 **数据。设置 \_ 信息。** 将 [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request) 结构中的成员 BytesNeeded 为所需的最小缓冲区大小。

    否则，扩展必须返回功能状态信息并完成具有 NDIS 状态成功的 OID 请求 \_ \_ 。

-   如果扩展不管理自定义的可扩展交换机属性，则它必须调用 [**NdisFOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest) ，以便将 OID 请求向下转发到可扩展交换机驱动程序堆栈。

    有关如何转发 OID 请求的详细信息，请参阅 [在 NDIS 筛选器驱动程序中筛选 Oid 请求](filtering-oid-requests-in-an-ndis-filter-driver.md)。

有关如何定义和注册端口功能状态信息的详细信息，请参阅 [自定义端口功能状态](custom-port-feature-status.md)。

 


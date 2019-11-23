---
title: 管理自定义端口功能状态信息
description: 管理自定义端口功能状态信息
ms.assetid: C989888B-1636-488A-80BF-13D136312417
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e6f116340e593dd33816e71109f3ccfd6c3ac43
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844125"
---
# <a name="managing-custom-port-feature-status-information"></a>管理自定义端口功能状态信息


Hyper-v 可扩展交换机接口使用以下对象标识符（OID）来查询可扩展交换机端口的自定义状态信息。 此状态信息称为*端口功能状态*信息：

<a href="" id="oid-switch-port-feature-status-query"></a>[OID\_交换机\_端口\_功能\_状态\_查询](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-feature-status-query)  
此 OID 方法请求由可扩展交换机的协议边缘发出，以获取指定端口属性的自定义功能状态信息。

成功从此 OID 方法请求返回后， [**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构包含一个指向**缓冲区的指针**。 此缓冲区包含以下数据：

-   [**NDIS\_交换机\_端口\_功能\_状态\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_feature_status_parameters)结构，指定要返回的自定义功能状态信息。

    **注意**  对于自定义功能状态， **FeatureStatusType**成员设置为**NdisSwitchPortPropertyTypeCustom**。

     

-   [**NDIS\_交换机\_端口\_功能\_状态\_自定义**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_feature_status_custom)结构，其中包含有关分配给可扩展交换机端口的自定义属性的状态信息。

    当可扩展交换机的协议边缘[\_交换机\_端口\_功能\_状态\_查询](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-feature-status-query)请求时，它会将**FeatureStatusCustomBufferLength**和**FeatureStatusCustomBufferOffset**成员设置为**InformationBuffer**成员中的一个位置，扩展可使用该位置返回功能状态信息。

可扩展交换机扩展在收到 Oid 的 OID 方法请求时必须遵循这些准则[\_交换机\_端口\_功能\_状态\_查询](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-feature-status-query)：

-   如果扩展插件管理的自定义可扩展交换机端口属性与[**NDIS\_交换机\_端口\_功能\_状态\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_feature_status_parameters)结构相**匹配，则**必须处理 OID 请求。

-   如果扩展处理 OID 方法请求，则它必须返回与 NDIS 指定的参数匹配的功能状态信息[ **\_交换机\_端口\_功能\_状态\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_feature_status_parameters)结构。

    如果功能状态缓冲区太小，则扩展必须使具有 NDIS\_状态\_无效\_长度的 OID 请求失败。 扩展必须设置**数据。设置\_信息。** \_OID 中的 BytesNeeded 成员[ **\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构到所需的最小缓冲区大小。

    否则，扩展必须返回功能状态信息，并通过 NDIS\_状态完成 OID 请求，\_成功。

-   如果扩展不管理自定义的可扩展交换机属性，则它必须调用[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest) ，以便将 OID 请求向下转发到可扩展交换机驱动程序堆栈。

    有关如何转发 OID 请求的详细信息，请参阅[在 NDIS 筛选器驱动程序中筛选 Oid 请求](filtering-oid-requests-in-an-ndis-filter-driver.md)。

有关如何定义和注册端口功能状态信息的详细信息，请参阅[自定义端口功能状态](custom-port-feature-status.md)。

 

 






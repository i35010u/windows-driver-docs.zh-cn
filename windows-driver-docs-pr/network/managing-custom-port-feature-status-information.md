---
title: 管理自定义端口功能状态信息
description: 管理自定义端口功能状态信息
ms.assetid: C989888B-1636-488A-80BF-13D136312417
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 202b844530a4b68bbbbb3b2c7b071c339281829e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356174"
---
# <a name="managing-custom-port-feature-status-information"></a>管理自定义端口功能状态信息


HYPER-V 可扩展交换机接口为可扩展交换机端口使用查询自定义状态信息的以下对象标识符 (OID)。 此状态信息被称为*端口功能状态*信息：

<a href="" id="oid-switch-port-feature-status-query"></a>[OID\_交换机\_端口\_功能\_状态\_查询](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-feature-status-query)  
获取指定的端口属性的自定义功能状态信息的可扩展交换机的协议边缘颁发此 OID 方法请求。

通过此 OID 方法请求成功返回后**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含指向缓冲区的指针。 此缓冲区包含以下数据：

-   [ **NDIS\_交换机\_端口\_功能\_状态\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_port_feature_status_parameters)结构，它指定自定义功能状态要返回的信息。

    **请注意**  的自定义功能状态**FeatureStatusType**成员设置为**NdisSwitchPortPropertyTypeCustom**。

     

-   [ **NDIS\_交换机\_端口\_功能\_状态\_自定义**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_port_feature_status_custom)结构，其中包含有关的状态信息分配给可扩展交换机端口的自定义属性。

    当发出可扩展交换机的协议边缘[OID\_切换\_端口\_功能\_状态\_查询](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-feature-status-query)请求，它会设置**FeatureStatusCustomBufferLength**并**FeatureStatusCustomBufferOffset**中的某个位置的成员**InformationBuffer**扩展插件可以使用到的成员返回功能的状态信息。

当它收到的 OID 方法请求时，可扩展交换机扩展必须遵循这些准则[OID\_切换\_端口\_功能\_状态\_查询](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-feature-status-query):

-   如果它管理与匹配的自定义可扩展交换机端口属性，该扩展必须处理 OID 请求**FeatureStatusId**的成员[ **NDIS\_切换\_端口\_功能\_状态\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_port_feature_status_parameters)结构。

-   如果该扩展处理 OID 方法请求，它必须返回由指定的参数匹配的功能状态信息[ **NDIS\_交换机\_端口\_功能\_状态\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_port_feature_status_parameters)结构。

    如果功能状态缓冲区太小，该扩展必须故障 OID 请求使用 NDIS\_状态\_无效\_长度。 扩展必须设置**数据。设置\_信息。BytesNeeded**中的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)是必需的最小缓冲区大小的结构。

    否则为该扩展必须返回功能的状态信息并完成 OID 请求使用 NDIS\_状态\_成功。

-   如果扩展不管理自定义可扩展交换机属性，它必须调用[ **NdisFOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfoidrequest)可扩展交换机在驱动程序堆栈的下层 OID 请求转发。

    有关如何将请求转发 OID 的详细信息，请参阅[NDIS 筛选器驱动程序中筛选 OID 请求](filtering-oid-requests-in-an-ndis-filter-driver.md)。

有关如何定义和注册端口功能的状态信息的详细信息，请参阅[自定义端口功能状态](custom-port-feature-status.md)。

 

 






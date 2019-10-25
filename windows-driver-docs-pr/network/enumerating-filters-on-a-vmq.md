---
title: 枚举 VMQ 上的筛选器
description: 枚举 VMQ 上的筛选器
ms.assetid: 6d5d8cb6-7bdf-488b-8fcd-7c6e78c4fb24
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9bbb976e7217d5926460bfcd411bca4a9cdc0282
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834785"
---
# <a name="enumerating-filters-on-a-vmq"></a>枚举 VMQ 上的筛选器





为了获取在接收队列中设置的所有筛选器的列表，过量驱动程序和应用程序可以使用[OID\_接收\_筛选器\_枚举\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)方法对象标识符（OID）请求。

[**Ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员最初包含指向[**NDIS\_接收\_筛选器\_\_数组结构的筛选器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)的指针。 如果它将**NDIS\_接收\_筛选器\_信息\_数组**结构的格式，则过量驱动程序或应用程序必须将**QueueId**成员设置为接收队列的标识符（ID）。 接收队列 ID 通过以下方式获取：

-   过量驱动程序从[oid\_接收\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-allocate-queue)的早期 oid 方法请求中获取接收队列 ID 值，\_分配\_队列或 OID\_\_[枚举\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-queues)\_队列. 驱动程序还可以指定**NDIS\_默认\_接收默认接收队列的\_队列\_ID** 。

-   应用程序从 Oid 的早期 OID 方法请求中获取了接收队列 ID 值[\_接收\_FILTER\_枚举\_队列](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-queues)。 应用程序还可以指定**NDIS\_默认\_接收默认接收队列的\_队列\_ID** 。

成功从 Oid 的 OID 方法请求返回[\_接收\_FILTER\_枚举\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)后， [**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向已更新 Ndis\_的指针将[**接收\_筛选器\_信息\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)结构，后面跟有一个或多个[**NDIS\_\_INFO 结构接收\_筛选器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info)。 每个**NDIS\_接收\_筛选器\_信息**结构指定在指定接收队列中设置的筛选器的 ID。

过量驱动程序或应用程序可以使用[oid\_接收\_筛选器\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-parameters)OID 方法请求，以获取接收队列中特定筛选器的参数。

[**Ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员最初包含指向[**NDIS\_接收\_筛选器\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)结构的指针。 过量驱动程序或应用程序通过将**FilterId**成员设置为要返回其参数的筛选器的非零 ID 值，将**NDIS\_接收\_筛选器\_参数**结构。

**请注意**  过量驱动程序从 oid 的早期 oid 方法请求中获取了筛选器 ID [\_接收\_筛选器\_设置\_筛选](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)器或 OID\_\_[枚举接收\_筛选器\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)。 应用程序只能从 OID 的早期 OID 方法请求中获取筛选器 ID\_接收\_FILTER\_枚举\_筛选器。

 

NDIS 处理[OID\_接收\_筛选器\_枚举\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)和[OID\_接收\_筛选器\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-parameters)方法 OID 请求用于微型端口驱动程序。 NDIS 从 OID 收到的数据的内部缓存获取信息[\_接收\_filter\_设置\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)OID 请求。

 

 






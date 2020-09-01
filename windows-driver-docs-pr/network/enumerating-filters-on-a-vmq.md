---
title: 枚举 VMQ 上的筛选器
description: 枚举 VMQ 上的筛选器
ms.assetid: 6d5d8cb6-7bdf-488b-8fcd-7c6e78c4fb24
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4179c1ece09ad93207b38aaae583c01fff1bedb3
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216196"
---
# <a name="enumerating-filters-on-a-vmq"></a>枚举 VMQ 上的筛选器





为了获取在接收队列中设置的所有筛选器的列表，过量驱动程序和应用程序可以使用 [oid \_ 接收 \_ 筛选器 \_ 枚举 \_ 筛选器](./oid-receive-filter-enum-filters.md) 方法对象标识符 (oid) 请求。

[**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员最初包含指向[**ndis \_ 接收 \_ 筛选器 \_ 信息 \_ 数组**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)结构的指针。 在设置 **NDIS \_ 接收 \_ 筛选器 \_ 信息 \_ 数组** 结构的格式时，过量驱动程序或应用程序必须将 **QueueId** 成员设置为接收队列的标识符 (ID) 。 接收队列 ID 通过以下方式获取：

-   过量驱动程序从 [oid \_ 接收 \_ 筛选器 \_ 分配 \_ 队列](./oid-receive-filter-allocate-queue.md) 或 [oid \_ 接收 \_ 筛选器 \_ 枚举 \_ 队列](./oid-receive-filter-enum-queues.md)的早期 oid 方法请求中获取接收队列 ID 值。 驱动程序还可以为默认接收队列指定 **NDIS \_ 默认 \_ 接收 \_ 队列 \_ ID** 。

-   应用程序从 [oid \_ 接收 \_ 筛选器 \_ 枚举 \_ 队列](./oid-receive-filter-enum-queues.md)的早期 oid 方法请求中获取了接收队列 ID 值。 应用程序还可以为默认接收队列指定 **NDIS \_ 默认 \_ 接收 \_ 队列 \_ ID** 。

成功从[oid \_ 接收 \_ 筛选器 \_ 枚举 \_ 筛选器](./oid-receive-filter-enum-filters.md)的 Oid 方法请求返回后， [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向已更新的[**ndis \_ 接收 \_ 筛选 \_ 信息 \_ 数组**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)结构的指针，该结构后跟一个或多个[**NDIS \_ 接收 \_ 筛选器 \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info)结构。 每个 **NDIS \_ 接收 \_ 筛选器 \_ 信息** 结构指定在指定接收队列中设置的筛选器的 ID。

过量驱动程序或应用程序可以使用 [oid \_ 接收 \_ 筛选器 \_ 参数](./oid-receive-filter-parameters.md) oid 方法请求来获取接收队列中特定筛选器的参数。

[**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员最初包含指向[**ndis \_ 接收 \_ 筛选器 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)结构的指针。 过量驱动程序或应用程序通过将**FilterId**成员设置为要返回其参数的筛选器的非零 ID 值，来设置**NDIS \_ 接收 \_ 筛选器 \_ 参数**结构的格式。

**注意**   过量驱动程序从[oid \_ 接收 \_ 筛选器 \_ 集 \_ 筛选](./oid-receive-filter-set-filter.md)器或[oid \_ 接收 \_ 筛选器 \_ 枚举 \_ 筛选器](./oid-receive-filter-enum-filters.md)的早期 OID 方法请求获取了筛选器 ID。 应用程序只能从 OID \_ 接收 \_ 筛选器 \_ 枚举 \_ 筛选器的早期 oid 方法请求中获取筛选器 ID。

 

NDIS 为微型端口驱动程序处理 [oid \_ 接收 \_ 筛选器 \_ 枚举 \_ 筛选器](./oid-receive-filter-enum-filters.md) 和 [oid \_ 接收 \_ 筛选器 \_ 参数](./oid-receive-filter-parameters.md) 方法 oid 请求。 NDIS 从 [oid \_ 接收 \_ 筛选器 \_ 设置 \_ 筛选器](./oid-receive-filter-set-filter.md) oid 请求收到的数据的内部缓存获取了信息。

 


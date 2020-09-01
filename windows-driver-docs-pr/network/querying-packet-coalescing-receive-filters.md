---
title: 查询数据包合并接收筛选器
description: 查询数据包合并接收筛选器
ms.assetid: D0B41718-37B9-4FB4-BA10-20765F836214
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec6d63b4485522607edcd99ad7c6d0bc7a8c5dc1
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215136"
---
# <a name="querying-packet-coalescing-receive-filters"></a>查询数据包合并接收筛选器





通过执行以下操作，过量驱动程序和应用程序可以查询已下载到微型端口驱动程序的数据包合并接收筛选器：

-   通过发出 [oid 接收筛选器 \_ \_ \_ 枚举 \_ 筛选器](./oid-receive-filter-enum-filters.md)的 oid 方法请求，在微型端口驱动程序上请求接收筛选器的枚举列表。 有关详细信息，请参阅 [在微型端口驱动程序上枚举接收筛选器](#enumerating-the-receive-filters-on-a-miniport-driver)。

-   通过发出 [oid \_ 接收筛选 \_ 器 \_ 参数](./oid-receive-filter-parameters.md)的 oid 方法请求，为微型端口驱动程序上的接收筛选器请求测试条件参数。 有关详细信息，请参阅 [在微型端口驱动程序上查询接收筛选器](#querying-the-parameters-of-a-receive-filters-on-a-miniport-driver)

NDIS 为微型端口驱动程序处理 [oid \_ 接收 \_ 筛选器 \_ 枚举 \_ 筛选器](./oid-receive-filter-enum-filters.md) 和 [oid \_ 接收 \_ 筛选器 \_ 参数](./oid-receive-filter-parameters.md) 方法 oid 请求。 NDIS 从 [oid \_ 接收 \_ 筛选器 \_ 设置 \_ 筛选器](./oid-receive-filter-set-filter.md) oid 请求收到的数据的内部缓存获取了信息。

## <a name="enumerating-the-receive-filters-on-a-miniport-driver"></a>枚举微型端口驱动程序上的接收筛选器


为了获取已下载到微型端口驱动程序的所有数据包合并接收筛选器的列表，过量驱动程序和应用程序会发出 [oid \_ 接收 \_ 筛选器 \_ 枚举 \_ 筛选器](./oid-receive-filter-enum-filters.md)的 oid 方法请求。 [**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS \_ 接收 \_ 筛选器 \_ 信息 \_ 数组**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)结构的指针。

**注意**   当过量驱动程序或应用程序初始化[**ndis \_ 接收 \_ 筛选器 \_ 信息 \_ 数组**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)结构时，它必须将**QueueId**成员设置为 NDIS \_ 默认 \_ 接收 \_ 队列 \_ ID。

 

成功从 OID 方法请求返回后， [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向缓冲区的指针。 此缓冲区的格式设置为包含以下内容：

-   [**NDIS \_ 接收 \_ 筛选 \_ 信息 \_ 数组**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)结构，指定当前在微型端口驱动程序上配置的接收筛选器的列表。

-   与当前在微型端口驱动程序上配置的接收筛选器有关的 [**NDIS \_ 接收 \_ 筛选器 \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info) 结构的数组。

## <a name="querying-the-parameters-of-a-receive-filters-on-a-miniport-driver"></a>在微型端口驱动程序上查询接收筛选器的参数


为了获取已下载到微型端口驱动程序的特定包合并接收筛选器的参数，过量驱动程序或应用程序发出 [oid \_ 接收 \_ 筛选器 \_ 参数](./oid-receive-filter-parameters.md)的 oid 方法请求。 [**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS \_ 接收 \_ 筛选器 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)结构的指针。 过量驱动程序或应用程序通过将**FilterId**成员设置为要返回其参数的筛选器的非零 ID 值来初始化**NDIS \_ 接收 \_ 筛选器 \_ 参数**结构。

**注意**   过量驱动程序从[oid \_ 接收 \_ 筛选器 \_ 集 \_ 筛选](./oid-receive-filter-set-filter.md)器或[oid \_ 接收 \_ 筛选器 \_ 枚举 \_ 筛选器](./oid-receive-filter-enum-filters.md)的早期 OID 方法请求获取了筛选器 ID。 应用程序只能从 OID \_ 接收 \_ 筛选器 \_ 枚举 \_ 筛选器的早期 oid 方法请求中获取筛选器 ID。

 

成功从 OID 方法请求返回后， [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向缓冲区的指针。 此缓冲区的格式设置为包含以下内容：

-   用于指定 NDIS 接收筛选器参数的 [**ndis \_ 接收 \_ 筛选器 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters) 结构。

-   用于为网络数据包标头中的一个字段指定筛选器测试条件的 [**NDIS \_ 接收 \_ 筛选器 \_ 字段 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters) 结构的数组。

 


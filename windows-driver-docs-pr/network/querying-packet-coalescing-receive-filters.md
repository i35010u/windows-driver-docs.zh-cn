---
title: 查询数据包合并接收筛选器
description: 查询数据包合并接收筛选器
ms.assetid: D0B41718-37B9-4FB4-BA10-20765F836214
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 61917538b8948893bc62f95c145c32638c5e74f8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844882"
---
# <a name="querying-packet-coalescing-receive-filters"></a>查询数据包合并接收筛选器





通过执行以下操作，过量驱动程序和应用程序可以查询已下载到微型端口驱动程序的数据包合并接收筛选器：

-   通过向[oid\_接收\_FILTER\_枚举\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)发出 OID 的 oid 方法请求，来请求微型端口驱动程序上接收筛选器的枚举列表。 有关详细信息，请参阅[在微型端口驱动程序上枚举接收筛选器](#enumerating-the-receive-filters-on-a-miniport-driver)。

-   通过向[oid\_接收\_filter\_参数发出 oid](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-parameters)方法请求来请求微型端口驱动程序上接收筛选器的测试条件参数。 有关详细信息，请参阅[在微型端口驱动程序上查询接收筛选器](#querying-the-parameters-of-a-receive-filters-on-a-miniport-driver)

NDIS 处理[OID\_接收\_筛选器\_枚举\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)和[OID\_接收\_筛选器\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-parameters)方法 OID 请求用于微型端口驱动程序。 NDIS 从 OID 收到的数据的内部缓存获取信息[\_接收\_filter\_设置\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)OID 请求。

## <a name="enumerating-the-receive-filters-on-a-miniport-driver"></a>枚举微型端口驱动程序上的接收筛选器


为了获取已下载到微型端口驱动程序的所有数据包合并接收筛选器的列表，过量驱动程序和应用程序会发出 oid 的 OID 方法请求[\_接收\_FILTER\_枚举\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)。 [ **\_OID 的 ndis\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**ndis\_\_筛选器\_\_数组结构的筛选器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)的指针。

**请注意**  当过量驱动程序或应用程序初始化[**NDIS\_接收\_筛选器\_信息\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)结构时，它必须将**QueueId**成员设置为 NDIS\_默认\_接收\_队列\_ID。

 

成功从 OID 方法请求返回后， [**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构包含一个指向**缓冲区的指针**。 此缓冲区的格式设置为包含以下内容：

-   [**NDIS\_接收\_筛选器\_信息\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)结构，该结构指定当前在微型端口驱动程序上配置的接收筛选器的列表。

-   一组[**NDIS\_接收\_筛选器\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info)结构有关当前在微型端口驱动程序上配置的接收筛选器。

## <a name="querying-the-parameters-of-a-receive-filters-on-a-miniport-driver"></a>在微型端口驱动程序上查询接收筛选器的参数


为了获取已下载到微型端口驱动程序的特定包合并接收筛选器的参数，过量驱动程序或应用程序会发出 oid 的 OID 方法请求[\_接收\_filter\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-parameters)。 [ **\_OID 的 ndis\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS\_接收\_筛选器\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)结构的指针。 过量驱动程序或应用程序通过将**FilterId**成员设置为要返回其参数的筛选器的非零 ID 值，来初始化**NDIS\_接收\_筛选器\_参数**结构。

**请注意**  过量驱动程序从 oid 的早期 oid 方法请求中获取了筛选器 ID [\_接收\_筛选器\_设置\_筛选](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)器或[OID\_\_枚举\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)筛选器。\_ 应用程序只能从 OID 的早期 OID 方法请求中获取筛选器 ID\_接收\_FILTER\_枚举\_筛选器。

 

成功从 OID 方法请求返回后， [**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构包含一个指向**缓冲区的指针**。 此缓冲区的格式设置为包含以下内容：

-   [**Ndis\_接收\_筛选器，\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)结构，用于指定 NDIS 接收筛选器的参数。

-   一组[**NDIS\_接收\_筛选器\_字段\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters)结构，用于为网络数据包标头中的一个字段指定筛选器测试条件。

 

 






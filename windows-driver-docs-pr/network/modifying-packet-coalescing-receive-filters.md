---
title: 修改数据包合并接收筛选器
description: 修改数据包合并接收筛选器
ms.assetid: 082A969F-2977-482A-B060-ED8D353EC2E9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d76a39853622635ad84d7c63ca7ceb269b1c4fd9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844224"
---
# <a name="modifying-packet-coalescing-receive-filters"></a>修改数据包合并接收筛选器


若要修改支持数据包合并的微型端口驱动程序上的接收筛选器，请执行以下步骤：

1.  为了获取已下载到微型端口驱动程序的所有数据包合并接收筛选器的列表，过量驱动程序会发出 oid 的 OID 方法请求[\_接收\_FILTER\_枚举\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)。 [ **\_OID 的 ndis\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**ndis\_\_筛选器\_\_数组结构的筛选器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)的指针。

    **注意** 当过量驱动程序或应用程序初始化[**NDIS\_接收\_筛选器\_信息\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)结构时，它必须将**QueueId**成员设置为 NDIS\_默认\_接收\_队列\_ID。

    成功从 Oid 的 OID 方法请求返回[\_接收\_FILTER\_枚举\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)后， [**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向已更新 Ndis\_的指针将[**接收\_筛选器\_信息\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)结构，后面跟有一个或多个[**NDIS\_\_INFO 结构接收\_筛选器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info)。 每个**NDIS\_接收\_筛选器\_信息**结构指定网络适配器上设置的筛选器的标识符（ID）。

2.  为了获取已下载到微型端口驱动程序的特定包合并接收筛选器的参数，过量的驱动程序会发出 oid 的 OID 方法请求[\_接收\_filter\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-parameters)。 [ **\_OID 的 ndis\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS\_接收\_筛选器\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)结构的指针。 过量驱动程序或应用程序通过将**FilterId**成员设置为要返回其参数的筛选器的非零 ID 值，来初始化**NDIS\_接收\_筛选器\_参数**结构。

    成功从 OID 方法请求返回后， [**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构包含一个指向**缓冲区的指针**。 此缓冲区的格式设置为包含以下内容：

    -   [**Ndis\_接收\_筛选器，\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)结构，用于指定 NDIS 接收筛选器的参数。

    -   一组[**NDIS\_接收\_筛选器\_字段\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters)结构，用于为网络数据包标头中的一个字段指定筛选器测试条件。

3.  过量驱动程序会修改接收筛选器，以添加、删除或更改筛选器的测试条件集。 驱动程序通过以下方式来实现此功能：添加、删除或修改单个[**ndis\_接收\_FILTER\_字段\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters)结构来自由[**NDIS\_接收\_筛选器指定的字段参数数组\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)结构。

    当过量驱动程序已经完成对测试条件的修改时，它必须更新[**NDIS\_接收\_FILTER\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)结构的成员，以反映对接收筛选器所做的更改。 例如，过量驱动程序必须更新**FieldParametersArrayNumElements**成员，使其包含数组中新数量的元素。

    有关详细信息，请参阅[指定数据包合并接收筛选器](specifying-a-packet-coalescing-receive-filter.md)。

4.  过量驱动程序发出[oid\_接收\_筛选器的 oid 方法请求\_设置\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)，以将修改后的接收筛选器下载到微型端口驱动程序。

    有关详细信息，请参阅[设置数据包合并接收筛选器](setting-a-packet-coalescing-receive-filter.md)。










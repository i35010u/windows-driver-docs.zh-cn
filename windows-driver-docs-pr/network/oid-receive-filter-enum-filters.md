---
title: OID_RECEIVE_FILTER_ENUM_FILTERS
description: 过量驱动程序发出 OID_RECEIVE_FILTER_ENUM_FILTERS 的 OID 方法请求，以获取在网络适配器上配置的所有筛选器的列表。
ms.assetid: 498c1e96-c3ee-4f5d-b0f2-6e88921187e5
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_RECEIVE_FILTER_ENUM_FILTERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 5752c74412f3150fbe2b2153d3234b0b40eb7897
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844012"
---
# <a name="oid_receive_filter_enum_filters"></a>OID\_接收\_筛选器\_枚举\_筛选器


过量驱动程序发出 OID 的 OID 方法请求\_接收\_FILTER\_枚举\_筛选器以获取在网络适配器上配置的所有筛选器的列表。

[ **\_OID 的 ndis\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**ndis\_\_筛选器\_\_数组结构的筛选器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)的指针。

成功从 OID 方法请求返回后， [**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构包含一个指向**缓冲区的指针**。 此缓冲区的格式设置为包含以下内容：

-   [**NDIS\_接收\_筛选器\_信息\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)结构，该结构指定当前在微型端口驱动程序上配置的接收筛选器的列表。

-   一组[**NDIS\_接收\_筛选器\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info)结构。 每个结构都指定当前在微型端口驱动程序上配置的接收筛选器的参数。

<a name="remarks"></a>备注
-------

NDIS 接收筛选器在以下 NDIS 接口中使用：

-   [NDIS 数据包合并](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-packet-coalescing)。 有关如何在此接口中使用接收筛选器的详细信息，请参阅[管理包合并接收筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/managing-packet-coalescing-receive-filters)。

-   [单个根 I/o 虚拟化（sr-iov）](https://docs.microsoft.com/windows-hardware/drivers/network/single-root-i-o-virtualization--sr-iov-)。 有关如何在此接口中使用接收筛选器的详细信息，请参阅[设置虚拟端口上的接收筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/setting-a-receive-filter-on-a-virtual-port)。

-   [虚拟机队列 (VMQ)](https://docs.microsoft.com/windows-hardware/drivers/network/virtual-machine-queue--vmq--in-ndis-6-20)。 有关如何在此接口中使用接收筛选器的详细信息，请参阅[设置和清除 VMQ 筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/setting-and-clearing-vmq-filters)。

过量驱动程序或应用程序发出 oid\_接收\_筛选器的 OID 方法请求\_枚举\_筛选器，以枚举网络适配器上设置的接收筛选器。 这包括在 SR-IOV 虚拟端口（VPort）或 VMQ 接收队列上设置的接收筛选器。

### <a name="additional-guidelines-for-the-ndis-packet-coalescing-interface"></a>NDIS 数据包合并接口的其他准则

从 Windows Server 2012 开始，NDIS 数据包合并仅支持网络适配器的默认接收队列。

为了枚举数据包合并接收筛选器，过量驱动程序必须将[**ndis\_接收\_筛选器\_信息\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)结构的**QueueId**成员设置为 NDIS\_默认\_接收\_队列\_ID。

### <a name="additional-guidelines-for-the-sr-iov-interface"></a>SR-IOV 接口的其他准则

从 Windows Server 2012 开始，SR-IOV 接口仅支持虚拟端口（VPort）的默认接收队列。

若要枚举 VPort 接收筛选器，过量驱动程序必须将[**ndis\_接收\_筛选器\_信息\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)结构的**QueueId**成员设置为 NDIS\_默认\_接收\_队列\_ID。

### <a name="additional-guidelines-for-the-vmq-interface"></a>有关 VMQ 接口的其他准则

过量驱动程序可以发出 OID\_接收\_筛选器的 OID 方法请求\_枚举\_筛选器，以枚举在 VMQ 接收队列上设置的接收筛选器。 当过量驱动程序初始化[**NDIS\_接收\_筛选器\_信息\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)结构时，它会将**QueueId**成员设置为以下值之一：

-   非默认接收队列的队列标识符值。 过量驱动程序从 Oid 的早期 OID 方法请求中获取队列标识符输入值[\_接收\_FILTER\_分配\_队列](oid-receive-filter-allocate-queue.md)，或 OID [\_接收\_筛选器的 oid 查询请求\_枚举\_队列](oid-receive-filter-enum-queues.md)。

-   NDIS\_默认\_的队列标识符值接收\_队列\_ID，该 ID 指定默认接收队列。

### <a name="return-status-codes"></a>返回状态代码

NDIS 处理 OID\_接收\_筛选器的 OID 方法请求\_小型端口驱动程序的枚举\_筛选器，并返回以下状态代码之一：

<a href="" id="ndis-status-success"></a>成功的 NDIS\_状态\_  
请求已成功完成。 **InformationBuffer**指向[**NDIS\_接收\_筛选器\_信息\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)结构。

<a href="" id="ndis-status-pending"></a>NDIS\_状态\_挂起  
请求正在等待完成。 请求完成后，NDIS 会将最终状态代码和结果传递给调用方的 OID 请求完成处理程序。

<a href="" id="ndis-status-invalid-length"></a>NDIS\_状态\_无效的\_长度  
信息缓冲区太短。 NDIS 设置**数据。查询\_信息。** \_OID 中的 BytesNeeded 成员[ **\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构到所需的最小缓冲区大小。

<a href="" id="ndis-status-failure"></a>\_故障时的 NDIS\_状态  
由于其他原因，请求失败。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>在 NDIS 6.20 和更高版本中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_接收\_筛选器\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info)

[**NDIS\_接收\_筛选器\_信息\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)

[OID\_接收\_筛选器\_分配\_队列](oid-receive-filter-allocate-queue.md)

[OID\_接收\_筛选器\_枚举\_队列](oid-receive-filter-enum-queues.md)

[OID\_接收\_筛选器\_设置\_筛选器](oid-receive-filter-set-filter.md)

 

 





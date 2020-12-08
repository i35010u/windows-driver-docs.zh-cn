---
title: OID_RECEIVE_FILTER_ENUM_FILTERS
description: 过量驱动程序发出 OID_RECEIVE_FILTER_ENUM_FILTERS 的 OID 方法请求，以获取在网络适配器上配置的所有筛选器的列表。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_RECEIVE_FILTER_ENUM_FILTERS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 8f7f2047e4cec2ee8c9ae3284330d71be25f049b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786091"
---
# <a name="oid_receive_filter_enum_filters"></a>OID \_ 接收 \_ 筛选器 \_ 枚举 \_ 筛选器


过量驱动程序发出 OID \_ 接收筛选器枚举筛选器的 oid 方法请求 \_ \_ \_ ，以获取在网络适配器上配置的所有筛选器的列表。

[**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 **InformationBuffer** 成员包含指向 [**NDIS \_ 接收 \_ 筛选器 \_ 信息 \_ 数组**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)结构的指针。

成功从 OID 方法请求返回后， [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 **InformationBuffer** 成员包含指向缓冲区的指针。 此缓冲区的格式设置为包含以下内容：

-   [**NDIS \_ 接收 \_ 筛选 \_ 信息 \_ 数组**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)结构，指定当前在微型端口驱动程序上配置的接收筛选器的列表。

-   [**NDIS \_ 接收 \_ 筛选 \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info)结构的数组。 每个结构都指定当前在微型端口驱动程序上配置的接收筛选器的参数。

<a name="remarks"></a>备注
-------

NDIS 接收筛选器在以下 NDIS 接口中使用：

-   [NDIS 数据包合并](./ndis-packet-coalescing.md)。 有关如何在此接口中使用接收筛选器的详细信息，请参阅 [管理包合并接收筛选器](./guidelines-for-managing-packet-coalescing-receive-filters.md)。

-   [单个根 I/o 虚拟化 (sr-iov) ](./single-root-i-o-virtualization--sr-iov-.md)。 有关如何在此接口中使用接收筛选器的详细信息，请参阅 [设置虚拟端口上的接收筛选器](./setting-a-receive-filter-on-a-virtual-port.md)。

-   [虚拟机队列 (VMQ)](./virtual-machine-queue--vmq--in-ndis-6-20.md)。 有关如何在此接口中使用接收筛选器的详细信息，请参阅 [设置和清除 VMQ 筛选器](./setting-and-clearing-vmq-filters.md)。

过量驱动程序或应用程序发出 oid 的 oid 方法请求， \_ \_ \_ \_ 以枚举网络适配器上设置的接收筛选器。 这包括在 SR-IOV 虚拟端口 (VPort) 或 VMQ 接收队列上设置的接收筛选器。

### <a name="additional-guidelines-for-the-ndis-packet-coalescing-interface"></a>NDIS 数据包合并接口的其他准则

从 Windows Server 2012 开始，NDIS 数据包合并仅支持网络适配器的默认接收队列。

为了枚举数据包合并接收筛选器，过量驱动程序必须将 [**ndis \_ 接收 \_ 筛选器 \_ 信息 \_ 数组**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)结构的 **QueueId** 成员设置为 ndis \_ 默认 \_ 接收 \_ 队列 \_ ID。

### <a name="additional-guidelines-for-the-sr-iov-interface"></a>SR-IOV 接口的其他准则

从 Windows Server 2012 开始，SR-IOV 接口仅支持 (VPort) 的虚拟端口的默认接收队列。

为了枚举 VPort 接收筛选器，过量驱动程序必须将 [**ndis \_ 接收 \_ 筛选器 \_ 信息 \_ 数组**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)结构的 **QueueId** 成员设置为 ndis \_ 默认 \_ 接收 \_ 队列 \_ ID。

### <a name="additional-guidelines-for-the-vmq-interface"></a>有关 VMQ 接口的其他准则

过量驱动程序可以发出 OID \_ 接收筛选器枚举筛选器的 oid 方法请求 \_ \_ \_ ，以枚举在 VMQ 接收队列上设置的接收筛选器。 当过量驱动程序初始化 [**NDIS \_ 接收 \_ 筛选器 \_ 信息 \_ 数组**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array) 结构时，它会将 **QueueId** 成员设置为以下值之一：

-   非默认接收队列的队列标识符值。 过量驱动程序从 [oid \_ 接收 \_ 筛选器 \_ 分配 \_ 队列](oid-receive-filter-allocate-queue.md) 的较早 oid 方法请求中获取队列标识符输入值，或者为 [oid \_ 接收 \_ 筛选器 \_ 枚举 \_ 队列](oid-receive-filter-enum-queues.md)从 oid 查询请求中获取。

-   NDIS \_ 默认接收队列 ID 的队列标识符值 \_ \_ \_ ，指定默认接收队列。

### <a name="return-status-codes"></a>返回状态代码

NDIS 处理 \_ \_ 微型端口驱动程序的 oid 接收筛选器枚举筛选器的 oid 方法请求 \_ \_ ，并返回以下状态代码之一：

<a href="" id="ndis-status-success"></a>NDIS \_ 状态 \_ 成功  
请求已成功完成。 **InformationBuffer** 指向 [**NDIS \_ 接收 \_ 筛选器 \_ 信息 \_ 数组**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)结构。

<a href="" id="ndis-status-pending"></a>NDIS \_ 状态 \_ 挂起  
请求正在等待完成。 请求完成后，NDIS 会将最终状态代码和结果传递给调用方的 OID 请求完成处理程序。

<a href="" id="ndis-status-invalid-length"></a>NDIS \_ 状态 \_ 无效 \_ 长度  
信息缓冲区太短。 NDIS 设置 **数据。查询 \_ 信息。** 将 [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request) 结构中的成员 BytesNeeded 为所需的最小缓冲区大小。

<a href="" id="ndis-status-failure"></a>NDIS \_ 状态 \_ 故障  
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
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS \_ 接收 \_ 筛选器 \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info)

[**NDIS \_ 接收 \_ 筛选器 \_ 信息 \_ 数组**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)

[OID \_ 接收 \_ 筛选器 \_ 分配 \_ 队列](oid-receive-filter-allocate-queue.md)

[OID \_ 接收 \_ 筛选器 \_ 枚举 \_ 队列](oid-receive-filter-enum-queues.md)

[OID \_ 接收 \_ 筛选器 \_ 集 \_ 筛选器](oid-receive-filter-set-filter.md)


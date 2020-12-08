---
title: OID_RECEIVE_FILTER_CLEAR_FILTER
description: 过量驱动程序发出 OID 设置 OID_RECEIVE_FILTER_CLEAR_FILTER 的请求，以清除网络适配器上的接收筛选器。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_RECEIVE_FILTER_CLEAR_FILTER 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d0c8ad80c73dc615a1822d72e62cf7733dae68a1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799359"
---
# <a name="oid_receive_filter_clear_filter"></a>OID \_ 接收 \_ 筛选器 \_ 清除 \_ 筛选器


过量驱动程序发出 oid 设置 OID \_ 接收 \_ 筛选器 \_ 清除 \_ 筛选器的请求，以清除网络适配器上的接收筛选器。

[**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 **InformationBuffer** 成员包含指向 [**ndis \_ 接收 \_ 筛选器 \_ CLEAR \_ PARAMETERS**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_clear_parameters)结构的指针。

<a name="remarks"></a>备注
-------

NDIS 接收筛选器在以下 NDIS 接口中使用：

-   [NDIS 数据包合并](./ndis-packet-coalescing.md)。 有关如何在此接口中使用接收筛选器的详细信息，请参阅 [管理包合并接收筛选器](./guidelines-for-managing-packet-coalescing-receive-filters.md)。

-   [单个根 I/o 虚拟化 (sr-iov) ](./single-root-i-o-virtualization--sr-iov-.md)。 有关如何在此接口中使用接收筛选器的详细信息，请参阅 [设置虚拟端口上的接收筛选器](./setting-a-receive-filter-on-a-virtual-port.md)。

-   [虚拟机队列 (VMQ)](./virtual-machine-queue--vmq--in-ndis-6-20.md)。 有关如何在此接口中使用接收筛选器的详细信息，请参阅 [设置和清除 VMQ 筛选器](./setting-and-clearing-vmq-filters.md)。

\_ \_ \_ \_ 对于支持 NDIS 数据包合并、sr-iov 或 VMQ 接口的微型端口驱动程序，oid 设置 oid 接收筛选器清除筛选器是必需的。

过量驱动程序（如 NDIS 协议或筛选器驱动程序）使用 OID \_ 接收 \_ 筛选器 \_ 清除 \_ 筛选器集请求来清除以前设置的筛选器。 只有设置接收筛选器的驱动程序才能将其清除。

过量驱动程序通过将 [**NDIS \_ 接收 \_ 筛选器 \_ \_**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_clear_parameters)的 **FilterId** 成员设置为筛选器的标识符，清除接收筛选器。 驱动程序从 [oid \_ 接收 \_ 筛选器 \_ 集 \_ 筛选](oid-receive-filter-set-filter.md)器的早期 oid 方法请求中获取了筛选器标识符。

### <a name="additional-instructions-for-ndis-packet-coalescing"></a>有关 NDIS 数据包合并的其他说明

以下要点适用于支持 NDIS 数据包合并的微型端口和过量驱动程序：

-   过量驱动程序必须清除它在微型端口驱动程序上设置的所有接收筛选器，然后再解除绑定或从驱动程序分离。

### <a name="additional-guidelines-for-the-sr-iov-interface"></a>SR-IOV 接口的其他准则

以下几点适用于支持 SR-IOV 接口的微型端口和过量驱动程序：

-   过量驱动程序必须清除它在 SR-IOV VPort 上设置的所有筛选器，然后才能释放 VPort。 过量驱动程序还必须清除它在默认 VPort 上设置的所有筛选器，然后再将其绑定到网络适配器。

-   如果某个小型小型驱动程序已完成 OID \_ 接收 \_ 筛选器 \_ 清除筛选器的 oid 请求 \_ 以清除 VPort 上的最后一个筛选器，则该驱动程序不能在非默认 VPort 上指示数据包。

    **注意**  如果某个小型小型驱动程序已经完成 [oid \_ NIC \_ 交换机 \_ DELETE \_ VPort](oid-nic-switch-delete-vport.md) 的 oid 请求以释放 VPort，则它也不能在非默认 VPort 上指示数据包。

     

### <a name="additional-guidelines-for-the-vmq-interface"></a>有关 VMQ 接口的其他准则

以下几点适用于支持 VMQ 接口的微型端口和过量驱动程序：

-   过量驱动程序必须清除它在 VMQ 接收队列上设置的所有筛选器，然后才能释放队列。 在关闭到网络适配器的绑定之前，过量驱动程序还必须清除它在默认或删除队列上设置的所有筛选器。

-   如果某个小型小型驱动程序已完成 OID \_ 接收 \_ 筛选器 \_ 清除筛选器的 oid 请求 \_ 以清除接收队列中的最后一个筛选器，则该驱动程序不能在接收队列中指示数据包。

    **注意**  如果某个微型端口驱动程序已经完成 [oid \_ 接收 \_ 筛选器 \_ \_](oid-receive-filter-free-queue.md) 的 oid 请求，则该驱动程序也不能在接收队列中指示数据包，以释放接收队列。

     

### <a name="return-status-codes"></a>返回状态代码

微型端口驱动程序的 [*MiniportOidRequest*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request) 函数为此请求返回以下值之一：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>术语</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>NDIS_STATUS_SUCCESS</strong></p></td>
<td><p>微型端口驱动程序已成功完成请求。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_PENDING</strong></p></td>
<td><p>微型端口驱动程序将异步完成请求。 当微型端口驱动程序完成所有处理后，它必须通过调用 <a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete" data-raw-source="[&lt;strong&gt;NdisMOidRequestComplete&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)"><strong>NdisMOidRequestComplete</strong></a> 函数来成功请求，同时传递 <strong>NDIS_STATUS_SUCCESS</strong> 的 <em>状态</em> 参数。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_NOT_ACCEPTED</strong></p></td>
<td><p>微型端口适配器已被意外删除。</p></td>
</tr>
</tbody>
</table>

 

NDIS 为此请求返回以下状态代码之一：

<a href="" id="ndis-status-success"></a>**NDIS \_ 状态 \_ 成功**  
已成功清除指定的筛选器。

<a href="" id="ndis-status-pending"></a>**NDIS \_ 状态 \_ 挂起**  
请求正在等待完成。 请求完成后，NDIS 会将最终状态代码和结果传递给调用方的 OID 请求完成处理程序。

<a href="" id="ndis-status-file-not-found"></a>**\_ \_ \_ \_ 找不到 NDIS 状态文件**  
筛选器标识符无效。

<a href="" id="ndis-status-invalid-length"></a>**NDIS \_ 状态 \_ 无效 \_ 长度**  
信息缓冲区太小。 NDIS 设置 **数据。设置 \_ 信息。** 将 [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request) 结构中的成员 BytesNeeded 为所需的最小缓冲区大小。

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

[**NDIS \_ 接收 \_ 筛选器 \_ 清除 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_clear_parameters)

[OID \_ NIC \_ 交换机 \_ 删除 \_ VPORT](oid-nic-switch-delete-vport.md)

[OID \_ 接收 \_ 筛选器 \_ 可用 \_ 队列](oid-receive-filter-free-queue.md)

[OID \_ 接收 \_ 筛选器 \_ 集 \_ 筛选器](oid-receive-filter-set-filter.md)

---
title: OID_RECEIVE_FILTER_CLEAR_FILTER
description: 过量驱动程序发出 OID 设置 OID_RECEIVE_FILTER_CLEAR_FILTER 的请求，以清除网络适配器上的接收筛选器。
ms.assetid: 5e92a11a-468e-431d-b4e5-7b0da3847e8a
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_RECEIVE_FILTER_CLEAR_FILTER 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b5f9791eca2fbabaac7db3b92aa75fc49a9dcdf3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844020"
---
# <a name="oid_receive_filter_clear_filter"></a>OID\_接收\_筛选器\_清除\_筛选器


过量驱动程序发出 oid 设置 OID\_接收\_筛选器的请求\_清除\_筛选器以清除网络适配器上的接收筛选器。

[**Ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS\_接收\_筛选器的指针，\_清除\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_clear_parameters)结构。

<a name="remarks"></a>备注
-------

NDIS 接收筛选器在以下 NDIS 接口中使用：

-   [NDIS 数据包合并](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-packet-coalescing)。 有关如何在此接口中使用接收筛选器的详细信息，请参阅[管理包合并接收筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/managing-packet-coalescing-receive-filters)。

-   [单个根 I/o 虚拟化（sr-iov）](https://docs.microsoft.com/windows-hardware/drivers/network/single-root-i-o-virtualization--sr-iov-)。 有关如何在此接口中使用接收筛选器的详细信息，请参阅[设置虚拟端口上的接收筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/setting-a-receive-filter-on-a-virtual-port)。

-   [虚拟机队列 (VMQ)](https://docs.microsoft.com/windows-hardware/drivers/network/virtual-machine-queue--vmq--in-ndis-6-20)。 有关如何在此接口中使用接收筛选器的详细信息，请参阅[设置和清除 VMQ 筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/setting-and-clearing-vmq-filters)。

Oid\_接收\_筛选器的 OID 集请求\_清除\_筛选器是支持 NDIS 数据包合并、SR-IOV 或 VMQ 接口的微型端口驱动程序所必需的。

覆盖驱动程序（如 NDIS 协议或筛选器驱动程序）使用 OID\_接收\_筛选器\_清除\_筛选器集请求以清除以前设置的筛选器。 只有设置接收筛选器的驱动程序才能将其清除。

过量驱动程序通过将[**NDIS\_接收\_筛选器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_clear_parameters)的**FilterId**成员设置为筛选器的标识符\_清除\_参数结构，从而清除接收筛选器。 驱动程序从 Oid 的早期 OID 方法请求中获取了筛选器标识符[\_接收\_filter\_设置\_筛选器](oid-receive-filter-set-filter.md)。

### <a name="additional-instructions-for-ndis-packet-coalescing"></a>有关 NDIS 数据包合并的其他说明

以下要点适用于支持 NDIS 数据包合并的微型端口和过量驱动程序：

-   过量驱动程序必须清除它在微型端口驱动程序上设置的所有接收筛选器，然后再解除绑定或从驱动程序分离。

### <a name="additional-guidelines-for-the-sr-iov-interface"></a>SR-IOV 接口的其他准则

以下几点适用于支持 SR-IOV 接口的微型端口和过量驱动程序：

-   过量驱动程序必须清除它在 SR-IOV VPort 上设置的所有筛选器，然后才能释放 VPort。 过量驱动程序还必须清除它在默认 VPort 上设置的所有筛选器，然后再将其绑定到网络适配器。

-   如果某个微型端口驱动程序已完成 OID\_接收\_筛选器的 OID 请求，则该驱动程序不能在非默认的 VPort 上指示数据包\_清除\_筛选器以清除 VPort 上的最后一个筛选器。

    **请注意**  微型端口驱动程序还不得在非默认 VPort 上指示数据包。如果它已完成 OID 的 oid 请求[\_NIC\_开关\_DELETE\_VPort](oid-nic-switch-delete-vport.md)以释放 VPort。

     

### <a name="additional-guidelines-for-the-vmq-interface"></a>有关 VMQ 接口的其他准则

以下几点适用于支持 VMQ 接口的微型端口和过量驱动程序：

-   过量驱动程序必须清除它在 VMQ 接收队列上设置的所有筛选器，然后才能释放队列。 在关闭到网络适配器的绑定之前，过量驱动程序还必须清除它在默认或删除队列上设置的所有筛选器。

-   如果某个小型小型驱动程序已完成 OID\_接收\_筛选器的 OID 请求，则该驱动程序不能在接收队列中指示数据包，\_清除\_筛选器以清除接收队列中的最后一个筛选器。

    **请注意**  微型端口驱动程序还不得在接收队列中指示数据包，前提是该驱动程序已完成 OID 的 oid 请求[\_接收\_筛选器\_免费\_队列](oid-receive-filter-free-queue.md)来释放接收队列。

     

### <a name="return-status-codes"></a>返回状态代码

微型端口驱动程序的[*MiniportOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)函数为此请求返回以下值之一：

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
<td><p>微型端口驱动程序将异步完成请求。 当微型端口驱动程序完成所有处理后，它必须通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete" data-raw-source="[&lt;strong&gt;NdisMOidRequestComplete&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)"><strong>NdisMOidRequestComplete</strong></a>函数来成功请求，同时传递<strong>NDIS_STATUS_SUCCESS</strong>的<em>状态</em>参数。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_NOT_ACCEPTED</strong></p></td>
<td><p>微型端口适配器已被意外删除。</p></td>
</tr>
</tbody>
</table>

 

NDIS 为此请求返回以下状态代码之一：

<a href="" id="ndis-status-success"></a>**成功的 NDIS\_状态\_**  
已成功清除指定的筛选器。

<a href="" id="ndis-status-pending"></a>**NDIS\_状态\_挂起**  
请求正在等待完成。 请求完成后，NDIS 会将最终状态代码和结果传递给调用方的 OID 请求完成处理程序。

<a href="" id="ndis-status-file-not-found"></a>**找\_不到\_文件\_\_的 NDIS 状态**  
筛选器标识符无效。

<a href="" id="ndis-status-invalid-length"></a>**NDIS\_状态\_无效的\_长度**  
信息缓冲区太小。 NDIS 设置**数据。设置\_信息。** \_OID 中的 BytesNeeded 成员[ **\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构到所需的最小缓冲区大小。

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

[**NDIS\_接收\_筛选器\_清除\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_clear_parameters)

[OID\_NIC\_交换机\_DELETE\_VPORT](oid-nic-switch-delete-vport.md)

[OID\_接收\_筛选器\_可用\_队列](oid-receive-filter-free-queue.md)

[OID\_接收\_筛选器\_设置\_筛选器](oid-receive-filter-set-filter.md)

 

 





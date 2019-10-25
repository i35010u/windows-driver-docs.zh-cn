---
title: OID_RECEIVE_FILTER_SET_FILTER
description: 过量驱动程序发出 OID_RECEIVE_FILTER_SET_FILTER 的 OID 方法请求，以在网络适配器上设置筛选器。
ms.assetid: ec3e119e-662f-48a6-8c68-20da20590b24
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_RECEIVE_FILTER_SET_FILTER 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: cf6848f8bccc829dcad2bb01c42e60469a76da73
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843996"
---
# <a name="oid_receive_filter_set_filter"></a>OID\_接收\_筛选器\_设置\_筛选器

过量驱动程序发出 OID\_接收\_筛选器的 OID 方法请求\_将\_筛选器设置为在网络适配器上设置筛选器。

[ **\_OID 的 NDIS\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向调用方分配的缓冲区的指针。 此缓冲区的格式设置为包含以下内容：

-   [**Ndis\_接收\_筛选器，\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)结构，用于指定 NDIS 接收筛选器的参数。

-   一组[**NDIS\_接收\_筛选器\_字段\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters)结构，后者指定网络数据包标头中的字段的筛选器测试条件。

成功从 OID 方法请求返回后， [**ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS\_接收\_筛选器的指针\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)构造. 如果过量驱动程序正在创建新的接收筛选器，NDIS 将使用新的筛选器标识符更新此结构。

<a name="remarks"></a>备注
-------

NDIS 接收筛选器在以下 NDIS 接口中使用：

-   [NDIS 数据包合并](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-packet-coalescing)。 有关如何在此接口中使用接收筛选器的详细信息，请参阅[管理包合并接收筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/managing-packet-coalescing-receive-filters)。

-   [单个根 I/o 虚拟化（sr-iov）](https://docs.microsoft.com/windows-hardware/drivers/network/single-root-i-o-virtualization--sr-iov-)。 有关如何在此接口中使用接收筛选器的详细信息，请参阅[设置虚拟端口上的接收筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/setting-a-receive-filter-on-a-virtual-port)。

-   [虚拟机队列 (VMQ)](https://docs.microsoft.com/windows-hardware/drivers/network/virtual-machine-queue--vmq--in-ndis-6-20)。 有关如何在此接口中使用接收筛选器的详细信息，请参阅[设置和清除 VMQ 筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/setting-and-clearing-vmq-filters)。

Oid\_接收\_筛选器的 OID 方法请求\_设置\_筛选器对于支持 NDIS 数据包合并、SR-IOV 或 VMQ 接口的微型端口驱动程序是必需的。

过量驱动程序初始化[**NDIS\_接收\_筛选器\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)结构，其请求的筛选器配置。 NDIS 在 NDIS\_接收\_筛选器\_参数结构的**FilterId**成员中分配筛选器标识符，并将方法请求传递到基础微型端口驱动程序。

在接收队列上设置的每个筛选器都有一个用于网络适配器的唯一筛选器标识符。 也就是说，筛选器标识符不会复制到网络适配器管理的不同队列。 当 NDIS 接收到在接收队列上设置筛选器的 OID 请求时，它将验证筛选器参数。 在 NDIS 分配所需的资源和筛选器标识符后，它会将 OID 请求提交到基础网络适配器。 如果网络适配器可以成功分配筛选器所需的软件和硬件资源，它将完成 OID 请求，返回状态为 NDIS\_状态\_SUCCESS。

**注意** 从 NDIS 6.30 开始，仅在网络适配器的默认接收队列中支持数据包合并接收筛选器。 此接收队列具有 NDIS\_默认\_接收\_队列\_ID 的标识符。



微型端口驱动程序必须保留已分配接收筛选器的筛选标识符。 NDIS 使用后面 OID 请求中的筛选器的标识符来更改接收筛选器参数或清除接收筛选器。

在微型端口驱动程序接收[OID 后\_接收\_筛选器\_队列\_分配\_完成](oid-receive-filter-queue-allocation-complete.md)请求，并包含在队列中设置的筛选器，队列处于 "*正在运行*" 状态。 在此状态下，微型端口驱动程序可以通过调用[**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)在队列中启动数据包的指示。

### <a name="additional-guidelines-for-the-sr-iov-interface"></a>SR-IOV 接口的其他准则

以下几点适用于支持 SR-IOV 接口的微型端口驱动程序：

-   对于 SR-IOV 接口，会在默认或非默认虚拟端口（VPort）上创建接收队列。

    **注意** 从 Windows Server 2012 开始，SR-IOV 接口仅支持 VPort 的默认接收队列。

    通过 OID\_NIC 的 OID 集请求来分配 SR-IOV 后[\_交换机\_创建\_VPort](oid-nic-switch-create-vport.md)，因此，过量驱动程序可以使用 OID 的 oid 请求在 VPort 上设置筛选器\_\_\_\_筛选器。

    **注意** 只有分配了 VPort 的过量驱动程序可以对该 VPort 设置筛选器。

-   由于默认 VPort 始终存在，因此过量驱动程序始终可以在默认的 VPort 上设置筛选器。

-   当创建 VPort 时，不会对其设置任何接收筛选器。 在这种情况下，微型端口驱动程序不得在微型端口驱动程序接收 oid\_接收\_筛选器的 OID 请求之前指示该 VPort 上的任何接收数据包，\_为 VPort 设置\_筛选器。 发出此 OID 请求后，微型端口驱动程序可以在该 VPort 上指示数据包。

    **注意** 如果微型端口驱动程序在处理 OID\_接收\_FILTER 的 OID 请求时在 VPort 上指示数据包\_\_筛选器，它必须完成 OID 请求并返回 NDIS\_状态\_成功状态代码。

### <a name="additional-guidelines-for-the-vmq-interface"></a>有关 VMQ 接口的其他准则

以下几点适用于支持 VMQ 接口的微型端口驱动程序：

-   分配 VMQ 接收队列后，过量驱动程序可以使用 OID\_接收\_筛选器的 OID 请求，在接收队列中设置筛选器，\_设置\_筛选器。

    **注意** 仅分配有接收队列的协议驱动程序可以对该队列设置筛选器。

-   因为默认队列始终存在，所以过量驱动程序始终可以在默认队列上设置筛选器。 如果网络适配器支持 drop queue，则过量驱动程序可以在放置队列上设置筛选器。

    过量驱动程序不拥有默认或删除队列。 因此，绑定到网络适配器的所有协议驱动程序都使用默认或删除队列。

-   创建接收队列时，不会对其设置任何接收筛选器。 在这种情况下，微型端口驱动程序不得在微型端口驱动程序接收 oid\_接收\_筛选器的 OID 请求之前指示该接收队列中的任何接收数据包，\_为接收队列设置\_筛选器。 发出此 OID 请求后，微型端口驱动程序可以指示该接收队列中的数据包。

    **注意** 如果微型端口驱动程序在处理 OID\_接收\_筛选器的 OID 请求时指示队列上的数据包\_\_筛选器，它必须完成 OID 请求并返回 NDIS\_状态\_成功状态代码。

### <a name="return-status-codes"></a>返回状态代码

对于 oid\_接收\_FILTER\_集\_筛选器，微型端口驱动程序返回以下状态代码之一：

<a href="" id="ndis-status-success"></a>成功的 NDIS\_状态\_  
已成功在队列上设置筛选器。 信息缓冲区包含更新后的[**NDIS\_接收\_筛选器\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)结构。

<a href="" id="ndis-status-pending"></a>NDIS\_状态\_挂起  
请求正在等待完成。 最终状态代码和结果将传递给调用方的 OID 请求完成处理程序。

<a href="" id="ndis-status-invalid-parameter"></a>NDIS\_状态\_无效\_参数  
提供的过量驱动程序的一个或多个参数无效。

<a href="" id="ndis-status-invalid-length"></a>NDIS\_状态\_无效的\_长度  
信息缓冲区太短。 NDIS 设置**数据。方法\_信息。** \_OID 中的 BytesNeeded 成员[ **\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构到所需的最小缓冲区大小。

<a href="" id="ndis-status-not-supported"></a>不\_支持 NDIS\_状态\_  
此微型端口驱动程序的 NDIS 版本是比6.20 更早的版本。

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


[**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)

[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_接收\_筛选器\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)

[**NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)

[**NET\_BUFFER\_列表\_接收\_筛选器\_ID**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-receive-filter-id)

[OID\_NIC\_交换机\_CREATE\_VPORT](oid-nic-switch-create-vport.md)

[OID\_接收\_筛选器\_清除\_筛选器](oid-receive-filter-clear-filter.md)

[OID\_接收\_筛选器\_队列\_分配\_完成](oid-receive-filter-queue-allocation-complete.md)
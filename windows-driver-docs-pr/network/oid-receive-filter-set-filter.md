---
title: OID_RECEIVE_FILTER_SET_FILTER
description: 过量驱动程序发出 OID_RECEIVE_FILTER_SET_FILTER 的 OID 方法请求，以在网络适配器上设置筛选器。
ms.assetid: ec3e119e-662f-48a6-8c68-20da20590b24
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_RECEIVE_FILTER_SET_FILTER 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 82ec5b468b2f7bad15c0cbf3779ea95d70c6dc36
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91734179"
---
# <a name="oid_receive_filter_set_filter"></a>OID \_ 接收 \_ 筛选器 \_ 集 \_ 筛选器

过量驱动程序发出 OID 方法请求，即 OID \_ 接收 \_ 筛选器 \_ 集 \_ 筛选器，用于在网络适配器上设置筛选器。

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向调用方分配的缓冲区的指针。 此缓冲区的格式设置为包含以下内容：

-   用于指定 NDIS 接收筛选器参数的 [**ndis \_ 接收 \_ 筛选器 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters) 结构。

-   用于指定网络数据包标头中的字段筛选器测试条件的 [**NDIS \_ 接收 \_ 筛选器 \_ 字段 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters) 结构的数组。

成功从 OID 方法请求返回后， [**ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**ndis \_ 接收 \_ 筛选器 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)结构的指针。 如果过量驱动程序正在创建新的接收筛选器，NDIS 将使用新的筛选器标识符更新此结构。

<a name="remarks"></a>备注
-------

NDIS 接收筛选器在以下 NDIS 接口中使用：

-   [NDIS 数据包合并](./ndis-packet-coalescing.md)。 有关如何在此接口中使用接收筛选器的详细信息，请参阅 [管理包合并接收筛选器](./guidelines-for-managing-packet-coalescing-receive-filters.md)。

-   [单个根 I/o 虚拟化 (sr-iov) ](./single-root-i-o-virtualization--sr-iov-.md)。 有关如何在此接口中使用接收筛选器的详细信息，请参阅 [设置虚拟端口上的接收筛选器](./setting-a-receive-filter-on-a-virtual-port.md)。

-   [虚拟机队列 (VMQ)](./virtual-machine-queue--vmq--in-ndis-6-20.md)。 有关如何在此接口中使用接收筛选器的详细信息，请参阅 [设置和清除 VMQ 筛选器](./setting-and-clearing-vmq-filters.md)。

OID \_ 接收 \_ 筛选器集筛选器的 oid 方法请求 \_ \_ 是支持 NDIS 数据包合并、sr-iov 或 VMQ 接口的微型端口驱动程序所必需的。

过量驱动程序用其请求的筛选器配置初始化 [**NDIS \_ 接收 \_ 筛选器 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters) 结构。 NDIS 在 NDIS 接收筛选器参数结构的 **FilterId** 成员中分配筛选器标识符 \_ \_ \_ ，并将该方法请求传递到基础微型端口驱动程序。

在接收队列上设置的每个筛选器都有一个用于网络适配器的唯一筛选器标识符。 也就是说，筛选器标识符不会复制到网络适配器管理的不同队列。 当 NDIS 接收到在接收队列上设置筛选器的 OID 请求时，它将验证筛选器参数。 在 NDIS 分配所需的资源和筛选器标识符后，它会将 OID 请求提交到基础网络适配器。 如果网络适配器可以成功分配筛选器所需的软件和硬件资源，则它将完成 OID 请求，返回状态为 NDIS \_ 状态 \_ 成功。

**注意**  从 NDIS 6.30 开始，仅在网络适配器的默认接收队列中支持数据包合并接收筛选器。 此接收队列具有 NDIS \_ 默认 \_ 接收 \_ 队列 ID 的标识符 \_ 。



微型端口驱动程序必须保留已分配接收筛选器的筛选标识符。 NDIS 使用后面 OID 请求中的筛选器的标识符来更改接收筛选器参数或清除接收筛选器。

当微型端口驱动程序收到 [OID \_ 接收 \_ 筛选器 \_ 队列 \_ 分配 \_ 完成](oid-receive-filter-queue-allocation-complete.md) 请求并且它具有在队列中设置的筛选器后，该队列将处于 " *正在运行* " 状态。 在此状态下，微型端口驱动程序可以通过调用 [**NdisMIndicateReceiveNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)在队列中启动数据包的指示。

### <a name="additional-guidelines-for-the-sr-iov-interface"></a>SR-IOV 接口的其他准则

以下几点适用于支持 SR-IOV 接口的微型端口驱动程序：

-   对于 SR-IOV 接口，会在默认或非默认的虚拟端口 (VPort) 上创建接收队列。

    **注意**  从 Windows Server 2012 开始，SR-IOV 接口仅支持 VPort 的默认接收队列。

    通过 oid [ \_ NIC \_ 交换机 \_ CREATE \_ VPort](oid-nic-switch-create-vport.md)的 oid 集请求分配 sr-iov VPort 后，过量驱动程序可以使用 oid \_ 接收 \_ 筛选器 \_ 集 \_ 筛选器的 oid 请求在 VPort 上设置筛选器。

    **注意**  只有分配了 VPort 的过量驱动程序可以对该 VPort 设置筛选器。

-   由于默认 VPort 始终存在，因此过量驱动程序始终可以在默认的 VPort 上设置筛选器。

-   当创建 VPort 时，不会对其设置任何接收筛选器。 在这种情况下，微型端口驱动程序不能在微型端口驱动程序接收到 VPort 的 OID \_ 接收 \_ 筛选器 \_ 集 \_ 筛选器的 oid 请求之前，在该 VPort 上不指定任何接收数据包。 发出此 OID 请求后，微型端口驱动程序可以在该 VPort 上指示数据包。

    **注意**  如果微型端口驱动程序在处理 OID 接收筛选器集筛选器的 OID 请求时在 VPort 上指示数据包 \_ \_ \_ \_ ，则它必须完成 OID 请求并返回 NDIS \_ 状态 \_ 成功状态代码。

### <a name="additional-guidelines-for-the-vmq-interface"></a>有关 VMQ 接口的其他准则

以下几点适用于支持 VMQ 接口的微型端口驱动程序：

-   分配 VMQ 接收队列后，过量驱动程序可以使用 OID \_ 接收 \_ 筛选器 \_ 集 \_ 筛选器的 oid 请求对接收队列设置筛选器。

    **注意**  仅分配有接收队列的协议驱动程序可以对该队列设置筛选器。

-   因为默认队列始终存在，所以过量驱动程序始终可以在默认队列上设置筛选器。 如果网络适配器支持 drop queue，则过量驱动程序可以在放置队列上设置筛选器。

    过量驱动程序不拥有默认或删除队列。 因此，绑定到网络适配器的所有协议驱动程序都使用默认或删除队列。

-   创建接收队列时，不会对其设置任何接收筛选器。 在这种情况下，微型端口驱动程序在微型端口驱动程序接收 oid \_ 接收 \_ 筛选器 \_ 集 \_ 筛选器的 oid 请求之前，不能在接收队列中显示接收数据包。 发出此 OID 请求后，微型端口驱动程序可以指示该接收队列中的数据包。

    **注意**  如果微型端口驱动程序在处理 OID 接收筛选器集筛选器的 OID 请求时指示队列上的数据包 \_ \_ \_ \_ ，则必须完成 OID 请求并返回 NDIS \_ 状态 \_ 成功状态代码。

### <a name="return-status-codes"></a>返回状态代码

对于 oid \_ 接收 \_ 筛选器 \_ 集 \_ 筛选器的 oid 方法请求，微型端口驱动程序返回以下状态代码之一：

<a href="" id="ndis-status-success"></a>NDIS \_ 状态 \_ 成功  
已成功在队列上设置筛选器。 信息缓冲区包含更新后的 [**NDIS \_ 接收 \_ 筛选器 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters) 结构。

<a href="" id="ndis-status-pending"></a>NDIS \_ 状态 \_ 挂起  
请求正在等待完成。 最终状态代码和结果将传递给调用方的 OID 请求完成处理程序。

<a href="" id="ndis-status-invalid-parameter"></a>NDIS \_ 状态 \_ 无效 \_ 参数  
提供的过量驱动程序的一个或多个参数无效。

<a href="" id="ndis-status-invalid-length"></a>NDIS \_ 状态 \_ 无效 \_ 长度  
信息缓冲区太短。 NDIS 设置 **数据。方法 \_ 信息。** 将 [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request) 结构中的成员 BytesNeeded 为所需的最小缓冲区大小。

<a href="" id="ndis-status-not-supported"></a>\_ \_ 不支持 NDIS \_ 状态  
此微型端口驱动程序的 NDIS 版本是比6.20 更早的版本。

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

## <a name="see-also"></a>另请参阅


[**NdisMIndicateReceiveNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS \_ 接收 \_ 筛选器 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)

[**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)

[**网络 \_ 缓冲区 \_ 列表 \_ 接收 \_ 筛选器 \_ ID**](/windows-hardware/drivers/ddi/ndis/nf-ndis-net_buffer_list_receive_filter_id)

[OID \_ NIC \_ 交换机 \_ CREATE \_ VPORT](oid-nic-switch-create-vport.md)

[OID \_ 接收 \_ 筛选器 \_ 清除 \_ 筛选器](oid-receive-filter-clear-filter.md)

[OID \_ 接收 \_ 筛选器 \_ 队列 \_ 分配 \_ 完成](oid-receive-filter-queue-allocation-complete.md)
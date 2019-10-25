---
title: OID_RECEIVE_FILTER_FREE_QUEUE
description: NDIS 协议驱动程序发出对象标识符（OID）设置 OID_RECEIVE_FILTER_FREE_QUEUE 的请求，以释放接收队列。
ms.assetid: ee8cff69-2f5e-4798-9c18-28e996dd1dd4
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_RECEIVE_FILTER_FREE_QUEUE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d63764fa3fa4b896b731ad788661b210fb02e5d9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844016"
---
# <a name="oid_receive_filter_free_queue"></a>OID\_接收\_筛选器\_可用\_队列


NDIS 协议驱动程序发出\_接收\_筛选器的对象标识符（OID）设置请求，以释放接收队列\_可用的\_队列。

[**Ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS\_接收\_队列的指针\_免费\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_free_parameters)结构，队列标识符类型为**NDIS\_接收\_队列\_ID**。

<a name="remarks"></a>备注
-------

对于 NDIS 6.20 和更高版本的小型小型驱动程序，oid\_接收\_筛选器\_FREE\_队列是可选的。 这对于支持虚拟机队列接口的微型端口驱动程序是必需的。

当过量驱动程序发出[OID\_接收\_FILTER\_分配\_队列](oid-receive-filter-allocate-queue.md)OID 来分配接收队列时，它会发出 OID\_接收\_筛选器\_免费\_队列 OID 以释放接收使.

当 NDIS 请求微型端口驱动程序释放 VMQ 接收队列时，将执行以下步骤：

1.  网络适配器停止数据的 DMA 传输以接收与接收队列关联的缓冲区，在此之后，队列必须进入 DMA 停止状态。 网络适配器在收到[oid\_接收\_筛选器](oid-receive-filter-clear-filter.md)时可能停止 DMA 活动，\_清除\_筛选 OID 请求以清除接收队列中的最后一个 set 筛选器。

2.  微型端口驱动程序生成[**ndis\_状态\_接收\_队列\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-receive-queue-state)状态指示与[**NDIS\_接收\_队列\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_receive_queue_state)结构集的**QueueState**成员**NdisReceiveQueueOperationalStateDmaStopped**以通知 NDIS 已停止 DMA 传输。

3.  微型端口驱动程序等待该队列的所有指示接收数据包返回到微型端口驱动程序。

4.  通过调用[**NdisFreeSharedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreesharedmemory)，微型端口驱动程序可释放它为网络适配器的接收缓冲区分配的、与队列关联的所有共享内存。

5.  微型端口驱动程序完成 OID\_接收\_FILTER\_可用的\_队列 OID 请求，以释放接收队列。

微型端口驱动程序调用[**NdisFreeSharedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreesharedmemory)函数来释放队列的共享内存。 如果微型端口驱动程序为非默认队列分配了共享内存，则驱动程序将在 OID\_接收\_筛选器的上下文中释放共享内存，\_在释放队列时使用\_队列 OID。 微型端口驱动程序在[*MiniportHaltEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)函数的上下文中为默认队列分配的共享内存可用。

当过量驱动程序释放队列之前，必须释放它在队列上设置的所有筛选器。 此外，在调用[**NdisCloseAdapterEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscloseadapterex)函数以关闭到网络适配器的绑定之前，过量驱动程序必须释放在网络适配器上分配的所有接收队列。 NDIS 在调用微型端口驱动程序的[*MiniportHaltEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)函数之前，释放在网络适配器上分配的所有队列。

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
<td><p>微型端口驱动程序将异步完成请求。 当微型端口驱动程序完成所有处理后，它必须通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete" data-raw-source="[&lt;strong&gt;NdisMOidRequestComplete&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)"><strong>NdisMOidRequestComplete</strong></a>函数（为<em>STATUS</em>参数传递<strong>NDIS_STATUS_SUCCESS</strong> ）成功执行请求。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_NOT_ACCEPTED</strong></p></td>
<td><p>正在重置微型端口驱动程序。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_REQUEST_ABORTED</strong></p></td>
<td><p>微型端口驱动程序已停止处理请求。 例如，NDIS 称为<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset" data-raw-source="[&lt;em&gt;MiniportResetEx&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset)"><em>MiniportResetEx</em></a>函数。</p></td>
</tr>
</tbody>
</table>

 

NDIS 为此请求返回以下状态代码之一：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>状态代码</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>NDIS_STATUS_SUCCESS</strong></p></td>
<td><p>已成功释放请求的队列。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_PENDING</strong></p></td>
<td><p>请求正在等待完成。 请求完成后，NDIS 会将最终状态代码和结果传递给调用方的 OID 请求完成处理程序。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_INVALID_PARAMETER</strong></p></td>
<td><p>队列标识符无效。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_INVALID_LENGTH</strong></p></td>
<td><p>信息缓冲区太短。 NDIS 设置<strong>数据</strong>。<strong>METHOD_INFORMATION</strong>。<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>结构中的<strong>BytesNeeded</strong>成员到所需的最小缓冲区大小。</p></td>
</tr>
</tbody>
</table>

 

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


[*MiniportHaltEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)

[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_接收\_QUEUE\_可用\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_free_parameters)

[**NDIS\_状态\_接收\_队列\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-receive-queue-state)

[**NdisCloseAdapterEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscloseadapterex)

[**NdisFreeSharedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreesharedmemory)

[OID\_接收\_筛选器\_分配\_队列](oid-receive-filter-allocate-queue.md)

 

 





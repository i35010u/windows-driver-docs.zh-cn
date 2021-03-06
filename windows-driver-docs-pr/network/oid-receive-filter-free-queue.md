---
title: OID_RECEIVE_FILTER_FREE_QUEUE
description: NDIS 协议驱动程序 (OID 发出对象标识符) 将 OID_RECEIVE_FILTER_FREE_QUEUE 的请求设置为释放接收队列。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_RECEIVE_FILTER_FREE_QUEUE 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c9d49fdafa88cb0028d2e5d223a9dd5e744c99cb
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248849"
---
# <a name="oid_receive_filter_free_queue"></a>OID \_ 接收 \_ 筛选器 \_ 可用 \_ 队列


NDIS 协议驱动程序发出对象标识符 (OID) 设置 OID \_ 接收 \_ 筛选器 \_ 可用队列的请求 \_ ，以释放接收队列。

[**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 成员包含指向 [**ndis \_ 接收 \_ 队列 \_ 可用 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_free_parameters)结构的指针，该结构具有类型为 **ndis \_ 接收 \_ 队列 \_ ID** 的队列标识符。

<a name="remarks"></a>备注
-------

\_ \_ \_ \_ 对于 NDIS 6.20 和更高版本的微型端口驱动程序，oid 请求 oid 接收筛选器免费队列是可选的。 这对于支持虚拟机队列接口的微型端口驱动程序是必需的。

当过量驱动程序发出 [oid \_ 接收 \_ 筛选器 \_ 分配 \_ 队列](oid-receive-filter-allocate-queue.md) oid 来分配接收队列后，它会发出 OID \_ 接收 \_ 筛选器 \_ 免费 \_ 队列 oid 来释放接收队列。

当 NDIS 请求微型端口驱动程序释放 VMQ 接收队列时，将执行以下步骤：

1.  网络适配器停止数据的 DMA 传输以接收与接收队列关联的缓冲区，在此之后，队列必须进入 DMA 停止状态。 网络适配器在收到 [oid \_ 接收筛选器 " \_ \_ 清除 \_ 筛选器](oid-receive-filter-clear-filter.md) oid 请求" 时可能会停止 DMA 活动，以清除接收队列中的最后一个 set 筛选器。

2.  微型端口驱动程序使用 [**ndis \_ 接收 \_ 队列 \_ 状态**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_receive_queue_state)结构设置为 " **NdisReceiveQueueOperationalStateDmaStopped** " 的 **QueueState** 成员生成 [**NDIS \_ 状态 \_ 接收 \_ 队列 \_ 状态**](./ndis-status-receive-queue-state.md)状态指示，以通知 NDIS 已停止 DMA 传输。

3.  微型端口驱动程序等待该队列的所有指示接收数据包返回到微型端口驱动程序。

4.  通过调用 [**NdisFreeSharedMemory**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreesharedmemory)，微型端口驱动程序可释放它为网络适配器的接收缓冲区分配的、与队列关联的所有共享内存。

5.  微型端口驱动程序完成 OID \_ 接收 \_ 筛选器 \_ 免费 \_ 队列 OID 请求，以释放接收队列。

微型端口驱动程序调用 [**NdisFreeSharedMemory**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreesharedmemory) 函数来释放队列的共享内存。 如果微型端口驱动程序为非默认队列分配了共享内存，驱动程序将在 \_ \_ \_ 释放队列时在 oid 接收筛选器的上下文中释放共享内存 \_ 。 微型端口驱动程序在 [*MiniportHaltEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt) 函数的上下文中为默认队列分配的共享内存可用。

当过量驱动程序释放队列之前，必须释放它在队列上设置的所有筛选器。 此外，在调用 [**NdisCloseAdapterEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscloseadapterex) 函数以关闭到网络适配器的绑定之前，过量驱动程序必须释放在网络适配器上分配的所有接收队列。 NDIS 在调用微型端口驱动程序的 [*MiniportHaltEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt) 函数之前，释放在网络适配器上分配的所有队列。

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
<td><p>正在重置微型端口驱动程序。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_REQUEST_ABORTED</strong></p></td>
<td><p>微型端口驱动程序已停止处理请求。 例如，NDIS 称为 <a href="/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset" data-raw-source="[&lt;em&gt;MiniportResetEx&lt;/em&gt;](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset)"><em>MiniportResetEx</em></a> 函数。</p></td>
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
<th>说明</th>
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
<td><p>信息缓冲区太短。 NDIS 设置<strong>数据</strong>。<strong>METHOD_INFORMATION</strong>。将<a href="/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>结构中的成员<strong>BytesNeeded</strong>为所需的最小缓冲区大小。</p></td>
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
<td><p>Version</p></td>
<td><p>在 NDIS 6.20 和更高版本中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标题</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[*MiniportHaltEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)

[**NDIS \_ 接收 \_ 队列 \_ 可用 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_free_parameters)

[**NDIS \_ 状态 \_ 接收 \_ 队列 \_ 状态**](./ndis-status-receive-queue-state.md)

[**NdisCloseAdapterEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscloseadapterex)

[**NdisFreeSharedMemory**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreesharedmemory)

[OID \_ 接收 \_ 筛选器 \_ 分配 \_ 队列](oid-receive-filter-allocate-queue.md)


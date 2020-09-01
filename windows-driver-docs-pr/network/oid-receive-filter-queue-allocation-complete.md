---
title: OID_RECEIVE_FILTER_QUEUE_ALLOCATION_COMPLETE
description: NDIS 协议驱动程序发出对象标识符 (OID) 方法请求 OID_RECEIVE_FILTER_QUEUE_ALLOCATION_COMPLETE，以通知微型端口驱动程序已为当前的接收队列分配完成分配。
ms.assetid: d09fcab5-4c3b-432a-ba9e-fd4269537de6
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_RECEIVE_FILTER_QUEUE_ALLOCATION_COMPLETE 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b01a44c1e5036f2300d16993c3c67dabe3d3b339
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217004"
---
# <a name="oid_receive_filter_queue_allocation_complete"></a>OID \_ 接收 \_ 筛选器 \_ 队列 \_ 分配 \_ 完成


NDIS 协议驱动程序发出对象标识符 (oid) 方法请求 OID \_ 接收 \_ 筛选器 \_ 队列 \_ 分配 \_ 完成，通知微型端口驱动程序已为当前的接收队列分配完成分配。

[**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**ndis \_ 接收 \_ 队列 \_ 分配 \_ 完成 \_ 数组**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_allocation_complete_array)结构的指针，该结构后跟每个队列的[**ndis \_ 接收 \_ 队列 \_ 分配 \_ 完成 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_allocation_complete_parameters)结构。 成功从 OID 方法请求返回后， **NDIS \_ OID \_ 请求**结构的**InformationBuffer**成员包含指向相同结构数组的指针，每个**NDIS \_ 接收 \_ 队列 \_ 分配 \_ 完成 \_ 参数**结构的**CompletionStatus**成员都包含每个队列的完成状态。

<a name="remarks"></a>备注
-------

\_ \_ \_ \_ \_ 对于 NDIS 6.20 和更高的微型端口驱动程序，oid 接收筛选器队列分配完成的 oid 方法请求是可选的。 对于支持虚拟机队列 (VMQ) 接口的微型端口驱动程序是必需的。

分配一个或多个接收队列并选择性地设置初始筛选器后，协议驱动程序必须发出 OID \_ 接收 \_ 筛选器队列分配完成的 oid 方法请求， \_ \_ \_ 以便通知微型端口驱动程序已为当前的接收队列分配完成分配。 这允许微型端口驱动程序在多个接收队列之间平衡硬件资源;如有必要，它可以为接收队列分配资源，如共享内存。

当微型端口驱动程序收到 OID \_ 接收 \_ 筛选器 \_ 队列 \_ 分配 \_ 完成请求并且它具有在队列中设置的筛选器后，该队列将处于 "正在运行" 状态。 在此状态下，微型端口驱动程序可以通过调用 [**NdisMIndicateReceiveNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)在队列中启动数据包的指示。

### <a name="return-status-codes"></a>返回状态代码

对于 oid \_ 接收 \_ 筛选器 \_ 队列 \_ 分配 \_ 完成的 oid 方法请求，微型端口驱动程序返回以下状态代码之一。

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
<td><p>队列分配已完成。 信息缓冲区包含更新后的 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_allocation_complete_array" data-raw-source="[&lt;strong&gt;NDIS_RECEIVE_QUEUE_ALLOCATION_COMPLETE_ARRAY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_allocation_complete_array)"><strong>NDIS_RECEIVE_QUEUE_ALLOCATION_COMPLETE_ARRAY</strong></a> 结构和参数结构，其完成状态为队列分配。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_PENDING</strong></p></td>
<td><p>请求正在等待完成。 最终状态代码和结果将传递给调用方的 OID 请求完成处理程序。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_INVALID_PARAMETER</strong></p></td>
<td><p>提供的过量驱动程序的一个或多个参数无效。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_INVALID_LENGTH</strong></p></td>
<td><p>信息缓冲区太短。 NDIS 设置<strong>数据</strong>。<strong>METHOD_INFORMATION</strong>。将<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>结构中的成员<strong>BytesNeeded</strong>为所需的最小缓冲区大小。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_NOT_SUPPORTED</strong></p></td>
<td><p>此微型端口驱动程序的 NDIS 版本早于版本6.20。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_FAILURE</strong></p></td>
<td><p>由于其他原因，请求失败。</p></td>
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
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NdisMIndicateReceiveNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS \_ 接收 \_ 队列 \_ 分配 \_ 完成 \_ 数组**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_allocation_complete_array)

[**NDIS \_ 接收 \_ 队列 \_ 分配 \_ 完成 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_allocation_complete_parameters)

 


---
title: OID_RECEIVE_FILTER_QUEUE_ALLOCATION_COMPLETE
description: NDIS 协议驱动程序发出 OID_RECEIVE_FILTER_QUEUE_ALLOCATION_COMPLETE 的对象标识符（OID）方法请求，通知微型端口驱动程序已为当前的接收队列分配完成分配。
ms.assetid: d09fcab5-4c3b-432a-ba9e-fd4269537de6
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_RECEIVE_FILTER_QUEUE_ALLOCATION_COMPLETE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 397f802e24f844bc2a45049acb91deed9fc3d3e6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844000"
---
# <a name="oid_receive_filter_queue_allocation_complete"></a>OID\_接收\_筛选器\_队列\_分配\_完成


NDIS 协议驱动程序发出 OID\_接收\_FILTER\_队列的对象标识符（OID）方法请求，\_分配\_完成，通知微型端口驱动程序已为当前的接收批分配完成了分配队列.

[**Ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS\_接收\_队列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_allocation_complete_array)的指针\_\_\_后跟[**NDIS\_接收\_队列\_分配\_完成**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_allocation_complete_parameters)每个队列的\_参数结构。 成功从 OID 方法请求返回后， **NDIS\_OID\_请求**结构的**InformationBuffer**成员包含指向同一结构数组的指针，以及每个的**CompletionStatus**成员**NDIS\_接收\_队列\_分配\_完成\_参数**结构包含每个队列的完成状态。

<a name="remarks"></a>备注
-------

Oid\_接收\_筛选器的 OID 方法请求\_队列\_分配\_完成对于 NDIS 6.20 和更高的微型端口驱动程序是可选的。 这对于支持虚拟机队列（VMQ）接口的微型端口驱动程序是必需的。

分配一个或多个接收队列并选择性地设置初始筛选器后，协议驱动程序必须发出 OID\_接收\_筛选\_器的 OID 方法请求，\_分配\_完成，以便通知小型端口驱动程序，为当前批次接收队列分配已完成。 这允许微型端口驱动程序在多个接收队列之间平衡硬件资源;如有必要，它可以为接收队列分配资源，如共享内存。

在微型端口驱动程序接收 OID 后\_接收\_筛选器\_队列\_分配\_完成请求，并包含在队列中设置的筛选器，队列处于 "正在运行" 状态。 在此状态下，微型端口驱动程序可以通过调用[**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)在队列中启动数据包的指示。

### <a name="return-status-codes"></a>返回状态代码

对于 oid\_接收\_筛选\_器的 OID 方法请求，微型端口驱动程序返回以下状态代码之一，\_分配\_完成。

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
<td><p>队列分配已完成。 信息缓冲区包含更新后的<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_allocation_complete_array" data-raw-source="[&lt;strong&gt;NDIS_RECEIVE_QUEUE_ALLOCATION_COMPLETE_ARRAY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_allocation_complete_array)"><strong>NDIS_RECEIVE_QUEUE_ALLOCATION_COMPLETE_ARRAY</strong></a>结构和参数结构，其完成状态为队列分配。</p></td>
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
<td><p>信息缓冲区太短。 NDIS 设置<strong>数据</strong>。<strong>METHOD_INFORMATION</strong>。<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>结构中的<strong>BytesNeeded</strong>成员到所需的最小缓冲区大小。</p></td>
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
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)

[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_接收\_队列\_分配\_完成\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_allocation_complete_array)

[**NDIS\_接收\_队列\_分配\_完成\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_allocation_complete_parameters)

 

 





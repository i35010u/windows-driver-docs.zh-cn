---
title: OID_RECEIVE_FILTER_ALLOCATE_QUEUE
description: 过量驱动程序发出对象标识符 (OID) 方法请求 OID_RECEIVE_FILTER_ALLOCATE_QUEUE 分配具有一组初始配置参数的队列。
ms.assetid: 8dd7ab91-b752-46fd-ae1b-014dc0fb0157
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_RECEIVE_FILTER_ALLOCATE_QUEUE 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 211840385dbd3a70da6fa745256220becdfc482e
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89214593"
---
# <a name="oid_receive_filter_allocate_queue"></a>OID \_ 接收 \_ 筛选器 \_ 分配 \_ 队列


过量驱动程序发出对象标识符 (oid) 方法请求 OID \_ 接收 \_ 筛选器 \_ 分配 \_ 队列，以分配具有一组初始配置参数的队列。

[**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS \_ 接收 \_ 队列 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)结构的指针。 成功从 OID 方法请求返回后， **ndis \_ OID \_ 请求**结构的**InformationBuffer**成员包含一个指向**NDIS \_ 接收 \_ 队列 \_ 参数**结构的指针，该结构具有新的队列标识符。

<a name="remarks"></a>备注
-------

\_ \_ \_ \_ 对于 NDIS 6.20 和更高的微型端口驱动程序，oid 接收筛选器分配队列的 oid 方法请求是可选的。 对于支持虚拟机队列 (VMQ) 接口的微型端口驱动程序是必需的。

过量驱动程序将 [**NDIS \_ 接收 \_ 队列 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters) 结构与请求的队列配置进行初始化。 NDIS 在**ndis \_ 接收 \_ 队列 \_ 参数**结构的**QueueId**成员中分配一个队列标识符，并将该方法请求传递给微型端口驱动程序。

**注意**   过量驱动程序可以在[**ndis 接收 \_ \_ 队列 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)结构的**flags**成员中设置** \_ \_ \_ \_ 每个 \_ 队列 \_ 接收 \_ 指示**和**ndis \_ 接收 \_ 队列 \_ \_ \_ \_ **参数的 ndis 接收队列参数。 其他标志不用于队列分配。

 

颁发微型端口驱动程序后，OID 接收筛选器的 OID 请求会 \_ \_ \_ 分配 \_ 队列并成功处理它，队列处于暂停状态。

过量驱动程序必须使用 NDIS 在后续 OID 请求中提供的队列标识符，例如，修改队列参数或释放队列。 队列标识符也包含在带外 (OOB) 与队列关联的所有 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构上的数据。 驱动程序使用 [**网络 \_ 缓冲区 \_ 列表 \_ 接收 \_ 队列 \_ ID**](/windows-hardware/drivers/ddi/ndis/nf-ndis-net_buffer_list_receive_queue_id) 宏来检索 **网络 \_ 缓冲区 \_ 列表** 结构中的队列标识符。

当 NDIS 接收到分配接收队列的 OID 请求时，它将验证队列参数。 在 NDIS 分配所需的资源和队列标识符后，它会将 OID 请求提交到基础微型端口驱动程序。 队列标识符对于关联的网络适配器是唯一的。

如果微型端口驱动程序可以成功分配接收队列所需的软件和硬件资源，则会通过返回 **NDIS \_ 状态 " \_ 成功**" 来完成 OID 请求。

微型端口驱动程序必须保留已分配接收队列的队列标识符。 对于对微型端口驱动程序的后续调用，NDIS 使用接收队列的队列标识符，以便在接收队列上设置接收筛选器、更改接收队列参数或释放接收队列。

当过量驱动程序分配一个或多个接收队列，并选择性地设置初始筛选器后，它必须发出 [oid \_ 接收 \_ 筛选器 \_ 队列 \_ 分配 \_ 完成](oid-receive-filter-queue-allocation-complete.md) 设置 oid 请求，通知微型端口驱动程序已为当前批接收队列分配完成。

如果没有对该队列设置任何筛选器，则微型端口驱动程序不得保留接收队列中的任何数据包。 如果队列中的任何筛选器均未设置或清除了所有筛选器，则队列应为空，并且应丢弃所有数据包。 也就是说，数据包不会指明驱动程序堆栈或保留在队列中。

过量驱动程序使用 [oid \_ 接收筛选器的 oid 请求 \_ \_ 可用 \_ 队列](oid-receive-filter-free-queue.md) 来释放它们分配的队列。

### <a name="return-status-codes"></a>返回状态代码

对于 OID \_ 接收 \_ 筛选器 \_ 分配队列，NDIS 或微型端口驱动程序返回以下状态代码之一 \_ 。

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
<td><p>已成功分配队列。 信息缓冲区包含更新的 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters" data-raw-source="[&lt;strong&gt;NDIS_RECEIVE_QUEUE_PARAMETERS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)"><strong>NDIS_RECEIVE_QUEUE_PARAMETERS</strong></a> 结构。</p></td>
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


[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)

[**网络 \_ 缓冲区 \_ 列表 \_ 接收 \_ 队列 \_ ID**](/windows-hardware/drivers/ddi/ndis/nf-ndis-net_buffer_list_receive_queue_id)

[OID \_ 接收 \_ 筛选器 \_ 可用 \_ 队列](oid-receive-filter-free-queue.md)

[OID \_ 接收 \_ 筛选器 \_ 队列 \_ 分配 \_ 完成](oid-receive-filter-queue-allocation-complete.md)

[**NDIS \_ 接收 \_ 队列 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)

 


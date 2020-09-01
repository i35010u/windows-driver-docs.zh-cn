---
title: OID_RECEIVE_FILTER_QUEUE_PARAMETERS
description: 过量驱动程序发出对象标识符 (OID) 方法请求 OID_RECEIVE_FILTER_QUEUE_PARAMETERS 获取接收队列的当前配置参数。
ms.assetid: f6cd7896-0811-4029-b1d8-8cf800d7813e
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_RECEIVE_FILTER_QUEUE_PARAMETERS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a181806c55bd08c12f98dfbe29312f05e479a316
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206035"
---
# <a name="oid_receive_filter_queue_parameters"></a>OID \_ 接收 \_ 筛选器 \_ 队列 \_ 参数


过量驱动程序发出对象标识符 (oid) 方法请求 OID \_ 接收 \_ 筛选器 \_ 队列 \_ 参数，以获取接收队列的当前配置参数。 [**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**ndis \_ 接收 \_ 队列 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)结构的指针，该结构具有类型为**ndis \_ 接收 \_ 队列 \_ ID**的队列标识符。 成功从 OID 方法请求返回后， **ndis \_ OID \_ 请求**结构的**InformationBuffer**成员包含指向**NDIS \_ 接收 \_ 队列 \_ 参数**结构的指针。

过量驱动程序发出 oid 设置 OID \_ 接收 \_ 筛选器 \_ 队列参数的请求 \_ ，以更改队列的当前配置参数。 过量驱动程序在[**ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员中提供了指向[**ndis \_ 接收 \_ 队列 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)结构的指针。

<a name="remarks"></a>备注
-------

过量驱动程序发出 oid 设置 OID \_ 接收 \_ 筛选器 \_ 队列参数的请求 \_ ，以更改一个或多个接收队列的参数。 对于 NDIS 6.20 和更高的微型端口驱动程序，OID set 请求是可选的。 但是，OID 请求对于支持虚拟机队列 (VMQ) 接口的微型端口驱动程序是必需的。

**注意**   只有分配了队列的过量驱动程序才可以通过发出 oid 设置 OID \_ 接收 \_ 筛选器 \_ 队列参数的请求来更改配置参数 \_ 。

 

过量驱动程序从较早的 [OID \_ 接收 \_ 筛选器 \_ 分配 \_ 队列](oid-receive-filter-allocate-queue.md) 方法 OID 请求中获取队列标识符输入值。

在过量的驱动程序分配队列后，它可以更改具有相应更改标志的配置参数， (ndis 接收队列参数 \_ \_ 结构的 \_ \_ *Xxx* \_ **Flags**成员中) [** \_ \_ \_ **](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)更改了 ndis 接收队列参数 Xxx。 但是，在分配队列后，过量驱动程序无法更改没有相应更改标志的配置参数。

### <a name="return-status-codes"></a>返回状态代码

NDIS 处理 \_ \_ 微型端口驱动程序的 oid 接收筛选器队列参数的 oid 方法请求 \_ \_ ，并返回以下状态代码之一。

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
<td><p>请求已成功完成。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_PENDING</strong></p></td>
<td><p>请求正在等待完成。 请求完成后，NDIS 会将最终状态代码和结果传递给调用方的 OID 请求完成处理程序。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_INVALID_LENGTH</strong></p></td>
<td><p>信息缓冲区太短。 NDIS 设置 <strong>数据</strong>。<strong>METHOD_INFORMATION</strong>。将 NDIS_OID_REQUEST 结构中的成员<strong>BytesNeeded</strong> 为所需的最小缓冲区大小。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_INVALID_PARAMETER</strong></p></td>
<td><p>请求失败，因为它尝试启用基础网络适配器不支持的功能。</p></td>
</tr>
<tr class="odd">
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

[**NDIS \_ 接收 \_ 队列 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)

[OID \_ 接收 \_ 筛选器 \_ 分配 \_ 队列](oid-receive-filter-allocate-queue.md)

[OID \_ 接收 \_ 筛选器 \_ 队列 \_ 参数](oid-receive-filter-queue-parameters.md)

 


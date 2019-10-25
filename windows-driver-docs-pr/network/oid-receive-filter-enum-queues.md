---
title: OID_RECEIVE_FILTER_ENUM_QUEUES
description: 过量驱动程序和用户模式应用程序发出 OID_RECEIVE_FILTER_ENUM_QUEUES 的对象标识符（OID）查询请求，以获取在网络适配器上分配的所有接收队列的列表。
ms.assetid: e8a946a2-9ee9-42a0-8175-fbc592d404d1
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_RECEIVE_FILTER_ENUM_QUEUES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 08ea9859a59bb72af6a06eab9a732d32b8c55d67
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844014"
---
# <a name="oid_receive_filter_enum_queues"></a>OID\_接收\_筛选器\_枚举\_队列


过量驱动程序和用户模式应用程序发出 OID\_接收\_筛选\_\_器的对象标识符（OID）查询请求，以获取在网络适配器上分配的所有接收队列的列表。

成功从 OID 查询请求返回后， [**ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构中的**InformationBuffer**成员包含指向[**ndis\_接收\_队列的指针\_\_的数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_info_array)结构，后跟 NDIS\_接收每个筛选器的[ **\_队列\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_info)结构。

<a name="remarks"></a>备注
-------

NDIS 从 OID 收到的数据的内部缓存获取信息[\_接收\_筛选器\_分配\_队列](oid-receive-filter-allocate-queue.md)和 OID\_\_\_\_的[参数](oid-receive-filter-queue-parameters.md)OID 请求。

过量驱动程序和用户模式应用程序发出 oid\_接收\_筛选器的 oid 查询请求\_枚举\_队列，以枚举网络适配器上的接收队列。

如果协议驱动程序发出请求， [**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构内的请求类型设置为**NdisRequestQueryInformation** ，并且此 OID 返回协议驱动程序分配的所有接收队列的数组在网络适配器上。 如果用户模式应用程序发出了请求， **NDIS\_OID\_请求**结构内的请求类型设置为**NdisRequestQueryStatistics**，并且此 OID 返回所有接收队列在网络适配器。

### <a name="return-status-codes"></a>返回状态代码

NDIS 处理 OID\_接收\_筛选器的 OID 查询请求\_小型端口驱动程序的枚举\_队列，并返回以下状态代码之一。

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
<td><p>请求已成功完成。 <strong>InformationBuffer</strong>指向<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_info_array" data-raw-source="[&lt;strong&gt;NDIS_RECEIVE_QUEUE_INFO_ARRAY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_info_array)"><strong>NDIS_RECEIVE_QUEUE_INFO_ARRAY</strong></a>结构。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_PENDING</strong></p></td>
<td><p>请求正在等待完成。 请求完成后，NDIS 会将最终状态代码和结果传递给调用方的 OID 请求完成处理程序。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_INVALID_LENGTH</strong></p></td>
<td><p>信息缓冲区太短。 NDIS 设置<strong>数据</strong>。<strong>METHOD_INFORMATION</strong>。<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>结构中的<strong>BytesNeeded</strong>成员到所需的最小缓冲区大小。</p></td>
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


[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_接收\_队列\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_info)

[**NDIS\_接收\_队列\_信息\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_info_array)

[OID\_接收\_筛选器\_分配\_队列](oid-receive-filter-allocate-queue.md)

[OID\_接收\_筛选器\_队列\_参数](oid-receive-filter-queue-parameters.md)

 

 





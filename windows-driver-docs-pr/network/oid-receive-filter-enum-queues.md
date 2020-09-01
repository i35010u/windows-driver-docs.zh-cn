---
title: OID_RECEIVE_FILTER_ENUM_QUEUES
description: 过量驱动程序和用户模式应用程序)  (OID 发出对象标识符，OID_RECEIVE_FILTER_ENUM_QUEUES 获取在网络适配器上分配的所有接收队列的列表。
ms.assetid: e8a946a2-9ee9-42a0-8175-fbc592d404d1
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_RECEIVE_FILTER_ENUM_QUEUES 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 60a7202be6904cbe556fb3025710b77bb5fbfd4b
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89214571"
---
# <a name="oid_receive_filter_enum_queues"></a>OID \_ 接收 \_ 筛选器 \_ 枚举 \_ 队列


过量驱动程序和用户模式应用程序) OID 接收筛选器枚举队列的查询请求中发出对象标识符 (OID， \_ \_ \_ \_ 以获取在网络适配器上分配的所有接收队列的列表。

成功从 OID 查询请求返回后， [**ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**ndis \_ 接收 \_ 队列 \_ 信息 \_ 数组**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_info_array)结构的指针，该结构后跟每个筛选器的[**ndis \_ 接收 \_ 队列 \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_info)结构。

<a name="remarks"></a>备注
-------

NDIS 从 [oid \_ 接收 \_ 筛选器 \_ 分配 \_ 队列](oid-receive-filter-allocate-queue.md) 和 [oid \_ 接收 \_ 筛选器 \_ 队列 \_ 参数](oid-receive-filter-queue-parameters.md) oid 请求中收到的数据的内部缓存获取信息。

过量驱动程序和用户模式应用程序发出 oid 查询请求，即 OID \_ 接收 \_ 筛选器 \_ 枚举 \_ 队列，以枚举网络适配器上的接收队列。

如果协议驱动程序发出请求，则将 [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request) 结构内的请求类型设置为 **NdisRequestQueryInformation** ，并且此 OID 返回在网络适配器上分配协议驱动程序的所有接收队列的数组。 如果用户模式应用程序发出了请求，则将 **NDIS \_ OID \_ 请求** 结构内的请求类型设置为 **NdisRequestQueryStatistics**，并且此 OID 返回网络适配器上所有接收队列的信息的数组。

### <a name="return-status-codes"></a>返回状态代码

NDIS 处理 \_ \_ 微型端口驱动程序的 oid 接收筛选器枚举队列的 oid 查询请求 \_ \_ ，并返回以下状态代码之一。

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
<td><p>请求已成功完成。 <strong>InformationBuffer</strong>指向<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_info_array" data-raw-source="[&lt;strong&gt;NDIS_RECEIVE_QUEUE_INFO_ARRAY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_info_array)"><strong>NDIS_RECEIVE_QUEUE_INFO_ARRAY</strong></a>结构。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_PENDING</strong></p></td>
<td><p>请求正在等待完成。 请求完成后，NDIS 会将最终状态代码和结果传递给调用方的 OID 请求完成处理程序。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_INVALID_LENGTH</strong></p></td>
<td><p>信息缓冲区太短。 NDIS 设置<strong>数据</strong>。<strong>METHOD_INFORMATION</strong>。将<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>结构中的成员<strong>BytesNeeded</strong>为所需的最小缓冲区大小。</p></td>
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

[**NDIS \_ 接收 \_ 队列 \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_info)

[**NDIS \_ 接收 \_ 队列 \_ 信息 \_ 数组**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_info_array)

[OID \_ 接收 \_ 筛选器 \_ 分配 \_ 队列](oid-receive-filter-allocate-queue.md)

[OID \_ 接收 \_ 筛选器 \_ 队列 \_ 参数](oid-receive-filter-queue-parameters.md)

 


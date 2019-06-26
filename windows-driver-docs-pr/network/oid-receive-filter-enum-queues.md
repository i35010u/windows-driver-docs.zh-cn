---
title: OID_RECEIVE_FILTER_ENUM_QUEUES
description: 基础驱动程序和用户模式应用程序发出对象标识符 (OID) 查询请求的 OID_RECEIVE_FILTER_ENUM_QUEUES 来获取网络适配器分配的所有接收队列的列表。
ms.assetid: e8a946a2-9ee9-42a0-8175-fbc592d404d1
ms.date: 08/08/2017
keywords: -OID_RECEIVE_FILTER_ENUM_QUEUES 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 4a81201dee22a03547a823eeef2173cd8a0deaf5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371201"
---
# <a name="oidreceivefilterenumqueues"></a>OID\_RECEIVE\_FILTER\_ENUM\_QUEUES


基础驱动程序和用户模式应用程序发出对象标识符 (OID) 查询请求的 OID\_接收\_筛选器\_枚举\_队列以获取在网络分配的所有接收队列的列表适配器。

从 OID 查询请求，成功返回后**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含一个指向[ **NDIS\_接收\_队列\_信息\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_queue_info_array)结构，后跟[**NDIS\_接收\_队列\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_queue_info)每个筛选器的结构。

<a name="remarks"></a>备注
-------

NDIS 从它来自数据的内部缓存中获取信息[OID\_接收\_筛选器\_分配\_队列](oid-receive-filter-allocate-queue.md)和[OID\_接收\_筛选器\_队列\_参数](oid-receive-filter-queue-parameters.md)OID 请求。

基础驱动程序和用户模式应用程序颁发的 OID 的 OID 查询请求\_接收\_筛选器\_枚举\_队列以枚举网络适配器上的接收队列。

如果协议驱动程序发出请求，请求类型内[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构设置为**NdisRequestQueryInformation**和此 OID 上的网络适配器返回的所有接收队列协议驱动程序分配的数组。 如果在用户模式应用程序发出的请求，请求键入内**NDIS\_OID\_请求**结构设置为**NdisRequestQueryStatistics**，并返回此 OID网络适配器上接收的所有队列的信息的数组。

### <a name="return-status-codes"></a>返回状态代码

NDIS 处理 OID 查询请求的 OID\_接收\_筛选器\_枚举\_队列用于微型端口驱动程序，并返回一个的以下状态代码。

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
<td><p>请求已成功完成。 <strong>InformationBuffer</strong>指向<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_queue_info_array" data-raw-source="[&lt;strong&gt;NDIS_RECEIVE_QUEUE_INFO_ARRAY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_queue_info_array)"> <strong>NDIS_RECEIVE_QUEUE_INFO_ARRAY</strong> </a>结构。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_PENDING</strong></p></td>
<td><p>请求正在等待完成。 NDIS 将传递的最终状态代码和结果到 OID 请求完成处理程序的调用方完成请求后。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_INVALID_LENGTH</strong></p></td>
<td><p>信息缓冲区太短。 NDIS 集<strong>数据</strong>。<strong>METHOD_INFORMATION</strong>。<strong>BytesNeeded</strong>中的成员<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)"> <strong>NDIS_OID_REQUEST</strong> </a>是必需的最小缓冲区大小的结构。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_FAILURE</strong></p></td>
<td><p>请求由于其他原因而失败。</p></td>
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
<td><p>支持 NDIS 6.20 及更高版本。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_OID\_REQUEST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_接收\_队列\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_queue_info)

[**NDIS\_接收\_队列\_信息\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_queue_info_array)

[OID\_RECEIVE\_FILTER\_ALLOCATE\_QUEUE](oid-receive-filter-allocate-queue.md)

[OID\_RECEIVE\_FILTER\_QUEUE\_PARAMETERS](oid-receive-filter-queue-parameters.md)

 

 





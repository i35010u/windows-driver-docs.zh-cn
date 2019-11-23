---
title: OID_RECEIVE_FILTER_QUEUE_PARAMETERS
description: 过量驱动程序发出 OID_RECEIVE_FILTER_QUEUE_PARAMETERS 的对象标识符（OID）方法请求，以获取接收队列的当前配置参数。
ms.assetid: f6cd7896-0811-4029-b1d8-8cf800d7813e
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_RECEIVE_FILTER_QUEUE_PARAMETERS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: e291b519fe6248f65238f320b75479b77717ac64
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843998"
---
# <a name="oid_receive_filter_queue_parameters"></a>OID\_接收\_筛选器\_队列\_参数


过量驱动程序发出 OID\_接收\_FILTER\_QUEUE\_参数的对象标识符（OID）方法请求，以获取接收队列的当前配置参数。 [ **\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含一个指向[**ndis\_接收\_队列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)的指针，该指针具有类型为**ndis\_接收\_queue\_ID**的队列标识符。\_ 成功从 OID 方法请求返回后， **ndis\_OID\_请求**结构的**InformationBuffer**成员包含指向**ndis\_接收\_队列\_参数**结构的指针。

过量驱动程序发出 oid\_接收\_FILTER\_\_队列的请求，以便更改队列的当前配置参数。 过量驱动程序提供了一个指向 Ndis\_的指针，该指针在[**ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**INFORMATIONBUFFER**成员中[**接收\_QUEUE\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)结构。

<a name="remarks"></a>备注
-------

过量驱动程序发出 oid\_接收\_FILTER\_\_队列的请求，以更改一个或多个接收队列的参数。 对于 NDIS 6.20 和更高的微型端口驱动程序，OID set 请求是可选的。 但是，OID 请求是支持虚拟机队列（VMQ）接口的微型端口驱动程序所必需的。

**请注意**  仅分配了队列的过量驱动程序可以通过发出 OID 的 oid 集请求来更改配置参数\_接收\_筛选器\_队列\_参数。

 

过量驱动程序从较早的 OID 获取队列标识符输入值， [\_接收\_FILTER\_分配\_队列](oid-receive-filter-allocate-queue.md)方法 OID 请求。

在过量的驱动程序分配队列后，它可以在[**NDIS\_接收\_queue\_parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)结构的**Flags**成员中更改具有相应更改标志（NDIS\_接收\_队列\_参数\_*Xxx*\_的配置参数）。 但是，在分配队列后，过量驱动程序无法更改没有相应更改标志的配置参数。

### <a name="return-status-codes"></a>返回状态代码

NDIS 处理 OID\_接收\_筛选器的 OID 方法请求\_微型端口驱动程序的队列\_参数，并返回以下状态代码之一。

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
<td><p>请求已成功完成。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_PENDING</strong></p></td>
<td><p>请求正在等待完成。 请求完成后，NDIS 会将最终状态代码和结果传递给调用方的 OID 请求完成处理程序。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_INVALID_LENGTH</strong></p></td>
<td><p>信息缓冲区太短。 NDIS 设置<strong>数据</strong>。<strong>METHOD_INFORMATION</strong>。将 NDIS_OID_REQUEST 结构中的成员<strong>BytesNeeded</strong>为所需的最小缓冲区大小。</p></td>
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
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_接收\_队列\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)

[OID\_接收\_筛选器\_分配\_队列](oid-receive-filter-allocate-queue.md)

[OID\_接收\_筛选器\_队列\_参数](oid-receive-filter-queue-parameters.md)

 

 





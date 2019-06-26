---
title: OID_RECEIVE_FILTER_QUEUE_PARAMETERS
description: 基础驱动程序发出对象标识符 (OID) 方法请求的 OID_RECEIVE_FILTER_QUEUE_PARAMETERS 获取接收队列的当前配置参数。
ms.assetid: f6cd7896-0811-4029-b1d8-8cf800d7813e
ms.date: 08/08/2017
keywords: -OID_RECEIVE_FILTER_QUEUE_PARAMETERS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d6b76956a9a159f14834695654672507cd208aab
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376763"
---
# <a name="oidreceivefilterqueueparameters"></a>OID\_RECEIVE\_FILTER\_QUEUE\_PARAMETERS


基础驱动程序发出对象标识符 (OID) 方法请求的 OID\_接收\_筛选器\_队列\_参数来获取接收队列的当前配置参数。 **InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含一个指向[ **NDIS\_接收\_队列\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)结构类型的队列标识符**NDIS\_接收\_队列\_ID**。 通过 OID 方法请求成功返回后**InformationBuffer**的成员**NDIS\_OID\_请求**结构包含一个指向**NDIS\_接收\_队列\_参数**结构。

过量驱动程序问题 OID 设置请求的 OID\_接收\_筛选器\_队列\_参数来更改队列的当前配置参数。 基础驱动程序提供一个指针指向[ **NDIS\_接收\_队列\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)结构**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构。

<a name="remarks"></a>备注
-------

过量驱动程序问题 OID 设置请求的 OID\_接收\_筛选器\_队列\_参数来更改一个或多个参数接收队列。 OID 集请求是可选的 NDIS 6.20 和更高版本的微型端口驱动程序。 但是，OID 请求是必需的支持的虚拟机队列 (VMQ) 接口的微型端口驱动程序。

**请注意**  OID 仅分配队列的基础驱动程序可以通过发出更改的配置参数设置请求的 OID\_接收\_筛选器\_队列\_参数.

 

基础驱动程序获取队列标识符输入的值从早期[OID\_接收\_筛选器\_分配\_队列](oid-receive-filter-allocate-queue.md)方法 OID 请求。

基础驱动程序分配一个队列后，它可以更改已设置相应更改标志的配置参数 (NDIS\_接收\_队列\_参数\_*Xxx*\_已更改) 中**标志**的成员[ **NDIS\_接收\_队列\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)结构。 但是，已分配队列后，基础驱动程序不能更改不具有相应更改标志的配置参数。

### <a name="return-status-codes"></a>返回状态代码

NDIS 处理 OID 方法请求的 OID\_接收\_筛选器\_队列\_微型端口驱动程序，并返回一个的以下状态代码的参数。

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
<td><p>请求正在等待完成。 NDIS 将传递的最终状态代码和结果到 OID 请求完成处理程序的调用方完成请求后。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_INVALID_LENGTH</strong></p></td>
<td><p>信息缓冲区太短。 NDIS 集<strong>数据</strong>。<strong>METHOD_INFORMATION</strong>。<strong>BytesNeeded</strong>是必需的最小缓冲区大小的 NDIS_OID_REQUEST 结构中的成员。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_INVALID_PARAMETER</strong></p></td>
<td><p>请求失败，因为它尝试启用的基础网络适配器不支持的功能。</p></td>
</tr>
<tr class="odd">
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

[**NDIS\_RECEIVE\_QUEUE\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)

[OID\_RECEIVE\_FILTER\_ALLOCATE\_QUEUE](oid-receive-filter-allocate-queue.md)

[OID\_RECEIVE\_FILTER\_QUEUE\_PARAMETERS](oid-receive-filter-queue-parameters.md)

 

 





---
title: OID_RECEIVE_FILTER_FREE_QUEUE
description: 协议的 NDIS 驱动程序发出对象标识符 (OID) 组的请求的 OID_RECEIVE_FILTER_FREE_QUEUE 免费接收队列。
ms.assetid: ee8cff69-2f5e-4798-9c18-28e996dd1dd4
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_RECEIVE_FILTER_FREE_QUEUE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 17482b9a41a0960addebfc8784e116fb0bb5b4e9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359151"
---
# <a name="oidreceivefilterfreequeue"></a>OID\_RECEIVE\_FILTER\_FREE\_QUEUE


协议的 NDIS 驱动程序发出的 OID 的对象标识符 (OID) 组请求\_接收\_筛选器\_免费\_队列以释放接收队列。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向[ **NDIS\_接收\_队列\_免费\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567201)结构类型的队列标识符**NDIS\_接收\_队列\_ID**。

<a name="remarks"></a>备注
-------

OID 设置请求的 OID\_接收\_筛选器\_免费\_队列是可选的 NDIS 6.20 和更高版本的微型端口驱动程序。 它是必需的支持的虚拟机队列接口的微型端口驱动程序。

过量的驱动程序问题后[OID\_接收\_筛选器\_分配\_队列](oid-receive-filter-allocate-queue.md)OID 分配接收队列中，它会发出 OID\_接收\_筛选器\_免费\_队列 OID 来释放接收队列。

NDIS 请求微型端口驱动程序以释放 VMQ 时接收队列，则会遵循以下步骤：

1.  网络适配器停止 DMA 将数据传输到接收队列，队列必须在其后输入 DMA 停止状态与相关联的接收缓冲区。 网络适配器可能停止 DMA 活动，当它收到[OID\_接收\_筛选器\_清除\_筛选器](oid-receive-filter-clear-filter.md)OID 请求清除上接收的最后一组筛选器队列。

2.  微型端口驱动程序将生成[ **NDIS\_状态\_接收\_队列\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff567417)与状态指示**QueueState**的成员[ **NDIS\_接收\_队列\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff567214)结构设置为**NdisReceiveQueueOperationalStateDmaStopped**通知 NDIS DMA 传输已停止。

3.  微型端口驱动程序等待所有所指示接收该队列要返回给微型端口驱动程序的数据包。

4.  微型端口驱动程序释放它分配为网络适配器的接收缓冲区通过调用与队列关联的所有共享的内存[ **NdisFreeSharedMemory**](https://msdn.microsoft.com/library/windows/hardware/ff562601)。

5.  微型端口驱动程序完成 OID\_接收\_筛选器\_免费\_队列 OID 请求免费接收队列。

微型端口驱动程序调用[ **NdisFreeSharedMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff562601)函数来释放队列的共享的内存。 该驱动程序微型端口驱动程序为非默认队列分配的共享的内存，如果释放 OID 的上下文中的共享的内存\_接收\_筛选器\_免费\_队列 OID 时它正在释放队列。 微型端口驱动程序免费共享默认的队列的上下文中为它们分配的内存[ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)函数。

基础驱动程序必须释放它在释放队列前在队列设置的所有筛选器。 此外，基础驱动程序必须释放它分配网络适配器调用之前的所有接收队列[ **NdisCloseAdapterEx** ](https://msdn.microsoft.com/library/windows/hardware/ff561640)函数以关闭到的网络适配器的绑定。 NDIS 释放之前它将调用微型端口驱动程序的网络适配器分配的所有队列[ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)函数。

### <a name="return-status-codes"></a>返回状态代码

微型端口驱动程序[ *MiniportOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559416)函数将返回以下值之一用于此请求：

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
<td><p>微型端口驱动程序将以异步方式完成的请求。 微型端口驱动程序已完成所有处理后，它必须请求成功通过调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff563622" data-raw-source="[&lt;strong&gt;NdisMOidRequestComplete&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563622)"> <strong>NdisMOidRequestComplete</strong> </a>函数，传递<strong>NDIS_STATUS_SUCCESS</strong>对于<em>状态</em>参数。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_NOT_ACCEPTED</strong></p></td>
<td><p>微型端口驱动程序正在重置。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_REQUEST_ABORTED</strong></p></td>
<td><p>微型端口驱动程序已停止处理请求。 例如，名为 NDIS <a href="https://msdn.microsoft.com/library/windows/hardware/ff559432" data-raw-source="[&lt;em&gt;MiniportResetEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559432)"> <em>MiniportResetEx</em> </a>函数。</p></td>
</tr>
</tbody>
</table>

 

NDIS 返回此请求的以下状态代码之一：

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
<td><p>请求的队列已成功释放。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_PENDING</strong></p></td>
<td><p>请求正在等待完成。 NDIS 将传递的最终状态代码和结果到 OID 请求完成处理程序调用方完成请求后。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_INVALID_PARAMETER</strong></p></td>
<td><p>队列标识符无效。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_INVALID_LENGTH</strong></p></td>
<td><p>信息缓冲区是太短。 NDIS 集<strong>数据</strong>。<strong>METHOD_INFORMATION</strong>。<strong>BytesNeeded</strong>中的成员<a href="https://msdn.microsoft.com/library/windows/hardware/ff566710" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566710)"> <strong>NDIS_OID_REQUEST</strong> </a>是必需的最小缓冲区大小的结构。</p></td>
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


[*MiniportHaltEx*](https://msdn.microsoft.com/library/windows/hardware/ff559388)

[**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_RECEIVE\_QUEUE\_FREE\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff567201)

[**NDIS\_状态\_接收\_队列\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff567417)

[**NdisCloseAdapterEx**](https://msdn.microsoft.com/library/windows/hardware/ff561640)

[**NdisFreeSharedMemory**](https://msdn.microsoft.com/library/windows/hardware/ff562601)

[OID\_RECEIVE\_FILTER\_ALLOCATE\_QUEUE](oid-receive-filter-allocate-queue.md)

 

 





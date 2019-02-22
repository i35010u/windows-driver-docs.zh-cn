---
title: OID_RECEIVE_FILTER_QUEUE_ALLOCATION_COMPLETE
description: 协议的 NDIS 驱动程序发出对象标识符 (OID) 方法请求的 OID_RECEIVE_FILTER_QUEUE_ALLOCATION_COMPLETE 通知的接收队列的当前批处理已完成分配的微型端口驱动程序。
ms.assetid: d09fcab5-4c3b-432a-ba9e-fd4269537de6
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_RECEIVE_FILTER_QUEUE_ALLOCATION_COMPLETE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 26cbf5558694d14e1e788235a43b80081453be5a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554122"
---
# <a name="oidreceivefilterqueueallocationcomplete"></a>OID\_接收\_筛选器\_队列\_分配\_完成


协议的 NDIS 驱动程序发出对象标识符 (OID) 方法请求的 OID\_接收\_筛选器\_队列\_分配\_完成通知分配已完成的微型端口驱动程序接收队列的当前批处理。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向[ **NDIS\_接收\_队列\_分配\_完成\_数组**](https://msdn.microsoft.com/library/windows/hardware/ff567195)结构，后跟[ **NDIS\_接收\_队列\_分配\_完成\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567197)结构为每个队列。 通过 OID 方法请求成功返回后**InformationBuffer**的成员**NDIS\_OID\_请求**结构包含指向同一数组的指针结构，并**CompletionStatus**的每个成员**NDIS\_接收\_队列\_分配\_完成\_参数**结构包含每个队列的完成状态。

<a name="remarks"></a>备注
-------

OID 方法请求的 OID\_接收\_筛选器\_队列\_分配\_完成是可选的 NDIS 6.20 和更高版本的微型端口驱动程序。 它是必需的支持的虚拟机队列 (VMQ) 接口的微型端口驱动程序。

分配后一个或多个接收队列并根据需要设置初始筛选器，协议驱动程序必须发出 OID 方法请求的 OID\_接收\_筛选器\_队列\_分配\_为了通知的接收队列的当前批处理已完成分配的微型端口驱动程序完成。 这允许微型端口驱动程序，以平衡硬件资源分到多个接收队列;如有必要，它可以为接收队列分配资源，例如共享内存。

后微型端口驱动程序将收到一个 OID\_接收\_筛选器\_队列\_分配\_完整的请求，并且它有队列设置的筛选器，该队列处于运行状态。 在此状态下，微型端口驱动程序可以通过调用开始的队列中的数据包迹象[ **NdisMIndicateReceiveNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff563598)。

### <a name="return-status-codes"></a>返回状态代码

微型端口驱动程序将返回一个 OID 的 OID 方法请求的以下状态代码\_接收\_筛选器\_队列\_分配\_完成。

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
<td><p>队列分配已完成。 包含已更新信息缓冲区<a href="https://msdn.microsoft.com/library/windows/hardware/ff567195" data-raw-source="[&lt;strong&gt;NDIS_RECEIVE_QUEUE_ALLOCATION_COMPLETE_ARRAY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567195)"> <strong>NDIS_RECEIVE_QUEUE_ALLOCATION_COMPLETE_ARRAY</strong> </a>结构和参数结构与队列分配的完成状态。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_PENDING</strong></p></td>
<td><p>请求正在等待完成。 最终状态代码和结果将传递给调用方的 OID 请求完成处理程序。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_INVALID_PARAMETER</strong></p></td>
<td><p>一个或多个基础驱动程序提供的参数不是有效的。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_INVALID_LENGTH</strong></p></td>
<td><p>信息缓冲区太短。 NDIS 集<strong>数据</strong>。<strong>METHOD_INFORMATION</strong>。<strong>BytesNeeded</strong>中的成员<a href="https://msdn.microsoft.com/library/windows/hardware/ff566710" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566710)"> <strong>NDIS_OID_REQUEST</strong> </a>是必需的最小缓冲区大小的结构。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_NOT_SUPPORTED</strong></p></td>
<td><p>微型端口驱动程序的 NDIS 版本低于版本 6.20。</p></td>
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
<td><p>版本</p></td>
<td><p>支持 NDIS 6.20 及更高版本。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NdisMIndicateReceiveNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff563598)

[**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_接收\_队列\_分配\_完成\_数组**](https://msdn.microsoft.com/library/windows/hardware/ff567195)

[**NDIS\_接收\_队列\_分配\_完成\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567197)

 

 





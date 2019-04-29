---
title: OID_RECEIVE_FILTER_ALLOCATE_QUEUE
description: 基础驱动程序发出对象标识符 (OID) 方法请求的 OID_RECEIVE_FILTER_ALLOCATE_QUEUE 分配有一组初始的配置参数的队列。
ms.assetid: 8dd7ab91-b752-46fd-ae1b-014dc0fb0157
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_RECEIVE_FILTER_ALLOCATE_QUEUE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d319435cfe9d5856dd03438343a6905598556483
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364094"
---
# <a name="oidreceivefilterallocatequeue"></a>OID\_RECEIVE\_FILTER\_ALLOCATE\_QUEUE


基础驱动程序发出对象标识符 (OID) 方法请求的 OID\_接收\_筛选器\_分配\_分配有一组初始的配置参数的队列的队列。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向[ **NDIS\_接收\_队列\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567211)结构。 通过 OID 方法请求成功返回后**InformationBuffer**的成员**NDIS\_OID\_请求**结构包含一个指向**NDIS\_接收\_队列\_参数**结构，它具有一个新的队列标识符。

<a name="remarks"></a>备注
-------

OID 方法请求的 OID\_接收\_筛选器\_分配\_队列是可选的 NDIS 6.20 和更高版本的微型端口驱动程序。 它是必需的支持的虚拟机队列 (VMQ) 接口的微型端口驱动程序。

基础驱动程序初始化[ **NDIS\_接收\_队列\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567211)结构，其请求的队列配置。 NDIS 分配中的队列标识符**QueueId**的成员**NDIS\_接收\_队列\_参数**结构，并将传递到方法请求微型端口驱动程序。

**请注意**  过量的驱动程序可以设置**NDIS\_接收\_队列\_参数\_每\_队列\_接收\_指示**并**NDIS\_接收\_队列\_参数\_预测先行\_拆分\_必需**标志在中**标志**的成员[ **NDIS\_接收\_队列\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567211)结构。 其他标志不能提供队列分配。

 

微型端口驱动程序发出的 OID 的 OID 请求后\_接收\_筛选器\_分配\_队列和它成功，队列是处于已暂停状态的句柄。

基础驱动程序必须使用 NDIS 提供了在 OID 的后续请求，例如，若要修改队列参数或释放队列的队列标识符。 队列标识符也包含在所有上的带外 (OOB) 数据[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)与队列相关联的结构。 驱动程序使用[ **NET\_缓冲区\_列表\_接收\_队列\_ID** ](https://msdn.microsoft.com/library/windows/hardware/ff568407)宏要检索的队列标识符中**NET\_缓冲区\_列表**结构。

当 NDIS 收到 OID 请求分配接收队列时，它会验证队列参数。 NDIS 分配所需的资源和队列标识符后，它将提交对基础微型端口驱动程序的 OID 请求。 队列标识符是唯一的关联的网络适配器。

通过返回微型端口驱动程序能够成功地分配必要的软件和硬件资源接收队列，如果完成 OID 请求**NDIS\_状态\_成功**。

微型端口驱动程序必须保留已分配的接收队列的队列标识符。 NDIS 以便后续调用微型端口驱动程序来接收队列上设置接收筛选器、 更改接收队列参数，或免费接收队列使用接收队列队列的标识符。

基础驱动程序会分配一个或多个接收队列，还可以选择设置初始筛选器后，必须颁发[OID\_接收\_筛选器\_队列\_分配\_完成](oid-receive-filter-queue-allocation-complete.md)设置 OID 请求用于通知微型端口驱动程序分配已完成当前批的接收队列。

如果没有该队列上设置筛选器，微型端口驱动程序必须保留在接收队列中的任何数据包。 如果队列从未遇到过设置任何筛选器，或已清除所有筛选器，队列应为空，并且应丢弃任何数据包。 也就是说，数据包不指示驱动程序堆栈中向上或保持在队列中。

基础驱动程序使用的 OID 请求[OID\_接收\_筛选器\_免费\_队列](oid-receive-filter-free-queue.md)来释放它们所分配的队列。

### <a name="return-status-codes"></a>返回状态代码

NDIS 或微型端口驱动程序返回一个 OID 的 OID 方法请求的以下状态代码\_接收\_筛选器\_分配\_队列。

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
<td><p>队列已成功分配。 包含已更新信息缓冲区<a href="https://msdn.microsoft.com/library/windows/hardware/ff567211" data-raw-source="[&lt;strong&gt;NDIS_RECEIVE_QUEUE_PARAMETERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567211)"> <strong>NDIS_RECEIVE_QUEUE_PARAMETERS</strong> </a>结构。</p></td>
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


[**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NET\_BUFFER\_LIST**](https://msdn.microsoft.com/library/windows/hardware/ff568388)

[**NET\_缓冲区\_列表\_接收\_队列\_ID**](https://msdn.microsoft.com/library/windows/hardware/ff568407)

[OID\_RECEIVE\_FILTER\_FREE\_QUEUE](oid-receive-filter-free-queue.md)

[OID\_接收\_筛选器\_队列\_分配\_完成](oid-receive-filter-queue-allocation-complete.md)

[**NDIS\_RECEIVE\_QUEUE\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff567211)

 

 





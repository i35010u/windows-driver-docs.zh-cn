---
title: OID_RECEIVE_FILTER_CLEAR_FILTER
description: OID 过量驱动程序问题设置请求的 OID_RECEIVE_FILTER_CLEAR_FILTER，若要清除的网络适配器的接收筛选器。
ms.assetid: 5e92a11a-468e-431d-b4e5-7b0da3847e8a
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_RECEIVE_FILTER_CLEAR_FILTER 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 00135aa3af9c79964fcdfa14622421b3a256598e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380893"
---
# <a name="oidreceivefilterclearfilter"></a>OID\_RECEIVE\_FILTER\_CLEAR\_FILTER


过量驱动程序问题 OID 设置请求的 OID\_接收\_筛选器\_清除\_要清除的网络适配器的接收筛选器筛选器。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向[ **NDIS\_接收\_筛选器\_清除\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567166)结构。

<a name="remarks"></a>备注
-------

NDIS 接收筛选器在以下的 NDIS 接口中使用：

-   [NDIS 数据包合并](https://msdn.microsoft.com/library/windows/hardware/hh451601)。 详细了解如何使用此接口中接收的筛选器，请参阅[管理数据包合并接收筛选器](https://msdn.microsoft.com/library/windows/hardware/hh464026)。

-   [单根 I/O 虚拟化 (SR-IOV)](https://msdn.microsoft.com/library/windows/hardware/hh440235)。 详细了解如何使用此接口中接收的筛选器，请参阅[上虚拟端口设置接收的筛选器](https://msdn.microsoft.com/library/windows/hardware/hh440224)。

-   [虚拟机队列 (VMQ)](https://msdn.microsoft.com/library/windows/hardware/ff571035)。 详细了解如何使用此接口中接收的筛选器，请参阅[设置和清除 VMQ 筛选器](https://msdn.microsoft.com/library/windows/hardware/ff570780)。

OID 设置请求的 OID\_接收\_筛选器\_清除\_筛选器是必需的支持 NDIS 数据包合并、 SR-IOV 或 VMQ 接口的微型端口驱动程序。

基础驱动程序，如 NDIS 协议或筛选器驱动程序，使用 OID\_接收\_筛选器\_清除\_设置请求要清除以前设置的筛选器筛选器。 设置接收筛选器的驱动程序可将其清除。

基础驱动程序通过设置清除接收筛选器**FilterId**的成员[ **NDIS\_接收\_筛选器\_清除\_参数** ](https://msdn.microsoft.com/library/windows/hardware/ff567166)结构与筛选器的标识符。 该驱动程序从较早的 OID 方法请求获取筛选器标识符[OID\_接收\_筛选器\_设置\_筛选器](oid-receive-filter-set-filter.md)。

### <a name="additional-instructions-for-ndis-packet-coalescing"></a>其他说明 ndis 数据包合并

以下点适用于微型端口和支持 NDIS 数据包合并的基础驱动程序：

-   基础驱动程序必须清除解除绑定或从该驱动程序中分离之前设置微型端口驱动程序的所有接收筛选器。

### <a name="additional-guidelines-for-the-sr-iov-interface"></a>SR-IOV 接口的其他准则

以下几点适用于微型端口和基础驱动程序支持 SR-IOV 接口：

-   基础驱动程序必须清除之前释放 VPort 设置 SR-IOV VPort 的所有筛选器。 基础驱动程序还必须清除它默认 VPort，然后设置就会关闭其绑定到的网络适配器的所有筛选器。

-   如果它已完成的 OID OID 请求微型端口驱动程序必须指示数据包上非默认 VPort\_接收\_筛选器\_清除\_筛选器以清除 VPort 上的最后一个筛选器。

    **请注意**  微型端口驱动程序还必须指示上非默认 VPort 数据包是否已完成的 OID 请求[OID\_NIC\_开关\_删除\_VPORT](oid-nic-switch-delete-vport.md)来释放 VPort。

     

### <a name="additional-guidelines-for-the-vmq-interface"></a>VMQ 接口的其他准则

以下几点适用于微型端口和基础驱动程序支持 VMQ 接口：

-   基础驱动程序必须清除所有它 VMQ 设置的筛选器接收队列之前释放队列。 基础驱动程序还必须清除它的默认值或删除队列，然后设置关闭其绑定到的网络适配器的所有筛选器。

-   如果它已完成的 OID OID 请求微型端口驱动程序必须指示接收队列上的数据包\_接收\_筛选器\_清除\_筛选器以清除接收队列上的最后一个筛选器。

    **请注意**  微型端口驱动程序还必须指示接收队列上的数据包如果它已完成的 OID 请求[OID\_接收\_筛选器\_免费\_队列](oid-receive-filter-free-queue.md)来释放接收队列。

     

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
<td><p>微型端口适配器已意外删除。</p></td>
</tr>
</tbody>
</table>

 

NDIS 返回此请求的以下状态代码之一：

<a href="" id="ndis-status-success"></a>**NDIS\_状态\_成功**  
已成功清除指定的筛选器。

<a href="" id="ndis-status-pending"></a>**NDIS\_状态\_PENDING**  
请求正在等待完成。 NDIS 将传递的最终状态代码和结果到 OID 请求完成处理程序的调用方完成请求之后。

<a href="" id="ndis-status-file-not-found"></a>**NDIS\_状态\_文件\_不\_找到**  
筛选器标识符无效。

<a href="" id="ndis-status-invalid-length"></a>**NDIS\_状态\_无效\_长度**  
信息缓冲区因过小。 NDIS 集**数据。设置\_信息。BytesNeeded**中的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)是必需的最小缓冲区大小的结构。

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

[**NDIS\_RECEIVE\_FILTER\_CLEAR\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff567166)

[OID\_NIC\_交换机\_删除\_VPORT](oid-nic-switch-delete-vport.md)

[OID\_RECEIVE\_FILTER\_FREE\_QUEUE](oid-receive-filter-free-queue.md)

[OID\_RECEIVE\_FILTER\_SET\_FILTER](oid-receive-filter-set-filter.md)

 

 





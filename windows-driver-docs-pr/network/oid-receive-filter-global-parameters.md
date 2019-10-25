---
title: OID_RECEIVE_FILTER_GLOBAL_PARAMETERS
description: 过量驱动程序发出 OID 查询请求 OID_RECEIVE_FILTER_GLOBAL_PARAMETERS，以获取网络适配器的全局接收筛选参数。
ms.assetid: be6f7210-d1f9-4490-838a-806488df41da
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_RECEIVE_FILTER_GLOBAL_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 5d5d7bb47fce54f51b0b6a26b41c7d13e669ed62
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844009"
---
# <a name="oid_receive_filter_global_parameters"></a>OID\_接收\_筛选器\_全局\_参数


过量驱动程序发出 oid 查询请求，\_接收\_FILTER\_全局\_参数以获取网络适配器的全局接收筛选参数。

成功从 OID 查询请求返回后， [**ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**ndis\_\_筛选器的指针\_全局\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_global_parameters)结构。

<a name="remarks"></a>备注
-------

NDIS 接收筛选器在以下 NDIS 接口中使用：

-   [NDIS 数据包合并](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-packet-coalescing)。 有关如何在此接口中使用接收筛选器的详细信息，请参阅[管理包合并接收筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/managing-packet-coalescing-receive-filters)。

-   [单个根 I/o 虚拟化（sr-iov）](https://docs.microsoft.com/windows-hardware/drivers/network/single-root-i-o-virtualization--sr-iov-)。 有关如何在此接口中使用接收筛选器的详细信息，请参阅[设置虚拟端口上的接收筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/setting-a-receive-filter-on-a-virtual-port)。

-   [虚拟机队列 (VMQ)](https://docs.microsoft.com/windows-hardware/drivers/network/virtual-machine-queue--vmq--in-ndis-6-20)。 有关如何在此接口中使用接收筛选器的详细信息，请参阅[设置和清除 VMQ 筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/setting-and-clearing-vmq-filters)。

从 NDIS 6.20 开始，协议驱动程序使用 OID\_接收\_筛选器\_全局\_参数，以便在网络适配器上查询接收筛选的当前全局配置参数。 例如，协议驱动程序可以使用此 OID 来确定是启用还是禁用接收队列的类型。

### <a name="return-status-codes"></a>返回状态代码

NDIS 处理 OID\_接收\_筛选器的 OID 查询请求\_微型端口驱动程序的全局\_参数，并返回以下状态代码之一：

<a href="" id="ndis-status-success"></a>成功的 NDIS\_状态\_  
请求已成功完成。

<a href="" id="ndis-status-pending"></a>NDIS\_状态\_挂起  
请求正在等待完成。 请求完成后，NDIS 会将最终状态代码和结果传递给调用方的 OID 请求完成处理程序。

<a href="" id="ndis-status-invalid-length"></a>NDIS\_状态\_无效的\_长度  
信息缓冲区太短。 NDIS 设置**数据。查询\_信息。** \_OID 中的 BytesNeeded 成员[ **\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构到所需的最小缓冲区大小。

<a href="" id="ndis-status-invalid-parameter"></a>NDIS\_状态\_无效\_参数  
请求失败，因为它尝试启用基础网络适配器不支持的功能。

<a href="" id="ndis-status-failure"></a>\_故障时的 NDIS\_状态  
由于其他原因，请求失败。

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

[**NDIS\_接收\_筛选器\_全局\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_global_parameters)

 

 





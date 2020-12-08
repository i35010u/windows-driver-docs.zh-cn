---
title: OID_RECEIVE_FILTER_GLOBAL_PARAMETERS
description: 过量驱动程序发出 OID 查询请求，OID_RECEIVE_FILTER_GLOBAL_PARAMETERS 获取网络适配器的全局接收筛选参数。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_RECEIVE_FILTER_GLOBAL_PARAMETERS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 043ef64ef65d267de5146014f0a586021fcc7435
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786077"
---
# <a name="oid_receive_filter_global_parameters"></a>OID \_ 接收 \_ 筛选器 \_ 全局 \_ 参数


过量驱动程序发出 oid 查询请求，OID \_ 接收 \_ 筛选器 \_ 全局 \_ 参数用于获取网络适配器的全局接收筛选参数。

成功从 OID 查询请求返回后， [**ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 **InformationBuffer** 成员包含指向 [**ndis \_ 接收 \_ 筛选器 \_ 全局 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_global_parameters)结构的指针。

<a name="remarks"></a>备注
-------

NDIS 接收筛选器在以下 NDIS 接口中使用：

-   [NDIS 数据包合并](./ndis-packet-coalescing.md)。 有关如何在此接口中使用接收筛选器的详细信息，请参阅 [管理包合并接收筛选器](./guidelines-for-managing-packet-coalescing-receive-filters.md)。

-   [单个根 I/o 虚拟化 (sr-iov) ](./single-root-i-o-virtualization--sr-iov-.md)。 有关如何在此接口中使用接收筛选器的详细信息，请参阅 [设置虚拟端口上的接收筛选器](./setting-a-receive-filter-on-a-virtual-port.md)。

-   [虚拟机队列 (VMQ)](./virtual-machine-queue--vmq--in-ndis-6-20.md)。 有关如何在此接口中使用接收筛选器的详细信息，请参阅 [设置和清除 VMQ 筛选器](./setting-and-clearing-vmq-filters.md)。

从 NDIS 6.20 开始，协议驱动程序使用 OID \_ 接收 \_ 筛选器 \_ 全局参数在 \_ 网络适配器上查询接收筛选的当前全局配置参数。 例如，协议驱动程序可以使用此 OID 来确定是启用还是禁用接收队列的类型。

### <a name="return-status-codes"></a>返回状态代码

NDIS 处理 \_ \_ 多端口驱动程序的 oid 接收筛选器全局参数的 oid 查询请求 \_ \_ ，并返回以下状态代码之一：

<a href="" id="ndis-status-success"></a>NDIS \_ 状态 \_ 成功  
请求已成功完成。

<a href="" id="ndis-status-pending"></a>NDIS \_ 状态 \_ 挂起  
请求正在等待完成。 请求完成后，NDIS 会将最终状态代码和结果传递给调用方的 OID 请求完成处理程序。

<a href="" id="ndis-status-invalid-length"></a>NDIS \_ 状态 \_ 无效 \_ 长度  
信息缓冲区太短。 NDIS 设置 **数据。查询 \_ 信息。** 将 [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request) 结构中的成员 BytesNeeded 为所需的最小缓冲区大小。

<a href="" id="ndis-status-invalid-parameter"></a>NDIS \_ 状态 \_ 无效 \_ 参数  
请求失败，因为它尝试启用基础网络适配器不支持的功能。

<a href="" id="ndis-status-failure"></a>NDIS \_ 状态 \_ 故障  
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
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS \_ 接收 \_ 筛选器 \_ 全局 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_global_parameters)


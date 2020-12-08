---
title: OID_RECEIVE_FILTER_PARAMETERS
description: 过量驱动程序发出 OID_RECEIVE_FILTER_PARAMETERS 的 OID 方法请求，以获取网络适配器上的筛选器的当前配置参数。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_RECEIVE_FILTER_PARAMETERS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c04f52d1d8ff94463bb99f68da6d6618a63aca6a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786067"
---
# <a name="oid_receive_filter_parameters"></a>OID \_ 接收 \_ 筛选器 \_ 参数


过量驱动程序发出 OID \_ 接收筛选器参数的 oid 方法请求 \_ \_ ，以获取网络适配器上的筛选器的当前配置参数。

[**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 **InformationBuffer** 成员包含指向 [**NDIS \_ 接收 \_ 筛选器 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)结构的指针。 NDIS 使用输入结构中的 **FilterId** 成员来确定筛选器。

成功从 OID 方法请求返回后， [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 **InformationBuffer** 成员包含指向缓冲区的指针。 此缓冲区的格式设置为包含以下内容：

-   用于指定 NDIS 接收筛选器参数的 [**ndis \_ 接收 \_ 筛选器 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters) 结构。

-   用于指定网络数据包标头中的字段筛选器测试条件的 [**NDIS \_ 接收 \_ 筛选器 \_ 字段 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters) 结构的数组。

<a name="remarks"></a>备注
-------

NDIS 接收筛选器在以下 NDIS 接口中使用：

-   [NDIS 数据包合并](./ndis-packet-coalescing.md)。 有关如何在此接口中使用接收筛选器的详细信息，请参阅 [管理包合并接收筛选器](./guidelines-for-managing-packet-coalescing-receive-filters.md)。

-   [单个根 I/o 虚拟化 (sr-iov) ](./single-root-i-o-virtualization--sr-iov-.md)。 有关如何在此接口中使用接收筛选器的详细信息，请参阅 [设置虚拟端口上的接收筛选器](./setting-a-receive-filter-on-a-virtual-port.md)。

-   [虚拟机队列 (VMQ)](./virtual-machine-queue--vmq--in-ndis-6-20.md)。 有关如何在此接口中使用接收筛选器的详细信息，请参阅 [设置和清除 VMQ 筛选器](./setting-and-clearing-vmq-filters.md)。

过量驱动程序发出 OID \_ 接收筛选器参数的 oid 方法请求 \_ \_ ，以获取在网络适配器上设置的接收筛选器的配置参数。 这包括在 VMQ 接收队列或 SR-IOV 虚拟端口上设置的接收筛选器 (VPort) ，以及下载到微型端口驱动程序的数据包合并筛选器。

过量驱动程序从 [oid \_ 接收 \_ 筛选器 \_ 集 \_ 筛选](oid-receive-filter-set-filter.md) 器的早期 oid 方法请求或 [oid \_ 接收 \_ 筛选器 \_ 枚举 \_ 筛选器](oid-receive-filter-enum-filters.md)的 oid 请求获取了筛选器标识符。

### <a name="return-status-codes"></a>返回状态代码

NDIS 处理 \_ \_ 微型端口驱动程序的 oid 接收筛选器参数的 oid 请求 \_ ，并返回以下状态代码之一：

<a href="" id="ndis-status-success"></a>NDIS \_ 状态 \_ 成功  
请求已成功完成。 **InformationBuffer** 指向 [**NDIS \_ 接收 \_ 筛选器 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)结构。

<a href="" id="ndis-status-pending"></a>NDIS \_ 状态 \_ 挂起  
请求正在等待完成。 请求完成后，NDIS 会将最终状态代码和结果传递给调用方的 OID 请求完成处理程序。

<a href="" id="ndis-status-invalid-parameter"></a>NDIS \_ 状态 \_ 无效 \_ 参数  
过量驱动程序或应用程序提供了无效的筛选器标识符。 如果筛选器标识符为零或指定了未定义的筛选器，则筛选器标识符无效。

<a href="" id="ndis-status-invalid-length"></a>NDIS \_ 状态 \_ 无效 \_ 长度  
信息缓冲区太短。 NDIS 设置 **数据。查询 \_ 信息。** 将 [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request) 结构中的成员 BytesNeeded 为所需的最小缓冲区大小。

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

[OID \_ 接收 \_ 筛选器 \_ 枚举 \_ 筛选器](oid-receive-filter-enum-filters.md)

[**NDIS \_ 接收 \_ 筛选器 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)

[OID \_ 接收 \_ 筛选器 \_ 集 \_ 筛选器](oid-receive-filter-set-filter.md)


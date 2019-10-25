---
title: OID_RECEIVE_FILTER_PARAMETERS
description: 过量驱动程序发出 OID_RECEIVE_FILTER_PARAMETERS 的 OID 方法请求，以获取网络适配器上的筛选器的当前配置参数。
ms.assetid: 1bb12945-0dad-47b9-9f44-e05efe292979
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_RECEIVE_FILTER_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d971f7c9722fd89e0b2cc62aad3e5a38507266ad
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844002"
---
# <a name="oid_receive_filter_parameters"></a>OID\_接收\_筛选器\_参数


过量驱动程序发出 OID\_接收\_FILTER\_参数的 OID 方法请求，以获取网络适配器上的筛选器的当前配置参数。

[ **\_OID 的 ndis\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS\_接收\_筛选器\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)结构的指针。 NDIS 使用输入结构中的**FilterId**成员来确定筛选器。

成功从 OID 方法请求返回后， [**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构包含一个指向**缓冲区的指针**。 此缓冲区的格式设置为包含以下内容：

-   [**Ndis\_接收\_筛选器，\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)结构，用于指定 NDIS 接收筛选器的参数。

-   一组[**NDIS\_接收\_筛选器\_字段\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters)结构，后者指定网络数据包标头中的字段的筛选器测试条件。

<a name="remarks"></a>备注
-------

NDIS 接收筛选器在以下 NDIS 接口中使用：

-   [NDIS 数据包合并](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-packet-coalescing)。 有关如何在此接口中使用接收筛选器的详细信息，请参阅[管理包合并接收筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/managing-packet-coalescing-receive-filters)。

-   [单个根 I/o 虚拟化（sr-iov）](https://docs.microsoft.com/windows-hardware/drivers/network/single-root-i-o-virtualization--sr-iov-)。 有关如何在此接口中使用接收筛选器的详细信息，请参阅[设置虚拟端口上的接收筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/setting-a-receive-filter-on-a-virtual-port)。

-   [虚拟机队列 (VMQ)](https://docs.microsoft.com/windows-hardware/drivers/network/virtual-machine-queue--vmq--in-ndis-6-20)。 有关如何在此接口中使用接收筛选器的详细信息，请参阅[设置和清除 VMQ 筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/setting-and-clearing-vmq-filters)。

过量驱动程序发出 oid\_接收\_筛选器\_参数的 OID 方法请求，以获取在网络适配器上设置的接收筛选器的配置参数。 这包括在 VMQ 接收队列或 SR-IOV 虚拟端口（VPort）上设置的接收筛选器，以及下载到微型端口驱动程序的数据包合并筛选器。

覆盖驱动程序从 Oid 的早期 OID 方法请求中获取了筛选器标识符[\_接收\_筛选器\_设置\_筛选器](oid-receive-filter-set-filter.md)，或从 OID [\_接收\_筛选器的 OID 请求\_枚举\_筛选器](oid-receive-filter-enum-filters.md)。

### <a name="return-status-codes"></a>返回状态代码

NDIS 处理 OID\_接收\_筛选器的 OID 请求\_微型端口驱动程序的参数，并返回以下状态代码之一：

<a href="" id="ndis-status-success"></a>成功的 NDIS\_状态\_  
请求已成功完成。 **InformationBuffer**指向[**NDIS\_接收\_筛选器\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)结构。

<a href="" id="ndis-status-pending"></a>NDIS\_状态\_挂起  
请求正在等待完成。 请求完成后，NDIS 会将最终状态代码和结果传递给调用方的 OID 请求完成处理程序。

<a href="" id="ndis-status-invalid-parameter"></a>NDIS\_状态\_无效\_参数  
过量驱动程序或应用程序提供了无效的筛选器标识符。 如果筛选器标识符为零或指定了未定义的筛选器，则筛选器标识符无效。

<a href="" id="ndis-status-invalid-length"></a>NDIS\_状态\_无效的\_长度  
信息缓冲区太短。 NDIS 设置**数据。查询\_信息。** \_OID 中的 BytesNeeded 成员[ **\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构到所需的最小缓冲区大小。

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

[OID\_接收\_筛选器\_枚举\_筛选器](oid-receive-filter-enum-filters.md)

[**NDIS\_接收\_筛选器\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)

[OID\_接收\_筛选器\_设置\_筛选器](oid-receive-filter-set-filter.md)

 

 





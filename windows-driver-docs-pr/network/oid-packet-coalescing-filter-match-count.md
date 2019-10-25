---
title: OID_PACKET_COALESCING_FILTER_MATCH_COUNT
description: NDIS 发出 OID_PACKET_COALESCING_FILTER_MATCH_COUNT 的 OID 查询请求，以获取网络适配器上缓存或合并的数据包数。
ms.assetid: 3325865D-A329-4562-8270-CC2F42043D48
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_PACKET_COALESCING_FILTER_MATCH_COUNT 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 8e3cee607f632cebe14ac4b508106e2de71cc88d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844072"
---
# <a name="oid_packet_coalescing_filter_match_count"></a>OID\_数据包\_合并\_筛选器\_匹配\_计数


NDIS\_数据包\_合并\_筛选\_\_器发出 oid 请求 oid 请求，以获取网络适配器上缓存或*合并*的数据包数。 如果为[NDIS 数据包合并](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-packet-coalescing)启用了适配器并且数据包与接收筛选器匹配，网络适配器将合并收到的数据包。

[ **\_OID 的 NDIS\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向分配给调用方的 ULONG64 变量的指针。 在成功返回查询请求之前，驱动程序会使用网络适配器上已匹配的接收筛选器更新 ULONG64 变量。

<a name="remarks"></a>备注
-------

从 NDIS 6.30 开始，支持[NDIS 数据包合并](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-packet-coalescing)的驱动程序必须支持 OID\_数据包\_合并的 oid 查询请求，\_筛选器\_匹配\_计数。

**注意**  支持[单一根 i/o 虚拟化（sr-iov）](https://docs.microsoft.com/windows-hardware/drivers/network/single-root-i-o-virtualization--sr-iov-)或[虚拟机队列（VMQ）](https://docs.microsoft.com/windows-hardware/drivers/network/virtual-machine-queue--vmq--in-ndis-6-20)接口的驱动程序不需要支持此 oid 的 oid 查询请求。

 

支持数据包合并的微型端口驱动程序必须为网络适配器上合并的每个已接收数据包递增 ULONG64 计数器。 如果数据包与接收筛选器匹配，而该接收筛选器过量驱动程序通过 oid 的 OID 方法请求（ [\_接收\_filter\_设置\_筛选器](oid-receive-filter-set-filter.md)），则合并数据包。

驱动程序在处理 OID 的 OID 查询请求时返回此计数器的值\_数据包\_合并\_筛选器\_匹配\_计数。

小型端口驱动程序在处理 OID\_数据包\_合并的 OID 查询请求后，不能清除计数器，\_筛选器\_匹配\_计数。 如果满足以下条件，微型端口驱动程序必须仅清除计数器：

-   微型端口驱动程序处理 Oid\_PNP 的 OID 集请求[\_将\_电源](oid-pnp-set-power.md)恢复为 NdisDeviceStateD0 的完全电源状态。

-   NDIS 调用微型端口驱动程序的[*MiniportResetEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset)函数来重置基础网络适配器。

有关数据包合并的详细信息，请参阅[NDIS 数据包合并](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)。

### <a name="return-status-codes"></a>返回状态代码

微型端口驱动程序为 oid\_数据包\_合并\_筛选器的 OID 方法请求之一返回以下状态代码之一，\_匹配\_计数：

<a href="" id="ndis-status-success"></a>成功的 NDIS\_状态\_  
OID 请求已成功完成。

<a href="" id="ndis-status-invalid-length"></a>NDIS\_状态\_无效的\_长度  
信息缓冲区太短。 驱动程序设置**数据。设置\_信息。** \_OID 中的 BytesNeeded 成员[ **\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构到所需的最小缓冲区大小。

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
<td><p>在 NDIS 6.30 和更高版本中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[*MiniportResetEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset)

[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[OID\_PNP\_集\_电源](oid-pnp-set-power.md)

[OID\_接收\_筛选器\_设置\_筛选器](oid-receive-filter-set-filter.md)

 

 





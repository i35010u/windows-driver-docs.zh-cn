---
title: OID_PACKET_COALESCING_FILTER_MATCH_COUNT
description: NDIS 发出 OID_PACKET_COALESCING_FILTER_MATCH_COUNT 的 OID 查询请求，以获取网络适配器上缓存或合并的数据包数。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_PACKET_COALESCING_FILTER_MATCH_COUNT 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 3a6909e59300d77e80454f4142cb061e31cbf684
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102249047"
---
# <a name="oid_packet_coalescing_filter_match_count"></a>OID \_ 数据包 \_ 合并 \_ 筛选器 \_ 匹配 \_ 计数


NDIS 发出 OID \_ 数据包 \_ 合并筛选器匹配计数的 oid 查询请求， \_ \_ \_ 以获取网络适配器上缓存或 *合并* 的数据包数。 如果为 [NDIS 数据包合并](./ndis-packet-coalescing.md) 启用了适配器并且数据包与接收筛选器匹配，网络适配器将合并收到的数据包。

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 成员包含指向分配给调用方的 ULONG64 变量的指针。 在成功返回查询请求之前，驱动程序会使用网络适配器上已匹配的接收筛选器更新 ULONG64 变量。

<a name="remarks"></a>备注
-------

从 NDIS 6.30 开始，支持 [NDIS 数据包合并](./ndis-packet-coalescing.md) 的驱动程序必须支持 OID 请求 oid \_ \_ \_ 筛选器 \_ 匹配 \_ 计数。

**注意**  支持 [单一根 i/o 虚拟化的驱动程序 (sr-iov)](./single-root-i-o-virtualization--sr-iov-.md) 或 [虚拟机队列 (VMQ)](./virtual-machine-queue--vmq--in-ndis-6-20.md) 接口不需要支持此 oid 的 oid 查询请求。

 

支持数据包合并的微型端口驱动程序必须为网络适配器上合并的每个已接收数据包递增 ULONG64 计数器。 如果数据包与接收筛选器匹配（过量驱动程序通过 oid [ \_ 接收 \_ 筛选器 \_ 集 \_ 筛选器](oid-receive-filter-set-filter.md)的 oid 方法请求下载到微型端口驱动程序），则会合并这些数据包。

驱动程序在处理 OID \_ 数据包 \_ 合并 \_ 筛选器 \_ 匹配 \_ 计数的 oid 查询请求时返回此计数器的值。

微型端口驱动程序在处理 OID \_ 数据包 \_ 合并 \_ 筛选器 \_ 匹配 \_ 计数的 oid 查询请求后不得清除计数器。 如果满足以下条件，微型端口驱动程序必须仅清除计数器：

-   微型端口驱动程序处理 [oid \_ PNP \_ 集 \_ 电源](oid-pnp-set-power.md) 的 oid 设置请求，以恢复到 NdisDeviceStateD0 的完全电源状态。

-   NDIS 调用微型端口驱动程序的 [*MiniportResetEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset) 函数来重置基础网络适配器。

有关数据包合并的详细信息，请参阅 [NDIS 数据包合并](/windows-hardware/drivers/ddi/_netvista/)。

### <a name="return-status-codes"></a>返回状态代码

对于 OID " \_ 数据包 \_ 合并 \_ 筛选器 \_ 匹配 \_ 计数"，微型端口驱动程序返回 oid 方法请求的下列状态之一：

<a href="" id="ndis-status-success"></a>NDIS \_ 状态 \_ 成功  
OID 请求已成功完成。

<a href="" id="ndis-status-invalid-length"></a>NDIS \_ 状态 \_ 无效 \_ 长度  
信息缓冲区太短。 驱动程序设置 **数据。设置 \_ 信息。** 将 [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request) 结构中的成员 BytesNeeded 为所需的最小缓冲区大小。

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
<td><p>Version</p></td>
<td><p>在 NDIS 6.30 和更高版本中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标题</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[*MiniportResetEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset)

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)

[OID \_ PNP \_ 设置 \_ 电源](oid-pnp-set-power.md)

[OID \_ 接收 \_ 筛选器 \_ 集 \_ 筛选器](oid-receive-filter-set-filter.md)

 


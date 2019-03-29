---
title: OID_PACKET_COALESCING_FILTER_MATCH_COUNT
description: NDIS 发出 OID_PACKET_COALESCING_FILTER_MATCH_COUNT OID 查询的请求，若要获取的已缓存，或合并的网络适配器上的数据包数。
ms.assetid: 3325865D-A329-4562-8270-CC2F42043D48
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_PACKET_COALESCING_FILTER_MATCH_COUNT 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a90580eea69d85ccf616b3793ba48617810d5678
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563694"
---
# <a name="oidpacketcoalescingfiltermatchcount"></a>OID\_数据包\_COALESCING\_筛选器\_匹配\_计数


NDIS 发出 OID 查询请求的 OID\_数据包\_COALESCING\_筛选器\_匹配\_若要获取的已缓存的数据包数的计数或*合并*上中的网络适配器。 网络适配器将合并接收的数据包，如果适配器启用了[NDIS 数据包合并](https://msdn.microsoft.com/library/windows/hardware/hh451601)和数据包与接收筛选器相匹配。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含指向调用方分配的 ULONG64 变量. 之前从查询请求成功返回时，驱动程序更新 ULONG64 变量具有匹配的数据包数与接收的网络适配器上的筛选器。

<a name="remarks"></a>备注
-------

支持的驱动程序从 NDIS 6.30 [NDIS 数据包合并](https://msdn.microsoft.com/library/windows/hardware/hh451601)必须支持 OID 查询请求的 OID\_数据包\_COALESCING\_筛选器\_匹配\_计数。

**请注意**  支持的驱动程序[单根 I/O 虚拟化 (SR-IOV)](https://msdn.microsoft.com/library/windows/hardware/hh440235)或[虚拟机队列 (VMQ)](https://msdn.microsoft.com/library/windows/hardware/ff571035)接口不支持所需的 OID 查询请求此 OID。

 

支持数据包合并的微型端口驱动程序必须递增每个网络适配器已合并的接收数据包的 ULONG64 计数器。 如果它们匹配哪些基础驱动程序下载到通过 OID 方法请求的微型端口驱动程序的接收筛选器合并了数据包[OID\_接收\_筛选器\_设置\_筛选器](oid-receive-filter-set-filter.md).

当处理 OID 的 OID 查询请求时，驱动程序将返回此计数器的值\_数据包\_COALESCING\_筛选器\_匹配\_计数。

它处理一个 OID OID 查询请求后，微型端口驱动程序必须清除该计数器\_数据包\_COALESCING\_筛选器\_匹配\_计数。 如果满足以下条件，微型端口驱动程序必须仅清除计数器：

-   微型端口驱动程序处理的 OID 集请求[OID\_PNP\_设置\_POWER](oid-pnp-set-power.md)继续 NdisDeviceStateD0 全功率状态。

-   NDIS 调用微型端口驱动程序[ *MiniportResetEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559432)函数以重置基础的网络适配器。

有关数据包合并的详细信息，请参阅[NDIS 数据包合并](https://msdn.microsoft.com/library/windows/hardware/hh205393)。

### <a name="return-status-codes"></a>返回状态代码

微型端口驱动程序将返回一个 OID 的 OID 方法请求的以下状态代码\_数据包\_COALESCING\_筛选器\_匹配\_计数：

<a href="" id="ndis-status-success"></a>NDIS\_状态\_成功  
OID 请求已成功完成。

<a href="" id="ndis-status-invalid-length"></a>NDIS\_状态\_无效\_长度  
信息缓冲区太短。 驱动程序集**数据。设置\_信息。BytesNeeded**中的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)是必需的最小缓冲区大小的结构。

<a href="" id="ndis-status-failure"></a>NDIS\_状态\_失败  
请求由于其他原因而失败。

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
<td><p>支持在 NDIS 6.30 和更高版本。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[*MiniportResetEx*](https://msdn.microsoft.com/library/windows/hardware/ff559432)

[**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[OID\_PNP\_SET\_POWER](oid-pnp-set-power.md)

[OID\_RECEIVE\_FILTER\_SET\_FILTER](oid-receive-filter-set-filter.md)

 

 





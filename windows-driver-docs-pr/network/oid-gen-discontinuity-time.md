---
title: OID_GEN_DISCONTINUITY_TIME
description: 作为查询，使用 OID_GEN_DISCONTINUITY_TIME OID 确定 (ifCounterDiscontinuityTime 从 RFC 2863) 的网络接口的中断时间。
ms.assetid: 3eac6818-c346-47f6-b812-f98b808dc36a
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_DISCONTINUITY_TIME 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 35833f792e214517a4a91cda5709e20a2b5cebdb
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213855"
---
# <a name="oid_gen_discontinuity_time"></a>OID 生成中断 \_ \_ \_ 时间


作为查询，使用 OID 生成中断 \_ \_ \_ 时间 oid 来确定 (*ifCounterDiscontinuityTime* 从 [RFC 2863](https://go.microsoft.com/fwlink/p/?linkid=84054)) 的网络接口的中断时间。

**版本信息**

<a href="" id="windows-vista-and-later"></a>Windows Vista 和更高版本  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。 仅适用于 NDIS 接口提供程序。

<a name="remarks"></a>备注
-------

只有 [NDIS 网络接口](./ndis-network-interfaces2.md) 提供程序（因此不是微型端口驱动程序或筛选器驱动程序）才能支持此 OID 作为 oid 请求。

此 OID 返回在维护统计信息计数器时，从上一次计算机重新启动开始的时间。 例如，由于接口已禁用或从计算机中删除了关联的适配器，导致了中断。 有关统计信息计数器的详细信息，请参阅 [OID \_ GEN \_ statistics](oid-gen-statistics.md)。 为获取当前时间，接口提供程序可以调用 [**NdisGetSystemUpTimeEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgetsystemuptimeex) 函数。

如果自上次重新初始化接口后没有发生此类中断，此值应为零。 如果接口提供程序不跟踪中断时间，则此值应为零。

如果接口提供程序返回 NDIS \_ 状态 \_ SUCCESS，则查询的结果是一个 ULONG64 值，该值指定自上次计算机重新启动以来的中断时间（以毫秒为单位）。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[NDIS 网络接口 Oid](./ndis-network-interface-oids.md)

 


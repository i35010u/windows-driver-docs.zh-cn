---
title: OID_GEN_DISCONTINUITY_TIME
description: 作为查询，使用 OID_GEN_DISCONTINUITY_TIME OID 来确定网络接口（ifCounterDiscontinuityTime 从 RFC 2863）的中断时间。
ms.assetid: 3eac6818-c346-47f6-b812-f98b808dc36a
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_DISCONTINUITY_TIME 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c6cf543aaf140cf97d63d7891ee30c3e395f6aed
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837986"
---
# <a name="oid_gen_discontinuity_time"></a>OID\_代\_不连续性\_时间


作为查询，使用 OID\_代\_不连续性\_时间 OID 来确定网络接口（*ifCounterDiscontinuityTime*从[RFC 2863](https://go.microsoft.com/fwlink/p/?linkid=84054)）的中断时间。

**版本信息**

<a href="" id="windows-vista-and-later"></a>Windows Vista 和更高版本  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。 仅适用于 NDIS 接口提供程序。

<a name="remarks"></a>备注
-------

只有[NDIS 网络接口](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-network-interfaces2)提供程序（因此不是微型端口驱动程序或筛选器驱动程序）才能支持此 OID 作为 oid 请求。

此 OID 返回在维护统计信息计数器时，从上一次计算机重新启动开始的时间。 例如，由于接口已禁用或从计算机中删除了关联的适配器，导致了中断。 有关统计信息计数器的详细信息，请参阅[OID\_GEN\_统计信息](oid-gen-statistics.md)。 为获取当前时间，接口提供程序可以调用[**NdisGetSystemUpTimeEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgetsystemuptimeex)函数。

如果自上次重新初始化接口后没有发生此类中断，此值应为零。 如果接口提供程序不跟踪中断时间，则此值应为零。

如果接口提供程序返回 NDIS\_状态\_SUCCESS，则查询的结果是一个 ULONG64 值，该值指定自上次计算机重新启动以来的中断时间（以毫秒为单位）。

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
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[NDIS 网络接口 Oid](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-network-interface-oids)

 

 





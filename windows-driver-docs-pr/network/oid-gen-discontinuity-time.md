---
title: OID_GEN_DISCONTINUITY_TIME
description: 为查询，使用 OID_GEN_DISCONTINUITY_TIME OID 来确定网络接口 (RFC 2863 从 ifCounterDiscontinuityTime) 的中断时间。
ms.assetid: 3eac6818-c346-47f6-b812-f98b808dc36a
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_DISCONTINUITY_TIME 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 26b11a4694eac734ce093c0863188676dc3c02ab
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369117"
---
# <a name="oidgendiscontinuitytime"></a>OID\_GEN\_中断\_时间


为查询，使用 OID\_GEN\_中断\_要确定网络接口的中断时间的时间 OID (*ifCounterDiscontinuityTime*从[RFC 2863](https://go.microsoft.com/fwlink/p/?linkid=84054)).

**版本信息**

<a href="" id="windows-vista-and-later"></a>Windows Vista 及更高版本  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。 NDIS 接口提供程序仅。

<a name="remarks"></a>备注
-------

仅[NDIS 网络接口](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-network-interfaces2)提供程序，因此不微型端口驱动程序或筛选器驱动程序必须支持此 OID 作为 OID 的请求。

此 OID 返回时，该接口必须维护的统计信息计数器的不连续性时从上次计算机重新启动，开始。 例如，出现中断由于接口被禁用或关联的适配器已从计算机中删除。 有关统计信息计数器的详细信息，请参阅[OID\_代\_统计信息](oid-gen-statistics.md)。 若要获取当前时间，接口提供程序可以调用[ **NdisGetSystemUpTimeEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisgetsystemuptimeex)函数。

如果没有此类中断以来发生了接口的最后一个重新初始化此值应为零。 如果接口提供程序不会跟踪中断时间，此值应为零。

如果接口提供程序返回 NDIS\_状态\_成功后，查询的结果是 ULONG64 值，该值指定中断时间，以毫秒为单位，自上次计算机重新启动。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[NDIS 网络接口 Oid](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-network-interface-oids)

 

 





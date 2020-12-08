---
title: NDIS_STATUS_LINK_SPEED_CHANGE
description: NDIS_STATUS_LINK_SPEED_CHANGE 状态指示链接速度发生变化。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_LINK_SPEED_CHANGE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 365df7692113ad993e47375404f9752992e584a7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801517"
---
# <a name="ndis_status_link_speed_change"></a>NDIS \_ 状态 \_ 链接 \_ 速度 \_ 更改


NDIS \_ 状态 \_ 链接 \_ 速度 \_ 更改状态指示链接速度发生变化。

<a name="remarks"></a>备注
-------

\_ \_ \_ \_ 对于过量的 ndis 6.0 驱动程序，ndis 将 ndis 状态链接速度更改状态指示转换为 [**ndis \_ 状态 \_ 链接 \_ 状态**](ndis-status-link-state.md)指示。 当 NDIS 收到 NDIS \_ 状态 \_ 链接 \_ 速度 \_ 更改状态时，ndis 会发出 oid 生成 [ \_ \_ 链接 \_ 速度](./oid-gen-link-speed.md)oid 查询请求。 NDIS 使用 OID \_ GEN \_ 链接速度查询的结果， \_ 将 ndis \_ 状态 \_ 链接 \_ 状态状态发布到过量的 ndis 6.0 驱动程序。

NDIS 5。*x* 或更低的微型端口驱动程序在 [**NdisMIndicateStatus**](/previous-versions/windows/hardware/network/ff553538(v=vs.85))函数的 *StatusBuffer* 参数处提供 DWORD 类型值。 有关 NDIS \_ 状态 \_ 链接速度更改的详细信息 \_ \_ ，请参阅 [OID \_ IRDA \_ 速率 \_ 探查](/previous-versions/windows/hardware/network/ff560287(v=vs.85))。

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
<td><p>在 NDIS 6.0 和更高版本中不受支持 (改用 <a href="ndis-status-link-state.md" data-raw-source="[&lt;strong&gt;NDIS_STATUS_LINK_STATE&lt;/strong&gt;](ndis-status-link-state.md)"><strong>NDIS_STATUS_LINK_STATE</strong></a>) 。 只有 Windows Vista 和 Windows XP 中的 NDIS 5.1 驱动程序支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td> (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS \_ 状态 \_ 链接 \_ 状态**](ndis-status-link-state.md)

[**NdisMIndicateStatus**](/previous-versions/windows/hardware/network/ff553538(v=vs.85))

[OID \_ GEN \_ LINK \_ 速度](./oid-gen-link-speed.md)

[OID \_ IRDA \_ 速率 \_ 探查](/previous-versions/windows/hardware/network/ff560287(v=vs.85))

 


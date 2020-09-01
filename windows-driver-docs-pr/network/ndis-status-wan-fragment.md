---
title: NDIS_STATUS_WAN_FRAGMENT
description: "\"NDIS_STATUS_WAN_FRAGMENT 状态\" 指示支持 WAN 的微型端口驱动程序已收到来自远程节点的部分数据包。"
ms.assetid: 1ac00110-8b97-4905-b409-454e3d9a09e0
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WAN_FRAGMENT 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 19c5641f0679ebf15d4429c89459b6b7d36550f2
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89214661"
---
# <a name="ndis_status_wan_fragment"></a>NDIS \_ 状态 \_ WAN \_ 片段


NDIS \_ 状态 \_ wan \_ 片段状态表明，支持 wan 的微型端口驱动程序已收到来自远程节点的部分数据包。

<a name="remarks"></a>备注
-------

NDIS 4。*x* 和更早的 NDIS WAN 微型端口驱动程序使用此状态指示。 NDIS 5.0 和更高版本的微型端口驱动程序应使用 CoNDIS WAN 接口。 有关 NDIS \_ 状态 wan 片段的详细信息 \_ \_ ，请参阅 [**ndis \_ 状态 \_ wan \_ 归置 \_ **](ndis-status-wan-co-fragment.md)。

[**NdisMIndicateStatus**](/previous-versions/windows/hardware/network/ff553538(v=vs.85))函数的*StatusBuffer*参数包含指向[**NDIS \_ MAC \_ 片段**](/previous-versions/windows/hardware/network/ff557055(v=vs.85))结构的指针。 NDIS \_ MAC \_ 片段用于标识特定链接，并描述接收部分数据包的原因。

有关 NDIS \_ 状态 WAN 片段的详细信息 \_ \_ ，请参阅 [指示 Ndis WAN 微型端口驱动程序状态 (ndis 5.1) ](/previous-versions/windows/hardware/network/ff546867(v=vs.85))。

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
<td><p>在 Windows Vista 或 Windows XP 中，不支持 NDIS 6.0 驱动程序或 NDIS 5.1 驱动程序。 支持 NDIS 4.x 驱动程序。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td> (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS \_ MAC \_ 片段**](/previous-versions/windows/hardware/network/ff557055(v=vs.85))

[**NDIS \_ 状态 \_ WAN \_ CO \_ 片段**](ndis-status-wan-co-fragment.md)

[**NdisMIndicateStatus**](/previous-versions/windows/hardware/network/ff553538(v=vs.85))

 


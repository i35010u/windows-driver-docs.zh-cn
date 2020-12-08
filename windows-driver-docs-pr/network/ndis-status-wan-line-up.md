---
title: NDIS_STATUS_WAN_LINE_UP
description: NDIS_STATUS_WAN_LINE_UP 状态表明，支持 WAN 的微型端口驱动程序已建立与远程节点的连接。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WAN_LINE_UP 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f7c0ec75fda52eecafa01bbdb97ca508b8ea9503
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837155"
---
# <a name="ndis_status_wan_line_up"></a>NDIS \_ 状态 \_ WAN \_ \_ 向上排列


NDIS \_ 状态 \_ wan \_ \_ 上箭头状态表明，支持 WAN 的微型端口驱动程序已建立与远程节点的连接。

<a name="remarks"></a>备注
-------

NDIS 4。*x* 和更早的 NDIS WAN 微型端口驱动程序使用此状态指示。 NDIS 5.0 和更高版本的 WAN 微型端口驱动程序必须使用 CoNDIS WAN 接口。 有关 CoNDIS WAN 接口的详细信息，请参阅在 [NDIS 5.1) 中实现 CONDIS WAN 微型端口驱动 (程序 ](/previous-versions/windows/hardware/network/ff546752(v=vs.85))。

[**NdisMIndicateStatus**](/previous-versions/windows/hardware/network/ff553538(v=vs.85))函数的 *StatusBuffer* 参数包含指向 [**NDIS \_ MAC \_ 行 \_ 向上**](/previous-versions/windows/hardware/network/ff557058(v=vs.85))结构的指针。

有关 NDIS \_ 状态 WAN 线路的详细信息 \_ \_ \_ ，请参阅 [)  (ndis 5.1 的行指示 ](/previous-versions/windows/hardware/network/ff549189(v=vs.85)) ，并 [指明 ndis WAN 微型端口驱动程序状态 (ndis 5.1) ](/previous-versions/windows/hardware/network/ff546867(v=vs.85))。

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

## <a name="see-also"></a>请参阅


[**NDIS \_ MAC \_ \_ 向上排列**](/previous-versions/windows/hardware/network/ff557058(v=vs.85))

[**NdisMIndicateStatus**](/previous-versions/windows/hardware/network/ff553538(v=vs.85))

 


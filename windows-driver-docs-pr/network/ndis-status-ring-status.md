---
title: NDIS_STATUS_RING_STATUS
description: NDIS_STATUS_RING_STATUS 状态指示线路的环状态。 支持 WAN 的微型端口驱动程序可以使用此状态报告环形故障。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_RING_STATUS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 5d2d49d7c1a8220a62e88990bd413a27ca7b80d0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837173"
---
# <a name="ndis_status_ring_status"></a>NDIS \_ 状态 \_ 环形 \_ 状态


"NDIS \_ 状态环形状态" 状态 \_ \_ 指示线路的环状态。 支持 WAN 的微型端口驱动程序可以使用此状态报告环形故障。

<a name="remarks"></a>备注
-------

NDIS 4。*x* 和更早的 NDIS WAN 微型端口驱动程序使用此状态指示。 NDIS 5.0 和更高版本的 WAN 微型端口驱动程序必须使用 CoNDIS WAN 接口。 有关 CoNDIS WAN 接口的详细信息，请参阅在 [NDIS 5.1) 中实现 CONDIS WAN 微型端口驱动 (程序 ](/previous-versions/windows/hardware/network/ff546752(v=vs.85))。

[**NdisMIndicateStatus**](/previous-versions/windows/hardware/network/ff553538(v=vs.85))函数的 *StatusBuffer* 参数包含一个具有以下状态值之一的 ULONG 值：

NDIS \_ 环形 \_ 凸 \_ 线 \_ 故障

NDIS \_ 环形 \_ 硬 \_ 错误

NDIS \_ 环形 \_ 信号 \_ 丢失

这些值指定表示状态指示原因的震铃条件。 有关 NDIS \_ 状态环形状态的详细信息 \_ \_ ，请参阅 [报表硬件状态 (NDIS 5.1) ](/previous-versions/windows/hardware/network/ff564044(v=vs.85))。

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


[**NdisMIndicateStatus**](/previous-versions/windows/hardware/network/ff553538(v=vs.85))

 


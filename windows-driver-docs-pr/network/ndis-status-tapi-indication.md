---
title: NDIS_STATUS_TAPI_INDICATION
description: NDIS_STATUS_TAPI_INDICATION 状态表明发生了 TAPI 事件。 支持 WAN 的微型端口驱动程序可以指示 TAPI 状态。
ms.assetid: b90c5524-2e03-45e1-9ec9-478112eba01b
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_TAPI_INDICATION 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 6719be7416a604cf771f00d3bd728d2c90753676
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209723"
---
# <a name="ndis_status_tapi_indication"></a>NDIS \_ 状态 \_ TAPI \_ 指示


NDIS \_ 状态 \_ tapi \_ 指示状态表明发生了 TAPI 事件。 支持 WAN 的微型端口驱动程序可以指示 TAPI 状态。

<a name="remarks"></a>备注
-------

NDIS 4。*x* 和更早的 NDIS WAN 微型端口驱动程序使用此状态指示。 NDIS 5.0 和更高版本的 WAN 微型端口驱动程序必须使用 CoNDIS WAN 接口。 有关 CoNDIS WAN 接口的详细信息，请参阅在 [NDIS 5.1) 中实现 CONDIS WAN 微型端口驱动 (程序 ](/previous-versions/windows/hardware/network/ff546752(v=vs.85))。

[**NdisMIndicateStatus**](/previous-versions/windows/hardware/network/ff553538(v=vs.85))函数的*StatusBuffer*参数包含指向[**NDIS \_ TAPI \_ 事件**](/previous-versions/windows/hardware/network/ff558986(v=vs.85))结构的指针。NDIS \_ TAPI \_ 事件结构描述了出现 (的 TAPI 线路或呼叫事件，例如：行和呼叫状态变化、传入呼叫到达，以及由远程节点或现有呼叫或线路) 的微型端口驱动程序关闭。

有关 NDIS \_ 状态 TAPI 指示的详细信息 \_ \_ ，请参阅 [指示 Ndis WAN 微型端口驱动程序状态 (ndis 5.1) ](/previous-versions/windows/hardware/network/ff546867(v=vs.85))。

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


[**NDIS \_ TAPI \_ 事件**](/previous-versions/windows/hardware/network/ff558986(v=vs.85))

[**NdisMIndicateStatus**](/previous-versions/windows/hardware/network/ff553538(v=vs.85))

 


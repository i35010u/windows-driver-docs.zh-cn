---
title: NDIS_STATUS_WAN_CO_LINKPARAMS
description: NDIS_STATUS_WAN_CO_FRAGMENT 状态指示在 CoNDIS 微型端口适配器上处于活动状态的特定 VC 的参数已更改。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WAN_CO_LINKPARAMS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 3d5d54033c5c33ad98c5b8f3025bab6f9f41a739
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837159"
---
# <a name="ndis_status_wan_co_linkparams"></a>NDIS \_ 状态 \_ WAN \_ CO \_ LINKPARAMS


NDIS \_ 状态 \_ WAN \_ CO \_ 片段状态指示在 CoNDIS 微型端口适配器上处于活动状态的特定 VC 的参数已更改。

<a name="remarks"></a>备注
-------

[**NDIS \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的 **StatusBuffer** 成员包含指向 [**WAN \_ CO \_ LINKPARAMS**](/previous-versions/windows/hardware/network/ff565819(v=vs.85))结构的指针。 WAN \_ CO \_ LINKPARAMS 结构描述 VC 的新参数。

有关 NDIS \_ 状态 \_ WAN CO LINKPARAMS 的详细信息 \_ \_ ，请参阅 [指示 CoNDIS Wan 微型端口驱动程序状态](./indicating-condis-wan-miniport-driver-status.md)。 有关 CoNDIS WAN 接口的详细信息，请参阅 [实现 CONDIS Wan 微型端口驱动程序](./implementing-condis-wan-miniport-drivers.md)。

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
<td><p>支持 Windows Vista 中的 NDIS 6.0 和 NDIS 5.1 驱动程序。 Windows XP 中的 NDIS 5.1 驱动程序支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td> (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[**WAN \_ CO \_ LINKPARAMS**](/previous-versions/windows/hardware/network/ff565819(v=vs.85))

 


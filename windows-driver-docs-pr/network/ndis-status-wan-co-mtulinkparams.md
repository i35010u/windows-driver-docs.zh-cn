---
title: NDIS_STATUS_WAN_CO_MTULINKPARAMS
description: NDIS_STATUS_WAN_CO_MTULINKPARAMS 状态表明对于在 CoNDIS 微型端口适配器上处于活动状态的特定 VC，链接速度和发送窗口参数已经发生了更改。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WAN_CO_MTULINKPARAMS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 4139968109fbb354734ce53b039175fa71343aaf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801433"
---
# <a name="ndis_status_wan_co_mtulinkparams"></a>NDIS \_ 状态 \_ WAN \_ CO \_ MTULINKPARAMS


NDIS \_ 状态 \_ WAN \_ CO \_ MTULINKPARAMS 状态指示对于在 CoNDIS 微型端口适配器上处于活动状态的特定 VC，链接速度和发送窗口参数已更改。

<a name="remarks"></a>备注
-------

[**NDIS \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的 **StatusBuffer** 成员包含指向 [**WAN \_ CO \_ MTULINKPARAMS**](/previous-versions/windows/hardware/network/ff565821(v=vs.85))结构的指针。 WAN \_ CO \_ MTULINKPARAMS 结构描述 VC 的新参数。

有关 NDIS \_ 状态 \_ WAN CO MTULINKPARAMS 的详细信息 \_ \_ ，请参阅 [指示 CoNDIS Wan 微型端口驱动程序状态](./indicating-condis-wan-miniport-driver-status.md)。 有关 CoNDIS WAN 接口的详细信息，请参阅 [实现 CONDIS Wan 微型端口驱动程序](./implementing-condis-wan-miniport-drivers.md)。

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
<td><p>在 NDIS 6.20 和更高版本中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td> (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[**WAN \_ CO \_ MTULINKPARAMS**](/previous-versions/windows/hardware/network/ff565821(v=vs.85))

 


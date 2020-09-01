---
title: NDIS_STATUS_WAN_CO_FRAGMENT
description: NDIS_STATUS_WAN_CO_FRAGMENT 状态表明 CoNDIS WAN 微型端口驱动程序已收到来自 VC 终结点的部分数据包。
ms.assetid: 5a534364-d528-45f8-a2e0-3c745b3b5ad0
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WAN_CO_FRAGMENT 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b4c430a4a53a9fe92c6a8d1b1a69dc207f3a2f6c
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211735"
---
# <a name="ndis_status_wan_co_fragment"></a>NDIS \_ 状态 \_ WAN \_ CO \_ 片段


NDIS \_ 状态 \_ wan \_ CO \_ 片段状态指示 CoNDIS WAN 微型端口驱动程序已收到来自 VC 终结点的部分数据包。

<a name="remarks"></a>备注
-------

[**Ndis \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的**StatusBuffer**成员包含指向[**NDIS \_ WAN \_ CO \_ 片段**](/previous-versions/windows/hardware/network/ff559030(v=vs.85))结构的指针。 NDIS \_ WAN \_ CO \_ 片段结构描述接收部分数据包的原因。

有关 NDIS \_ 状态 \_ WAN CO 片段的详细信息 \_ \_ ，请参阅 [指示 CoNDIS Wan 微型端口驱动程序状态](./indicating-condis-wan-miniport-driver-status.md)。 有关 CoNDIS WAN 接口的详细信息，请参阅 [实现 CONDIS Wan 微型端口驱动程序](./implementing-condis-wan-miniport-drivers.md)。

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

## <a name="see-also"></a>另请参阅


[**NDIS \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[**NDIS \_ WAN \_ CO \_ 片段**](/previous-versions/windows/hardware/network/ff559030(v=vs.85))

 


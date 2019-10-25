---
title: NDIS_STATUS_WAN_CO_FRAGMENT
description: NDIS_STATUS_WAN_CO_FRAGMENT 状态表示 CoNDIS WAN 微型端口驱动程序已收到来自 VC 终结点的部分数据包。
ms.assetid: 5a534364-d528-45f8-a2e0-3c745b3b5ad0
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WAN_CO_FRAGMENT 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 8e09b31a63c3675baf3e2f66498180567f3eb9b8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843504"
---
# <a name="ndis_status_wan_co_fragment"></a>\_WAN\_CO\_片段的 NDIS\_状态


\_WAN\_CO\_片段状态的 NDIS\_状态表明 CoNDIS WAN 微型端口驱动程序已收到来自 VC 终结点的部分数据包。

<a name="remarks"></a>备注
-------

[**Ndis\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的**StatusBuffer**成员包含指向[**NDIS\_WAN\_联\_片段**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff559030(v=vs.85))结构的指针。 NDIS\_WAN\_CO\_片段结构描述接收部分数据包的原因。

有关 NDIS\_状态\_WAN\_CO\_片段的详细信息，请参阅[指示 CONDIS Wan 微型端口驱动程序状态](https://docs.microsoft.com/windows-hardware/drivers/network/indicating-condis-wan-miniport-driver-status)。 有关 CoNDIS WAN 接口的详细信息，请参阅[实现 CONDIS Wan 微型端口驱动程序](https://docs.microsoft.com/windows-hardware/drivers/network/implementing-condis-wan-miniport-drivers)。

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
<td>Ndis .h （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[**NDIS\_WAN\_CO\_片段**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff559030(v=vs.85))

 

 





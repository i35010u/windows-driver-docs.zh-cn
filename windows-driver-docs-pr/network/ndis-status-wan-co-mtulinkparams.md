---
title: NDIS_STATUS_WAN_CO_MTULINKPARAMS
description: NDIS_STATUS_WAN_CO_MTULINKPARAMS 状态表示 CoNDIS 微型端口适配器上处于活动状态的特定 VC 的链接速度和发送窗口参数已更改。
ms.assetid: 1ba67087-08aa-4359-9884-e47bf634fda5
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WAN_CO_MTULINKPARAMS 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 05269b2d05b5d3a76a04f0f7b6e4487be7934f3e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842378"
---
# <a name="ndis_status_wan_co_mtulinkparams"></a>\_WAN\_CO\_MTULINKPARAMS 的 NDIS\_状态


\_WAN\_CO\_MTULINKPARAMS 状态的 NDIS\_状态表明对于在 CoNDIS 微型端口适配器上处于活动状态的特定 VC，链接速度和发送窗口参数已经发生了更改。

<a name="remarks"></a>备注
-------

[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的**StatusBuffer**成员包含指向[**WAN\_CO\_MTULINKPARAMS**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565821(v=vs.85))结构的指针。 WAN\_CO\_MTULINKPARAMS 结构描述 VC 的新参数。

有关 NDIS\_状态\_WAN\_CO\_MTULINKPARAMS 的详细信息，请参阅[指示 CONDIS Wan 微型端口驱动程序状态](https://docs.microsoft.com/windows-hardware/drivers/network/indicating-condis-wan-miniport-driver-status)。 有关 CoNDIS WAN 接口的详细信息，请参阅[实现 CONDIS Wan 微型端口驱动程序](https://docs.microsoft.com/windows-hardware/drivers/network/implementing-condis-wan-miniport-drivers)。

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
<td>Ndis .h （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[**WAN\_CO\_MTULINKPARAMS**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565821(v=vs.85))

 

 





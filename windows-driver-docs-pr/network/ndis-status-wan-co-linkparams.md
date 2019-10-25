---
title: NDIS_STATUS_WAN_CO_LINKPARAMS
description: NDIS_STATUS_WAN_CO_FRAGMENT 状态表示 CoNDIS 微型端口适配器上处于活动状态的特定 VC 的参数已更改。
ms.assetid: a28460fc-c9e6-49c4-949a-badd3491cdd6
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WAN_CO_LINKPARAMS 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: df3f9d0d371bd06f9734e106e5c8bd19fd3b37da
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842383"
---
# <a name="ndis_status_wan_co_linkparams"></a>\_WAN\_CO\_LINKPARAMS 的 NDIS\_状态


\_WAN\_CO\_片段状态的 NDIS\_状态指示在 CoNDIS 微型端口适配器上处于活动状态的特定 VC 的参数已更改。

<a name="remarks"></a>备注
-------

[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的**StatusBuffer**成员包含指向[**WAN\_CO\_LINKPARAMS**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565819(v=vs.85))结构的指针。 WAN\_CO\_LINKPARAMS 结构描述 VC 的新参数。

有关 NDIS\_状态\_WAN\_CO\_LINKPARAMS 的详细信息，请参阅[指示 CONDIS Wan 微型端口驱动程序状态](https://docs.microsoft.com/windows-hardware/drivers/network/indicating-condis-wan-miniport-driver-status)。 有关 CoNDIS WAN 接口的详细信息，请参阅[实现 CONDIS Wan 微型端口驱动程序](https://docs.microsoft.com/windows-hardware/drivers/network/implementing-condis-wan-miniport-drivers)。

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

[**WAN\_CO\_LINKPARAMS**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565819(v=vs.85))

 

 





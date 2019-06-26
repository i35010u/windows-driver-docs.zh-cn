---
title: NDIS_STATUS_WAN_CO_LINKPARAMS
description: NDIS_STATUS_WAN_CO_FRAGMENT 状态指示已更改的 CoNDIS 微型端口适配器处于活动状态的特定 VC 的参数。
ms.assetid: a28460fc-c9e6-49c4-949a-badd3491cdd6
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WAN_CO_LINKPARAMS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 42ec319d632142f1a1bde1dd565fbc5ceb8496e2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372559"
---
# <a name="ndisstatuswancolinkparams"></a>NDIS\_状态\_WAN\_共同\_LINKPARAMS


NDIS\_状态\_WAN\_共同\_片段状态指示已更改的 CoNDIS 微型端口适配器处于活动状态的特定 VC 的参数。

<a name="remarks"></a>备注
-------

**StatusBuffer**的成员[ **NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)结构包含一个指向[ **WAN\_共同\_LINKPARAMS** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565819(v=vs.85))结构。 WAN\_CO\_LINKPARAMS 结构为 VC 描述新的参数。

详细了解 NDIS\_状态\_WAN\_共同\_LINKPARAMS，请参阅[，该值指示的 CoNDIS WAN 微型端口驱动程序状态](https://docs.microsoft.com/windows-hardware/drivers/network/indicating-condis-wan-miniport-driver-status)。 有关的 CoNDIS WAN 接口的详细信息，请参阅[实现的 CoNDIS WAN 微型端口驱动程序](https://docs.microsoft.com/windows-hardware/drivers/network/implementing-condis-wan-miniport-drivers)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>支持 Windows Vista 中的 NDIS 6.0 和 NDIS 5.1 驱动程序。 支持 NDIS 5.1 在 Windows XP 中的驱动程序。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)

[**WAN\_CO\_LINKPARAMS**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565819(v=vs.85))

 

 





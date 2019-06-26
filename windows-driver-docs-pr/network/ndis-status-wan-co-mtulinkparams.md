---
title: NDIS_STATUS_WAN_CO_MTULINKPARAMS
description: NDIS_STATUS_WAN_CO_MTULINKPARAMS 状态指示链接速度和发送窗口参数已发生了更改的 CoNDIS 微型端口适配器处于活动状态的特定 VC。
ms.assetid: 1ba67087-08aa-4359-9884-e47bf634fda5
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WAN_CO_MTULINKPARAMS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: acd894952e035cf4352d15c6a3276047dbf6b809
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372549"
---
# <a name="ndisstatuswancomtulinkparams"></a>NDIS\_状态\_WAN\_共同\_MTULINKPARAMS


NDIS\_状态\_WAN\_共同\_MTULINKPARAMS 状态指示链接速度和发送窗口参数已发生了更改的 CoNDIS 微型端口适配器处于活动状态的特定 VC。

<a name="remarks"></a>备注
-------

**StatusBuffer**的成员[ **NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)结构包含一个指向[ **WAN\_共同\_MTULINKPARAMS** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565821(v=vs.85))结构。 WAN\_CO\_MTULINKPARAMS 结构为 VC 描述新的参数。

详细了解 NDIS\_状态\_WAN\_共同\_MTULINKPARAMS，请参阅[，该值指示的 CoNDIS WAN 微型端口驱动程序状态](https://docs.microsoft.com/windows-hardware/drivers/network/indicating-condis-wan-miniport-driver-status)。 有关的 CoNDIS WAN 接口的详细信息，请参阅[实现的 CoNDIS WAN 微型端口驱动程序](https://docs.microsoft.com/windows-hardware/drivers/network/implementing-condis-wan-miniport-drivers)。

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
<td><p>支持 NDIS 6.20 及更高版本。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)

[**WAN\_CO\_MTULINKPARAMS**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565821(v=vs.85))

 

 





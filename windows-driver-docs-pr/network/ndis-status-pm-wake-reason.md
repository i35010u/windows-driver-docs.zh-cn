---
title: NDIS_STATUS_PM_WAKE_REASON
description: NDIS_STATUS_PM_WAKE_REASON 状态指示提供有关网络适配器生成的唤醒事件的信息。
ms.assetid: 0CF29C9B-4AAA-473D-A3E8-C1E9530B595E
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_PM_WAKE_REASON 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 65c6f691911d109e164e91df6d713f22a0f15bfb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843536"
---
# <a name="ndis_status_pm_wake_reason"></a>NDIS\_状态\_PM\_唤醒\_原因


**NDIS\_状态\_PM\_唤醒\_原因**状态指示提供有关网络适配器生成的唤醒事件的信息。

<a name="remarks"></a>备注
-------

从 NDIS 6.30 开始，微型端口驱动程序会发出 ndis 状态指示， **\_状态\_PM\_唤醒\_原因**。 此状态指示通知 NDIS 和过量驱动程序，指出网络适配器生成的唤醒事件的原因。

如果微型端口驱动程序支持这种类型的状态指示，微型端口驱动程序必须在网络适配器生成唤醒信号的情况下，将**NDIS\_状态\_PM\_唤醒\_原因**状态指示。 驱动程序在处理[oid\_PNP\_集](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)的 oid 集请求时执行此操作，\_电源将适配器转换为完全电源状态。

当微型端口驱动程序发出此状态指示时，它会将[**ndis\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的**StatusBuffer**成员设置为指向[**ndis\_PM\_唤醒\_原因**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wake_reason)结构的指针。

有关如何 **\_状态\_\_\_PM 发出 ndis 状态**的详细信息，请参阅[发出 Ndis 唤醒原因状态](https://docs.microsoft.com/windows-hardware/drivers/network/issuing-ndis-wake-reason-indications)指示。

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
<td><p>在 NDIS 6.30 和更高版本中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ndis .h （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


****
[**NDIS\_PM\_唤醒\_原因**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wake_reason)

[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

 

 





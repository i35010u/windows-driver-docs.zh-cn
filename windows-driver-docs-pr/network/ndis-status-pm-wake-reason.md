---
title: NDIS_STATUS_PM_WAKE_REASON
description: NDIS_STATUS_PM_WAKE_REASON 状态指示提供有关网络适配器生成的唤醒事件的信息。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_PM_WAKE_REASON 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 369d9726d1a1dfedcf56f9d4f9b75fd84e8c25c5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801479"
---
# <a name="ndis_status_pm_wake_reason"></a>NDIS \_ 状态 \_ PM \_ 唤醒 \_ 原因


**NDIS \_ 状态 \_ PM \_ 唤醒 \_ 原因** 状态指示提供有关网络适配器生成的唤醒事件的信息。

<a name="remarks"></a>备注
-------

从 NDIS 6.30 开始，微型端口驱动程序发出 ndis 状态指示 " **ndis \_ 状态 \_ PM \_ 唤醒 \_ 原因**"。 此状态指示通知 NDIS 和过量驱动程序，指出网络适配器生成的唤醒事件的原因。

如果微型端口驱动程序支持这种类型的状态指示，则如果网络适配器生成了唤醒信号，则微型端口驱动程序必须发出 **NDIS \_ 状态 \_ PM \_ 唤醒 \_ 原因** 状态指示。 驱动程序在处理 oid [ \_ PNP \_ 设置 \_ ](./oid-pnp-set-power.md) 的 oid 设置请求时执行此操作，以便将适配器转换为完全电源状态。

当微型端口驱动程序发出此状态指示时，它会将 [**ndis \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的 **StatusBuffer** 成员设置为指向 [**ndis \_ PM \_ 唤醒 \_ 原因**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wake_reason)结构的指针。

有关如何发出 **ndis \_ 状态 \_ PM \_ 唤醒 \_ 原因** 指示的详细信息，请参阅 [发出 ndis 唤醒原因状态指示](./issuing-ndis-wake-reason-indications.md)。

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
<td> (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


****
[**NDIS \_ PM \_ 唤醒 \_ 原因**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wake_reason)

[**NDIS \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

 

